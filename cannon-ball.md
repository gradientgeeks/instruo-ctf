# Cannon Ball

## 📋 Challenge Information

- **Challenge Name**: Cannon Ball
- **Category**: Web, Steganography
- **Points**: Unknown
- **URL**: https://cannon-ball-three.vercel.app/
- **Description**: "There is something wrong with this website, but I can't put a finger on it."
- **Flag Format**: EOF{}
- **Flag**: `EOF{F0und_!t}`

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Solution Methodology](#-solution-methodology)
  - [Phase 1: Initial Website Reconnaissance](#phase-1-initial-website-reconnaissance)
  - [Phase 2: JavaScript Analysis](#phase-2-javascript-analysis)
  - [Phase 3: Hidden Resources Discovery](#phase-3-hidden-resources-discovery)
  - [Phase 4: Secondary Site Investigation](#phase-4-secondary-site-investigation)
  - [Phase 5: Image Steganography](#phase-5-image-steganography)
- [Key Insights](#key-insights)
- [Tools Used](#tools-used)
- [Complete Solution](#complete-solution)

---

## 🔍 Solution Methodology

### Phase 1: Initial Website Reconnaissance

#### Step 1: Fetch and Analyze HTML

```bash
curl -s https://cannon-ball-three.vercel.app/ > page.html
cat page.html | grep -i "EOF\|flag\|hidden"
```

**Key Findings**:
- HTML comment: `<!--RCnYi2VTt9yXtWnnmzOPL-->`
- Low opacity image element with id `f00lish-stuff` (opacity: 0.01)
- Another image with id `secret-stuff` (opacity: 0.2)

#### Step 2: Check for Hidden Elements

```bash
grep -E "opacity|display.*none|visibility.*hidden" page.html
```

**Discovery**: Multiple elements with very low opacity values designed to be nearly invisible.

### Phase 2: JavaScript Analysis

#### Step 3: Download and Analyze JavaScript Files

```bash
# Find JavaScript bundles
curl -s https://cannon-ball-three.vercel.app/ | grep -o '_next/static/chunks/[^"]*\.js' | head -5

# Download main page JavaScript
curl -s https://cannon-ball-three.vercel.app/_next/static/chunks/app/page-3e3e016d861d1eb2.js > page.js

# Search for interesting strings
strings page.js | grep -i "EOF\|flag\|secret"
```

**Findings**:
- References to `/flag.zip`
- References to `/target_hit.mp3`
- References to `/secrets.txt`

### Phase 3: Hidden Resources Discovery

#### Step 4: Download Hidden Files

```bash
# Download the hidden resources
curl -s https://cannon-ball-three.vercel.app/flag.zip > flag.zip
curl -s https://cannon-ball-three.vercel.app/target_hit.mp3 > target_hit.mp3
curl -s https://cannon-ball-three.vercel.app/secrets.txt > secrets.txt

# Check file types
file flag.zip target_hit.mp3 secrets.txt
```

**Results**:
- All three files contain base64-encoded data URIs
- `flag.zip` contains a base64 string that decodes to a URL

#### Step 5: Decode Base64 Data

```bash
# Decode flag.zip content
cat flag.zip | cut -d',' -f2 | base64 -d
# Output: https://nothing-2-see-here.vercel.app/
```

**Discovery**: A hidden secondary website!

```bash
# Decode secrets.txt to get image
cat secrets.txt | cut -d',' -f2 | base64 -d > secrets.jpg
file secrets.jpg
# Output: JPEG image data

# Decode target_hit.mp3 to get another image
cat target_hit.mp3 | cut -d',' -f2 | base64 -d > target.png
file target.png
# Output: PNG image data
```

### Phase 4: Secondary Site Investigation

#### Step 6: Analyze the Hidden Site

```bash
# Fetch the hidden site
curl -s https://nothing-2-see-here.vercel.app/ > page2.html

# Check HTML comment
grep -o '<!--[^>]*-->' page2.html
# Output: <!--c1SDEePUGiYnO0EAUsgjk-->
```

#### Step 7: Extract Secrets Image and OCR

```bash
# Run OCR on secrets.jpg
tesseract secrets.jpg stdout
```

**Output**:
```
HAVE YOU LOOKED AT EVERYTHING CLOSELY?
SORRY, THAT WAS A STRANGE THING TO ASK
```

**Hint Interpretation**: Need to examine all resources more carefully!

### Phase 5: Image Steganography

#### Step 8: Use Zsteg on PNG

```bash
# Install zsteg (if not installed)
gem install zsteg

# Run zsteg on the target.png
zsteg target.png
```

**Output**:
```
b1,r,lsb,xy         .. text: "EOF{F0und_!t}"
b1,rgb,lsb,xy       .. text: "EOF{F0und_!t}EOF{F0und_!t}"
b1,rgba,lsb,xy      .. text: "EOF{F0und_!t}EOF{F0und_!t}EOF{F0und_!t}EOF{F0und_!t}"
```

**SUCCESS!** Flag found in the LSB (Least Significant Bit) of the PNG image!

---

## Key Insights

### Challenge Design

This challenge combined multiple techniques:

1. **Web Reconnaissance**: Finding hidden resources through HTML/JS analysis
2. **Base64 Encoding**: Multiple layers of base64-encoded data URIs
3. **Multi-Stage Puzzle**: First site leads to second site
4. **Visual Misdirection**: Low opacity elements and misleading game interface
5. **Steganography**: Final flag hidden in image LSB data

### The "Something Wrong"

The challenge description said "something is wrong with this website":
- **Hidden elements** with very low opacity (0.01, 0.2)
- **Encoded resources** disguised as different file types
- **Secondary site** hidden in base64 data
- **Flag in steganography** rather than in the game itself

### Why the Game Was a Decoy

The website appeared to be a physics-based cannon game, but:
- The actual challenge wasn't about solving the physics problem
- The game was designed to distract from the hidden resources
- The "Nice try man!" message when hitting the target was intentional misdirection

---

## Tools Used

### Web Analysis
- `curl` - Download web resources
- `grep` - Search for patterns
- `strings` - Extract readable strings

### Decoding
- `base64` - Decode base64-encoded data
- `cut` - Extract base64 from data URIs

### Image Analysis
- `file` - Identify file types
- `tesseract` - OCR for reading image text
- `zsteg` - **Critical**: Extract LSB steganography from PNG
- `exiftool` - EXIF metadata examination

---

## Complete Solution

```bash
# 1. Download and analyze main page
curl -s https://cannon-ball-three.vercel.app/ > page.html

# 2. Extract hidden resources
curl -s https://cannon-ball-three.vercel.app/flag.zip > flag.zip
curl -s https://cannon-ball-three.vercel.app/target_hit.mp3 > target_hit.mp3
curl -s https://cannon-ball-three.vercel.app/secrets.txt > secrets.txt

# 3. Decode flag.zip to find hidden URL
cat flag.zip | cut -d',' -f2 | base64 -d
# Output: https://nothing-2-see-here.vercel.app/

# 4. Decode target_hit.mp3 to get PNG image
cat target_hit.mp3 | cut -d',' -f2 | base64 -d > target.png

# 5. Run zsteg to extract flag from PNG
zsteg target.png

# Output: EOF{F0und_!t}
```

---

## Summary

This web challenge perfectly demonstrated:
- The importance of thorough reconnaissance
- Not trusting the obvious interface/game
- Checking all resources including hidden ones
- Using the right steganography tools (zsteg for PNG LSB)
- Following the "LOOK AT EVERYTHING CLOSELY" hint from the secrets image

The flag `EOF{F0und_!t}` celebrates the successful discovery after examining every element of both websites! 🎯
