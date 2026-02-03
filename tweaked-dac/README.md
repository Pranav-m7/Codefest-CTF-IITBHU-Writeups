# IIT BHU Codefest CTF - Tweaked DAC Writeup (Hardware/Crypto)

![Category](https://img.shields.io/badge/Category-Hardware%20%2F%20Crypto-blueviolet)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
![Technique](https://img.shields.io/badge/Technique-Known%20Plaintext%20Attack-red)
![Math](https://img.shields.io/badge/Math-Linear%20Regression-orange)

---

## 📋 Table of Contents

- [Quick Info](#-quick-info)
- [Challenge Description](#-challenge-description)
- [Initial Analysis](#-initial-analysis)
- [The Data](#-the-data)
- [Solution Strategy: Known Plaintext Attack](#-solution-strategy-known-plaintext-attack)
- [Mathematical Foundation](#-mathematical-foundation)
- [Implementation](#-implementation)
- [Results](#-results)
- [Flag](#-flag)
- [Key Takeaways](#-key-takeaways)
- [Tools Used](#-tools-used)

---

## 📊 Quick Info

| **Attribute**       | **Details**                                      |
|---------------------|--------------------------------------------------|
| **CTF Name**        | IIT BHU Codefest CTF                             |
| **Challenge**       | Tweaked DAC                                      |
| **Category**        | Hardware / Cryptography                          |
| **Difficulty**      | Medium                                           |
| **Keywords**        | CTF Walkthrough, DAC, Digital-to-Analog Converter, Known Plaintext Attack, Linear Regression, Cryptanalysis, Hardware Security |
| **File Provided**   | `values.csv`                                     |
| **Attack Vector**   | Known Plaintext Attack + Linear Regression       |

---

## 🎯 Challenge Description

> **"We just learned about 8 bit DACs in class and my friend thinks he can encrypt the flag using it. Well he tweaked some values and now thinks it is secure."**

**Attached:** `.csv` file containing voltage values

The challenge combines hardware concepts (Digital-to-Analog Converters) with cryptographic analysis, requiring understanding of both domains to solve.

---

## 🔍 Initial Analysis

We are provided with a `.csv` file containing a single column of floating-point numbers.

### Understanding DACs

Based on the challenge description ("8-bit DAC"), these numbers represent the **voltage outputs** of a **Digital-to-Analog Converter**.

In a standard DAC scenario, characters (ASCII bytes) are converted to voltage using a fixed reference:

$$V_{out} = \frac{\text{ASCII}}{255} \times V_{ref}$$

Where:
- **ASCII**: The character's ASCII value (0-255)
- **$V_{ref}$**: Reference voltage (typically 5V in digital systems)
- **$V_{out}$**: Output voltage

### 🚨 The "Tweak"

However, the description mentions the values were **"tweaked."** This implies a non-standard transformation, likely:
- A **linear shift** (offset/intercept)
- An **arbitrary scaling factor** (slope/multiplier)

This transforms the standard equation into:

$$V = (m \times \text{ASCII}) + c$$

Where:
- **$m$**: Unknown slope (voltage step per ASCII unit)
- **$c$**: Unknown intercept (base offset voltage)

---

## 📈 The Data

Opening the CSV, we see values like:

```plaintext
1800.55
2950.12
2923.45
1778.89
...
```

### Initial Observations

- Values are **not** in the standard 0-5V range
- Simple normalization (assuming $0 = 0V$ and $255 = \text{MaxV}$) produces **garbage text**
- This confirms the "tweak" involves **unknown parameters** ($m$ and $c$)

> **Challenge:** We need to reverse-engineer the transformation without knowing the calibration parameters.

---

## 🎯 Solution Strategy: Known Plaintext Attack

Since we know the standard flag format for this CTF is `CodefestCTF{...}`, we can perform a **Known Plaintext Attack**.

### The Approach

We assume the relationship between Voltage ($V$) and ASCII character ($A$) is **linear**:

$$V = (m \times A) + c$$

Where:
- **$m$** (Slope): The voltage "step size" per ASCII unit
- **$c$** (Intercept): The base offset voltage

### Attack Steps

1. **Map the Known Prefix**
   - The first voltage $V_0$ corresponds to `'C'` (ASCII 67)
   - The second voltage $V_1$ corresponds to `'o'` (ASCII 111)
   - Continue for all 11 characters in `CodefestCTF`

2. **Calculate Parameters**
   - Use **Linear Regression** to calculate slope $m$ and intercept $c$
   - This fits the best line through our known plaintext-voltage pairs

3. **Decrypt the Full Flag**
   - Reverse the equation for every voltage value:
   
   $$A = \text{round}\left( \frac{V - c}{m} \right)$$

---

## 📐 Mathematical Foundation

### Linear Regression Formulas

Given $n$ known pairs of (ASCII, Voltage), we calculate:

**Slope ($m$):**

$$m = \frac{\sum_{i=1}^{n} (A_i - \bar{A})(V_i - \bar{V})}{\sum_{i=1}^{n} (A_i - \bar{A})^2}$$

**Intercept ($c$):**

$$c = \bar{V} - m \times \bar{A}$$

Where:
- $\bar{A}$ = Mean of known ASCII values
- $\bar{V}$ = Mean of corresponding voltage values

### Why This Works

The "tweak" is a **linear transformation**, which means:
- The relationship between ASCII and voltage is consistent
- We only need **2 points** theoretically, but using 11 points (entire prefix) gives us **robust calibration**
- Linear regression minimizes error across all known points

---

## 🛠️ Implementation

### The Solver Script

We wrote a Python script to automatically calculate the calibration using the known string `CodefestCTF`.

**Solver Script (`solver.py`):**

```python
import csv
import statistics

FILENAME = "values.csv"
KNOWN_PREFIX = "CodefestCTF" 

def solve():
    # 1. Load Data
    with open(FILENAME, 'r') as f:
        voltages = [float(row[0]) for row in csv.reader(f) if row]

    # 2. Map Known Plaintext (Linear Regression)
    known_ascii = [ord(c) for c in KNOWN_PREFIX]
    known_volts = voltages[:len(known_ascii)]

    # Calculate Slope (m) and Intercept (c)
    # m = Cov(x,y) / Var(x)
    m_x = statistics.mean(known_ascii)
    m_y = statistics.mean(known_volts)
    
    numerator = sum((known_ascii[i] - m_x) * (known_volts[i] - m_y) 
                    for i in range(len(known_ascii)))
    denominator = sum((known_ascii[i] - m_x) ** 2 
                      for i in range(len(known_ascii)))
    
    slope = numerator / denominator
    intercept = m_y - (slope * m_x)

    print(f"[+] Calculated Slope: {slope}")
    print(f"[+] Calculated Intercept: {intercept}")

    # 3. Decrypt Full Flag
    flag = ""
    for v in voltages:
        ascii_val = int(round((v - intercept) / slope))
        flag += chr(ascii_val)

    print(f"[+] Flag: {flag}")

if __name__ == "__main__":
    solve()
```

### Script Breakdown

| Step | Action | Purpose |
|------|--------|---------|
| **1** | Load CSV data | Read all voltage values into memory |
| **2** | Map known plaintext | Extract first 11 voltages corresponding to `CodefestCTF` |
| **3** | Linear regression | Calculate slope and intercept using statistical formulas |
| **4** | Decrypt all values | Apply inverse transformation to recover ASCII characters |

---

## 🎉 Results

### Running the Script

```bash
python3 solver.py
```

### Terminal Output

```plaintext
┌──(heisenberg㉿vbox)-[~/Desktop/hardware]
└─$ python3 solver.py
[+] Calibrated Slope (Step): 26.536633
[+] Calibrated Intercept:    0.067632

[+] Full Flag: CodefestCTF{s33ms_like_y0u_can_st1ll_find_1t}
```

### Analysis of Results

- **Slope: 26.536633** - The "tweak" was a multiplier of roughly **26.5x** applied to ASCII values
- **Intercept: 0.067632** - A minimal offset, close to zero
- The transformation was: $V = 26.536633 \times \text{ASCII} + 0.067632$

> **Key Insight:** By using the known flag format, we successfully bypassed the obfuscation without needing to guess the voltage parameters manually.

---

## 🚩 Flag

```
CodefestCTF{s33ms_like_y0u_can_st1ll_find_1t}
```

---

## 💡 Key Takeaways

> **What We Learned:**

### Hardware Concepts
- **DACs** convert digital values (0-255) to analog voltages
- Standard DAC equations can be "tweaked" with linear transformations
- Understanding the hardware helps identify the attack surface

### Cryptographic Concepts
- **Known Plaintext Attacks** exploit predictable message formats
- CTF flags often follow standard patterns (`CTFName{...}`)
- Even "encrypted" data with unknown parameters can be broken with partial knowledge

### Mathematical Techniques
- **Linear Regression** can reverse-engineer unknown transformation parameters
- Using multiple known points (11 characters) provides robust calibration
- The attack requires only basic statistics, not brute force

### Cross-Domain Skills
- This challenge demonstrates how **hardware security** and **cryptanalysis** intersect
- Real-world systems often have predictable formats that enable similar attacks
- "Security through obscurity" (tweaking parameters) is insufficient protection

---

## 🧰 Tools Used

| Tool          | Purpose                                      |
|---------------|----------------------------------------------|
| **Python 3**  | Scripting and data processing                |
| **CSV Module**| Reading structured voltage data              |
| **Statistics**| Calculating mean for linear regression       |
| **Math**      | Linear regression and inverse transformation |

---

## 📂 Repository Structure

```
.
├── assets/
│   ├── dac_diagram.png        # DAC concept illustration
│   └── terminal_output.png    # Screenshot of solver execution
├── values.csv                 # Challenge file (if distributable)
├── solver.py                  # Solution script
└── README.md                  # This writeup
```

---

## 📜 License

This writeup is licensed under the [MIT License](../LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** for the creative hardware/crypto challenge
- The CTF community for fostering interdisciplinary problem-solving

---

**Happy Hacking! 🎉**

[← Back to Main Index](../README.md)
