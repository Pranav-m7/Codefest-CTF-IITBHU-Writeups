# IIT BHU Codefest CTF - The Wine & Wall Sculpture Writeup (OSINT)

![Category](https://img.shields.io/badge/Category-OSINT-brightgreen)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
![Technique](https://img.shields.io/badge/Technique-Reverse%20Image%20Search-blue)
![Platform](https://img.shields.io/badge/Platform-Instagram%20%7C%203D%20Warehouse-orange)

---

## 📋 Table of Contents

- [Quick Info](#-quick-info)
- [Challenge Description](#-challenge-description)
- [Challenge Objective](#-challenge-objective)
- [OSINT Methodology](#-osint-methodology)
  - [Phase 1: Visual Reconnaissance](#phase-1-visual-reconnaissance-reverse-image-search)
  - [Phase 2: Source Discovery](#phase-2-source-discovery-3d-warehouse)
  - [Phase 3: Intelligence Extraction](#phase-3-intelligence-extraction)
- [Flag Construction](#-flag-construction)
- [Flag](#-flag)
- [Key Takeaways](#-key-takeaways)
- [Tools & Resources](#-tools--resources)

---

## 📊 Quick Info

| **Attribute**       | **Details**                                      |
|---------------------|--------------------------------------------------|
| **CTF Name**        | IIT BHU Codefest CTF                             |
| **Challenge**       | The Wine & Wall Sculpture                        |
| **Category**        | OSINT (Open Source Intelligence)                 |
| **Difficulty**      | Medium                                           |
| **Keywords**        | CTF Walkthrough, OSINT, Reverse Image Search, Instagram Investigation, 3D Warehouse, Metadata Analysis, Architecture |
| **File Provided**   | Image of a wall sculpture                        |
| **Objective**       | Identify restaurant, designer, and artwork length |

---

## 🎯 Challenge Description

> **Challenge:** Identify the restaurant, the designer of its wall sculpture, and the precise length of the artwork.

**Provided:** An image showing a distinctive wall sculpture in what appears to be a restaurant setting

This advanced OSINT challenge requires multi-platform investigation, combining visual intelligence with technical metadata extraction to piece together three distinct data points.

---

## 🎯 Challenge Objective

The challenge requires identifying **three specific pieces of information**:

1. **Restaurant Name** - Where is this sculpture located?
2. **Designer Name** - Who created this artwork?
3. **Precise Length** - What are the exact dimensions of the sculpture?

All three components must be discovered through open-source intelligence gathering and combined into a single flag.

---

## 🕵️ OSINT Methodology

### Phase 1: Visual Reconnaissance (Reverse Image Search)

**Goal:** Identify the location from the provided image.

#### Methodology

I started by performing a **Reverse Image Search (RIS)** on the image of the wall sculpture using multiple tools to maximize coverage:

**Tools Used:**
- Google Lens (primary)
- Yandex Images (alternative)
- TinEye (for exact matches)

#### The Breakthrough

The search results directly linked the image to an Instagram handle:

```
@felukabeirut
```

![Instagram Discovery](./assets/instagram_search.png)

#### Verification Process

1. **Visited the Instagram profile** `@felukabeirut`
2. **Confirmed identity:** Feluka Seafood Restaurant in Beirut
3. **Cross-referenced interior photos** on the profile with the challenge image
4. **Matched the distinctive wall sculpture** visible in multiple posts

**Key Observations:**
- The Instagram handle directly reveals the restaurant name: **Feluka**
- Location confirmed: **Beirut, Lebanon**
- The "cool wall sculpture" mentioned in posts matches the challenge image
- Multiple angles of the same artwork visible in the feed

> **OSINT Tip:** Social media platforms like Instagram are goldmines for location-based OSINT. Restaurants and businesses often showcase their distinctive features, making them easily identifiable.

---

### Phase 2: Source Discovery (3D Warehouse)

**Goal:** Find technical details (Designer & Length) beyond what's visible in photos.

#### Search Strategy

With the specific restaurant name confirmed via Instagram, I needed to find **technical specifications** of the art piece. Standard image searches wouldn't provide dimensional data, so I pivoted to **3D model repositories**.

**Search Query:**
```
Feluka Seafood Restaurant wall sculpture 3D model
```

**Rationale:**
- Architectural firms often upload 3D models of custom installations
- SketchUp's 3D Warehouse is a common repository for commercial projects
- Models include metadata like dimensions, materials, and designer credits

#### The Critical Find

The search led to a specific asset hosted on **3D Warehouse** (SketchUp's repository):

**Model Details:**
- **Uploader:** `willytheboy`
- **Model Title:** "Fish Wall Sculpture for Feluka Seafood Restaurant Beirut"
- **Platform:** 3D Warehouse (SketchUp)

![3D Warehouse Model](./assets/3d_warehouse.png)

**Why This Was Important:**
- 3D models contain precise technical specifications
- Model descriptions often credit the original designer
- Dimensional data is embedded in the model properties

---

### Phase 3: Intelligence Extraction

**Goal:** Parse the metadata to extract the flag components.

#### Finding the Designer

I opened the model page on 3D Warehouse and carefully read the **Model Description** provided by the uploader `willytheboy`.

**Text Found:**
```
"Thematic Abstract Fish Sculpture designed by Waleed Abu Nassar 
for Feluka seafood restaurant..."
```

**Extracted Value:** `Waleed Abu Nassar`

**Verification:**
- Name appears in the official model description
- Consistent with Lebanese architectural design credits
- Cross-referenced with architectural databases (optional verification)

#### Finding the Length

I analyzed the **technical metrics** provided in the model data.

**Process:**
1. Examined the model's **Properties** panel
2. Reviewed **Dimensions** section
3. Identified the specific measurement: **298.9**

**Technical Note:**
- While standard bounding box dimensions were visible, the specific value `298.9` corresponds to a **curve length** or **detailed dimension**
- In complex OSINT challenges, this often requires:
  - Downloading the model file
  - Opening in SketchUp
  - Using measurement tools to extract precise dimensions
  - Checking model properties for embedded metadata

**Extracted Value:** `298.9` (likely in centimeters or a specific unit relevant to the sculpture's design)

---

## 🏗️ Flag Construction

**Goal:** Assemble the final string based on the extracted data.

### Data Collected

| Component | Value | Source |
|-----------|-------|--------|
| **Restaurant** | Feluka | Instagram handle @felukabeirut |
| **Length** | 298.9 | 3D Warehouse model properties |
| **Designer** | Waleed Abu Nassar | 3D Warehouse model description |

### Flag Format

```
CodefestCTF{Restaurant_Length_Designer_Name}
```

### Construction Process

1. **Restaurant Name:** `Feluka` (derived from the core name found via Instagram handle)
2. **Length:** `298.9` (precise measurement from 3D model)
3. **Designer Name:** `Waleed_Abu_Nassar` (formatted with underscores for multi-word name)

### Assembly

```
CodefestCTF{Feluka_298.9_Waleed_Abu_Nassar}
```

**Formatting Notes:**
- Underscores separate components
- Designer's full name included with underscores replacing spaces
- Numerical precision maintained (298.9, not rounded)
- Capitalization preserved as found in source

---

## 🚩 Flag

```
CodefestCTF{Feluka_298.9_Waleed_Abu_Nassar}
```

---

## 💡 Key Takeaways

> **What We Learned:**

### Advanced OSINT Techniques

**1. Multi-Platform Investigation**
- Single-source OSINT is rarely sufficient for complex challenges
- This challenge required **three distinct platforms**: Reverse Image Search → Instagram → 3D Warehouse
- Each platform provided a specific piece of the puzzle

**2. Social Media as Location Intelligence**
- Instagram handles often directly reveal business names
- Restaurant and business accounts showcase distinctive features
- Interior design photos provide visual confirmation
- Geotagged posts can confirm locations

**3. Technical Repository Mining**
- 3D model repositories (3D Warehouse, Sketchfab, TurboSquid) contain rich metadata
- Architectural projects often have public 3D models
- Model descriptions credit designers and provide context
- Embedded properties contain precise measurements

**4. Metadata Extraction**
- Visual data alone is insufficient for technical specifications
- Model files contain embedded dimensional data
- Descriptions often include designer credits and project details
- Cross-referencing multiple data points ensures accuracy

### OSINT Workflow for Complex Challenges

```
Visual Clue (Image)
    ↓
Reverse Image Search
    ↓
Social Media Identification (Instagram)
    ↓
Business/Location Confirmed
    ↓
Technical Repository Search (3D Warehouse)
    ↓
Metadata Extraction (Designer + Dimensions)
    ↓
Flag Construction
```

### Critical Skills Demonstrated

- **Visual Intelligence:** Identifying distinctive features in images
- **Platform Knowledge:** Knowing where to find specific types of information
- **Search Query Optimization:** Crafting effective search terms
- **Metadata Analysis:** Extracting technical data from model files
- **Cross-Referencing:** Verifying information across multiple sources

---

## 🧰 Tools & Resources

### Reverse Image Search Tools

| Tool | Purpose | URL |
|------|---------|-----|
| **Google Lens** | Primary reverse image search | lens.google.com |
| **Yandex Images** | Alternative search engine, good for international content | yandex.com/images |
| **TinEye** | Exact image matching | tineye.com |

### Social Media Platforms

| Platform | OSINT Value | Use Case |
|----------|-------------|----------|
| **Instagram** | High for businesses, locations | Restaurant identification, visual confirmation |
| **Facebook** | Business pages, reviews | Alternative verification |
| **LinkedIn** | Professional connections | Designer/architect verification |

### 3D Model Repositories

| Repository | Content Type | OSINT Value |
|------------|--------------|-------------|
| **3D Warehouse** | SketchUp models, architectural projects | High - includes metadata, descriptions |
| **Sketchfab** | 3D models, art installations | Medium - visual models, some metadata |
| **TurboSquid** | Commercial 3D models | Low - mostly paid content |

### Metadata Analysis Tools

- **SketchUp Free** - View and measure 3D Warehouse models
- **Blender** - Open various 3D file formats
- **ExifTool** - Extract metadata from images and files

---

## 📂 Repository Structure

```
.
├── assets/
│   ├── challenge_image.jpg    # Original wall sculpture image
│   ├── instagram_search.png   # Screenshot of Instagram discovery
│   ├── instagram_profile.png  # Feluka Instagram profile
│   ├── 3d_warehouse.png       # 3D Warehouse model page
│   └── model_metadata.png     # Model properties screenshot
└── README.md                  # This writeup
```

---

## 🔬 Alternative Approaches

### Method 1: Architectural Database Search

If 3D Warehouse didn't yield results:

1. Search architectural design databases (ArchDaily, Dezeen)
2. Look for Beirut restaurant design features
3. Contact design firms directly (last resort)

### Method 2: Designer-First Approach

If the designer's name was visible in the image:

1. Search for the designer's portfolio
2. Find the specific project
3. Extract restaurant name and dimensions from project details

### Method 3: Location-Based Search

If Instagram didn't work:

1. Use Google Maps to search "seafood restaurant Beirut"
2. Check restaurant websites for interior photos
3. Match distinctive features to the challenge image

---

## 🎓 Learning Resources

### OSINT Fundamentals
- [OSINT Framework](https://osintframework.com/) - Comprehensive tool directory
- [Bellingcat's Online Investigation Toolkit](https://bit.ly/bcattools)
- [Trace Labs OSINT Resources](https://www.tracelabs.org/resources)

### Social Media OSINT
- [Instagram OSINT Guide](https://www.osintcurio.us/2019/07/16/searching-instagram/)
- [Social Media Intelligence (SOCMINT)](https://www.bellingcat.com/category/resources/how-tos/)

### 3D Model Analysis
- [SketchUp 3D Warehouse](https://3dwarehouse.sketchup.com/)
- [Blender Tutorials](https://www.blender.org/support/tutorials/)

### Metadata Extraction
- [ExifTool Documentation](https://exiftool.org/)
- [Metadata Analysis Guide](https://www.sans.org/blog/metadata-analysis/)

---

## 🔒 OSINT Ethics & Legal Considerations

### Responsible OSINT Practices

> **Important:** Always conduct OSINT activities ethically and legally.

**Do:**
- ✅ Use publicly available information
- ✅ Respect platform terms of service
- ✅ Verify information across multiple sources
- ✅ Use information for educational purposes

**Don't:**
- ❌ Access private or restricted information
- ❌ Harass individuals or businesses
- ❌ Violate copyright or intellectual property rights
- ❌ Use automated scraping without permission

### Privacy Considerations

In this challenge:
- All information was publicly available
- Instagram profile was a business account (public by nature)
- 3D model was uploaded to a public repository
- No private data was accessed
- Educational context justifies the investigation

---

## 📜 License

This writeup is licensed under the [MIT License](../LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** for the creative multi-platform OSINT challenge
- **@felukabeirut** for maintaining an informative Instagram presence
- **willytheboy** for uploading the 3D model to 3D Warehouse
- **Waleed Abu Nassar** for the original sculpture design
- The OSINT community for developing excellent methodologies

---

**Happy Investigating! 🔍**

[← Back to Main Index](../README.md)

---

## 🌐 Additional Notes

### Why This Challenge Was Excellent

This challenge demonstrates **real-world OSINT scenarios**:

1. **Multi-Source Intelligence:** Real investigations require piecing together information from multiple platforms
2. **Technical Depth:** Beyond simple image searches, required understanding of 3D modeling repositories
3. **Verification:** Each piece of information could be cross-referenced and verified
4. **Practical Skills:** Techniques directly applicable to real-world investigations

### Real-World Applications

- **Architecture Research:** Identifying buildings and designers
- **Art Authentication:** Verifying artwork origins and specifications
- **Business Intelligence:** Researching companies and their assets
- **Investigative Journalism:** Tracking down sources and verifying claims

---

**Remember:** OSINT is about connecting dots across multiple sources. No single tool or platform has all the answers!
