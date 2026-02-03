# IIT BHU Codefest CTF - Nice Jam Writeup (OSINT)

![Category](https://img.shields.io/badge/Category-OSINT-brightgreen)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-success)
![Technique](https://img.shields.io/badge/Technique-Reverse%20Image%20Search-blue)
![Platform](https://img.shields.io/badge/Platform-Amazon%20Reviews-orange)

> **Note:** To display the challenge image properly, save the jam jar image as `assets/challenge_image.jpg` in this folder.

---

## 📋 Table of Contents

- [Quick Info](#-quick-info)
- [Challenge Description](#-challenge-description)
- [The Challenge Image](#-the-challenge-image)
- [Initial Analysis](#-initial-analysis)
- [OSINT Methodology](#-osint-methodology)
- [Flag Construction](#-flag-construction)
- [Flag](#-flag)
- [Key Takeaways](#-key-takeaways)

---

## 📊 Quick Info

| **Attribute**       | **Details**                                      |
|---------------------|--------------------------------------------------|
| **CTF Name**        | IIT BHU Codefest CTF                             |
| **Challenge**       | Nice Jam                                         |
| **Category**        | OSINT (Open Source Intelligence)                 |
| **Difficulty**      | Easy                                             |
| **Keywords**        | CTF Walkthrough, OSINT, Reverse Image Search, Google Lens, Amazon Reviews, Product Identification |
| **File Provided**   | Image of a jam jar                               |
| **Objective**       | Identify jam flavor and reviewer name            |

---

## 🎯 Challenge Description

> **"I saw this review online and ordered the same jam."**

**Goal:** Find the flavor of the jam and the person who made the order.

**Provided:** An image of a jam jar

This classic OSINT challenge requires identifying a physical product from visual data and then tracking down its digital footprint through online reviews.

---

## 🖼️ The Challenge Image

<div align="center">

![The Dutch Kettle Black Berry Jam](./assets/challenge_image.jpg)

**The Product:** The Dutch Kettle Amish Homemade Style Black Berry Jam

*Save the challenge image as `assets/challenge_image.jpg` to display it here*

</div>

### Visual Clues from the Image

Upon examining the provided image, several key identifiers are immediately visible:

| Visual Element | Details |
|----------------|---------|
| **Brand Name** | "THE DUTCH KETTLE" (prominently displayed at top) |
| **Product Line** | "Homemade Style" (cursive text) |
| **Flavor** | "BLACK BERRY JAM" (large text on label) |
| **Label Design** | Burlap/tan background with berry illustration |
| **Certifications** | "All Natural" and "Non GMO" badges |
| **Net Weight** | 19 oz (538 GRAMS) |
| **Jar Style** | Classic mason jar with gold screw-top lid |
| **Color** | Dark purple/black jam visible through glass |

These visual elements provide everything needed to perform an effective reverse image search and product identification.

---

## 🔍 Initial Analysis

The challenge provided an image of a jam jar and a hint about an "online review." This immediately suggests a two-phase approach:

### Phase 1: Product Identification
- Use the visual data (label, branding, packaging) to identify the specific product
- Determine the brand, product line, and flavor

### Phase 2: Digital Footprint Tracking
- Locate where this product is sold online
- Find reviews associated with the product
- Identify the specific reviewer mentioned in the challenge

> **Key Insight:** The phrase "I saw this review online and ordered" implies the review is publicly accessible on a major e-commerce platform.

---

## 🕵️ OSINT Methodology

### Step 1: Reverse Image Search

The first step in any visual OSINT challenge is to leverage reverse image search technology.

**Tools Available:**
- Google Lens (Best for commercial products)
- Yandex Images (Good for international products)
- TinEye (Best for exact image matches)

**Process:**

1. Upload the challenge image to Google Lens
2. Analyze the results for product matches

**Result:**

The search results immediately identified the brand and product line:

```
The Dutch Kettle Amish Homemade Style Jams
```

**Visual Indicators:**
- Distinctive burlap-style label design
- "THE DUTCH KETTLE" branding
- "Homemade Style" text
- Product weight: 19 oz (538 grams)

---

### Step 2: Locating the Product Source

Once the brand was identified, the next step was to find where this product is sold and reviewed online.

**Search Strategy:**

```
Search Query: "The Dutch Kettle Amish Homemade Style Jam Amazon"
```

**Why Amazon?**
- Largest e-commerce platform with extensive review system
- Challenge mentions "review online" and "ordered"
- Amazon reviews are publicly indexable and searchable

**Target Located:**

I found the specific Amazon listing for the **Black Raspberry Seedless Jam** variety, which matched the visual details in the challenge image:
- Dark purple/black color visible through the jar
- Consistency matching black raspberry jam
- Label text matching the product line

---

### Step 3: Review Enumeration

The challenge description explicitly mentioned: **"I saw this review online."**

**Process:**

1. Navigate to the **Customer Reviews** section of the Amazon product page
2. Scan through reviews looking for:
   - Recent activity
   - Verified purchases
   - Reviewer names that could be part of the flag

**Finding:**

I identified a review posted by a user named:

```
Beth Oliveri
```

> **Note:** In real OSINT scenarios, always respect privacy and terms of service. This challenge uses publicly available information for educational purposes.

---

## 🏗️ Flag Construction

The challenge required identifying two pieces of information:

1. **Flavor** of the jam
2. **Person** who made the order (reviewer)

### Data Collected

| Component | Value |
|-----------|-------|
| **Flavor** | Black Raspberry |
| **Person** | Beth Oliveri |

### Flag Format

```
CodefestCTF{Flavor_Person}
```

### Construction Process

1. Take the full flavor name: `Black Raspberry`
2. Take the full reviewer name: `Beth Oliveri`
3. Combine with underscores as separators
4. Wrap in the CTF flag format

---

## 🚩 Flag

```
CodefestCTF{Black_Raspberry_Beth_Oliveri}
```

---

## 💡 Key Takeaways

> **What We Learned:**

### OSINT Fundamentals

**1. Visual Intelligence**
- Commercial products often have distinct labels that reverse image search tools can identify instantly
- Brand names, logos, and packaging design are powerful search vectors
- Google Lens excels at identifying consumer products

**2. Platform Prediction**
- When a challenge mentions "reviews" and "ordering," Amazon is often the first place to check
- Amazon's massive indexable footprint makes it ideal for OSINT challenges
- Other platforms to consider: Walmart, Target, specialty food sites

**3. Information Correlation**
- Visual data (image) + textual hints ("review online") = complete picture
- Cross-reference multiple data points to confirm findings
- Verify product details match across sources

### Flag Formatting Best Practices

**Naming Conventions:**
- "Flavor" often implies the full variety name (e.g., `Black_Raspberry`, not just `Raspberry`)
- "Person" usually requires the full name if available (e.g., `Beth_Oliveri`, not just `Beth`)
- Use underscores to separate multi-word components
- Maintain capitalization as it appears in the source

---

## 🧰 OSINT Tools & Techniques

### Reverse Image Search Tools

| Tool | Best For | URL |
|------|----------|-----|
| **Google Lens** | Consumer products, commercial items | lens.google.com |
| **Yandex Images** | International products, faces | yandex.com/images |
| **TinEye** | Exact image matches, tracking image usage | tineye.com |
| **Bing Visual Search** | Alternative to Google | bing.com/visualsearch |

---


---

## 📜 License

This writeup is licensed under the [MIT License](../LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** for the engaging OSINT challenge
- The OSINT community for developing excellent tools and methodologies

---

**Happy Investigating! 🔍**

[← Back to Main Index](../README.md)
