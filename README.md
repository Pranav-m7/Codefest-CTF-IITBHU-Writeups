# IIT BHU Codefest CTF - Writeups Collection

![CTF](https://img.shields.io/badge/CTF-IIT%20BHU%20Codefest-red)
![Challenges Solved](https://img.shields.io/badge/Challenges%20Solved-5-success)
![Categories](https://img.shields.io/badge/Categories-Stego%20%7C%20Hardware%20%7C%20OSINT%20%7C%20Misc-blue)

---

## 📖 About This Repository

This repository contains detailed writeups for challenges solved during the **IIT BHU Codefest CTF**. Each writeup includes comprehensive methodology, tools used, and step-by-step solutions to help others learn and understand the techniques involved.

---

## 🎯 Challenges Overview

### 📊 Summary Table

| Challenge | Category | Difficulty | Points | Flag | Writeup |
|-----------|----------|------------|--------|------|---------|
| **Sanity Check** | Misc | Trivial | 50-100 | `CodefestCTF{w3lcome_70_cod3f3s7}` | [View →](./sanity-check/) |
| **Spectral Deception** | Steganography / Forensics | Medium | 388 | `CodefestCTF{secrets_of_2dfft}` | [View →](./spectral-deception/) |
| **Tweaked DAC** | Hardware / Crypto | Medium | - | `CodefestCTF{s33ms_like_y0u_can_st1ll_find_1t}` | [View →](./tweaked-dac/) |
| **Nice Jam** | OSINT | Easy | - | `CodefestCTF{Black_Raspberry_Beth_Oliveri}` | [View →](./nice-jam/) |
| **Wine & Wall Sculpture** | OSINT | Medium | - | `CodefestCTF{Feluka_298.9_Waleed_Abu_Nassar}` | [View →](./wine-wall-sculpture/) |

---

## 🔍 Challenge Details

### 1. Sanity Check
![Category](https://img.shields.io/badge/Category-Misc-purple)
![Difficulty](https://img.shields.io/badge/Difficulty-Trivial-brightgreen)
![Points](https://img.shields.io/badge/Points-50--100-success)

**Description:** "Are you sane?"

**Key Techniques:**
- Discord server interaction
- Bot command execution
- Slash commands (`/sane`, `/verify`, `/flag`)
- Platform verification
- Leetspeak decoding

**Flag:** `CodefestCTF{w3lcome_70_cod3f3s7}`

**[📄 Read Full Writeup →](./sanity-check/)**

---

### 2. Spectral Deception
![Category](https://img.shields.io/badge/Category-Steganography%20%2F%20Forensics-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
![Points](https://img.shields.io/badge/Points-388-success)

**Description:** "We intercepted this strange file. Can you make any sense of it??"

**Key Techniques:**
- NumPy array analysis
- 2D Inverse Fast Fourier Transform (IFFT)
- Frequency domain to spatial domain conversion
- Signal processing

**Flag:** `CodefestCTF{secrets_of_2dfft}`

**[📄 Read Full Writeup →](./spectral-deception/)**

---

### 3. Tweaked DAC
![Category](https://img.shields.io/badge/Category-Hardware%20%2F%20Crypto-blueviolet)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

**Description:** "We just learned about 8 bit DACs in class and my friend thinks he can encrypt the flag using it. Well he tweaked some values and now thinks it is secure."

**Key Techniques:**
- Digital-to-Analog Converter (DAC) analysis
- Known Plaintext Attack
- Linear Regression
- Cryptanalysis
- Hardware security concepts

**Flag:** `CodefestCTF{s33ms_like_y0u_can_st1ll_find_1t}`

**[📄 Read Full Writeup →](./tweaked-dac/)**

---

### 4. Nice Jam
![Category](https://img.shields.io/badge/Category-OSINT-brightgreen)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-success)

**Description:** "I saw this review online and ordered the same jam."

**Key Techniques:**
- Reverse image search (Google Lens)
- Product identification
- E-commerce platform investigation
- Amazon review enumeration
- Digital footprint tracking

**Flag:** `CodefestCTF{Black_Raspberry_Beth_Oliveri}`

**[📄 Read Full Writeup →](./nice-jam/)**

---

### 5. Wine & Wall Sculpture
![Category](https://img.shields.io/badge/Category-OSINT-brightgreen)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

**Description:** "Identify the restaurant, the designer of its wall sculpture, and the precise length of the artwork."

**Key Techniques:**
- Reverse image search (Google Lens, Yandex)
- Instagram investigation
- 3D Warehouse metadata extraction
- Multi-platform OSINT
- Technical specification analysis
- Designer attribution research

**Flag:** `CodefestCTF{Feluka_298.9_Waleed_Abu_Nassar}`

**[📄 Read Full Writeup →](./wine-wall-sculpture/)**

---

## 🛠️ Tools & Technologies Used

### By Category

**Misc:**
- Discord
- Bot interaction
- Slash commands

**Steganography / Forensics:**
- Python 3
- NumPy
- Matplotlib
- FFT/IFFT algorithms

**Hardware / Crypto:**
- Python 3
- CSV processing
- Statistics module
- Linear regression

**OSINT:**
- Google Lens
- Yandex Images
- TinEye
- Amazon platform
- Instagram investigation
- 3D Warehouse (SketchUp)
- Metadata analysis tools

---

## 📂 Repository Structure

```
.
├── sanity-check/
│   ├── README.md              # Full writeup
│   └── assets/                # Discord screenshots
│
├── spectral-deception/
│   ├── README.md              # Full writeup
│   ├── assets/                # Screenshots and images
│   ├── solve.py               # Solution script
│   └── chall.npy              # Challenge file (if distributable)
│
├── tweaked-dac/
│   ├── README.md              # Full writeup
│   ├── assets/                # Screenshots and images
│   ├── solver.py              # Solution script
│   └── values.csv             # Challenge file (if distributable)
│
├── nice-jam/
│   ├── README.md              # Full writeup
│   └── assets/                # Challenge image and screenshots
│
├── wine-wall-sculpture/
│   ├── README.md              # Full writeup
│   └── assets/                # Challenge image and screenshots
│
├── assets/                    # Shared assets
├── README.md                  # This file (main index)
└── LICENSE                    # MIT License
```

---

## 🎓 Learning Resources

### Steganography & Forensics
- [NumPy Documentation](https://numpy.org/doc/)
- [FFT Tutorial](https://www.youtube.com/watch?v=spUNpyF58BY)
- [Digital Signal Processing](https://www.coursera.org/learn/dsp)

### Hardware & Cryptography
- [DAC Fundamentals](https://en.wikipedia.org/wiki/Digital-to-analog_converter)
- [Known Plaintext Attacks](https://en.wikipedia.org/wiki/Known-plaintext_attack)
- [Linear Regression in Python](https://realpython.com/linear-regression-in-python/)

### OSINT
- [OSINT Framework](https://osintframework.com/)
- [Bellingcat's Toolkit](https://bit.ly/bcattools)
- [Google Lens Guide](https://support.google.com/websearch/answer/9099582)

---

## 🏆 CTF Statistics

| Metric | Value |
|--------|-------|
| **Total Challenges Solved** | 5 |
| **Categories Covered** | 4 (Misc, Stego, Hardware/Crypto, OSINT) |
| **Total Points** | --- |
| **Difficulty Breakdown** | Trivial: 1, Easy: 1, Medium: 3 |

---

## 🤝 Contributing

Found an alternative solution? Have suggestions for improvement? Feel free to:
- Open an issue
- Submit a pull request
- Share your own techniques

---

## 📜 License

This repository is licensed under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** organizers for creating engaging challenges
- The CTF community for fostering learning and collaboration
- All challenge authors for their creative problem designs

---

## 📞 Connect

If you found these writeups helpful:
- ⭐ Star this repository
- 🔄 Share with others learning CTF techniques
- 💬 Open discussions for alternative approaches

---

---

**Happy Hacking! 🎉**

*Last Updated: February 2026*
