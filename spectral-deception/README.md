# IIT BHU Codefest CTF - Spectral Deception Writeup (Steganography/Forensics)

![Category](https://img.shields.io/badge/Category-Steganography%20%2F%20Forensics-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
![Points](https://img.shields.io/badge/Points-388-success)
![Solves](https://img.shields.io/badge/Solves-54-informational)

---

## 📋 Table of Contents

- [Quick Info](#-quick-info)
- [Challenge Description](#-challenge-description)
- [Initial Reconnaissance](#-initial-reconnaissance)
- [Analysis & Theory](#-analysis--theory)
- [Solution](#-solution)
- [Flag](#-flag)
- [Key Takeaways](#-key-takeaways)
- [Tools Used](#-tools-used)

---

## 📊 Quick Info

| **Attribute**       | **Details**                                      |
|---------------------|--------------------------------------------------|
| **CTF Name**        | IIT BHU Codefest CTF                             |
| **Challenge**       | Spectral Deception                               |
| **Category**        | Steganography / Forensics                        |
| **Points**          | 388                                              |
| **Solves**          | 54                                               |
| **Difficulty**      | Medium                                           |
| **Keywords**        | CTF Walkthrough, Signal Processing, FFT, NumPy, Frequency Domain, Image Reconstruction |
| **File Provided**   | `chall.npy`                                      |

---

## 🎯 Challenge Description

> **"We intercepted this strange file. Can you make any sense of it??"**

**File:** `chall.npy`

The challenge provides a single NumPy array file, hinting at signal processing or data visualization techniques.

---

## 🔍 Initial Reconnaissance

The challenge provided a file named `chall.npy`. The `.npy` extension indicates a **NumPy array file**, which is a standard binary format for storing data in Python. This immediately suggests the challenge involves **signal processing** or **data visualization**.

### Step 1: Inspect the Array

First, we wrote a script to inspect the properties of the array (shape and data type) to understand what kind of data we were dealing with.

**Inspection Script:**

```python
import numpy as np

data = np.load('chall.npy')
print(f"Shape: {data.shape}")
print(f"Type:  {data.dtype}")
```

**Output:**

```plaintext
Shape: (574, 1366)
Type:  complex64
```

### 🔑 Key Observations

- **Shape `(574, 1366)`**: The data is **2-Dimensional**, suggesting it represents an image or matrix rather than a standard 1D audio signal.
- **Type `complex64`**: The data consists of **Complex Numbers** (Real + Imaginary components).

---

## 🧠 Analysis & Theory

The inspection revealed two critical clues that guided our approach:

### 1. **2D Structure**
The shape `(574, 1366)` indicates a 2D matrix, which is typical for images.

### 2. **Complex Numbers**
In image processing and signal analysis, raw images are usually stored as integers (0-255 for pixel values). However, **complex numbers** are typically the result of a **Fourier Transform**.

### 💡 The Hypothesis

The challenge title **"Spectral Deception"** confirms our theory. A **"Spectrum"** represents data in the **Frequency Domain**.

- **Spatial Domain**: Normal images (pixels at specific x, y coordinates).
- **Frequency Domain**: The same image converted into frequencies (waves).

> **Hypothesis:** The `chall.npy` file contains the **2D Frequency Spectrum** of an image. To reveal the hidden flag, we need to reverse this process and convert it back to the **Spatial Domain**.

### 🔄 The Transformation

To convert data from the **Frequency Domain** back to the **Spatial Domain**, we use the **Inverse Fast Fourier Transform (IFFT)**. Since the data is 2D, we specifically use the **2D Inverse FFT** (`ifft2`).

---

## 🛠️ Solution

### Step 2: Apply Inverse 2D FFT

We wrote the following solver script using `numpy` and `matplotlib`:

**Solver Script (`solve.py`):**

```python
import numpy as np
import matplotlib.pyplot as plt

# 1. Load the spectral data
data = np.load('chall.npy')

# 2. Perform the 2D Inverse Fast Fourier Transform
# This converts the frequency spectrum back into a spatial image.
decoded_matrix = np.fft.ifft2(data)

# 3. Process for Visualization
# The result of an IFFT is still complex numbers. To view it as an image,
# we calculate the magnitude (absolute value) of the signal.
image_data = np.abs(decoded_matrix)

# 4. Center the frequencies (Optional but good practice)
# Sometimes the zero-frequency component needs shifting, though often
# ifft2 output is viewable directly. We try the direct view first.

# 5. Plot the result
plt.figure(figsize=(10, 6))
plt.imshow(image_data, cmap='gray')
plt.title("Decoded Image (Spatial Domain)")
plt.axis('off')  # Hide axes for cleaner look
plt.show()
```

### Step 3: Run the Script

```bash
python solve.py
```

### 📸 Result

Upon running the script, the matplotlib window displayed a **grayscale image** containing clear text. The Inverse FFT successfully reconstructed the original image from the provided spectrum.

![Decoded Image](./assets/decoded_flag.png)

---

## 🚩 Flag

```
CodefestCTF{secrets_of_2dfft}
```

---

## 💡 Key Takeaways

> **What We Learned:**
> - NumPy `.npy` files can store complex numerical data, including frequency domain representations.
> - Complex numbers in image data typically indicate a **Fourier Transform** has been applied.
> - The **Inverse 2D FFT** (`np.fft.ifft2`) converts frequency domain data back to spatial domain.
> - Taking the **magnitude** (`np.abs()`) of complex IFFT results produces viewable grayscale images.
> - Challenge titles often contain hints about the technique required (e.g., "Spectral" → Frequency Spectrum).

---

## 🧰 Tools Used

| Tool          | Purpose                                      |
|---------------|----------------------------------------------|
| **Python 3**  | Scripting and data processing                |
| **NumPy**     | Loading and processing `.npy` array files    |
| **Matplotlib**| Visualizing the decoded image                |
| **FFT Theory**| Understanding frequency domain transformations |

---

## 📂 Repository Structure

```
.
├── assets/
│   └── decoded_flag.png       # Screenshot of the decoded image
├── chall.npy                  # Challenge file (if distributable)
├── solve.py                   # Solution script
└── README.md                  # This writeup
```

---

## 📜 License

This writeup is licensed under the [MIT License](../LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** for the challenge
- The CTF community for fostering learning and collaboration

---

**Happy Hacking! 🎉**

[← Back to Main Index](../README.md)
