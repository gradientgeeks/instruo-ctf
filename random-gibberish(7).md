# Random Gibberish

## 📋 Challenge Information

- **Name**: Random Gibberish
- **Category**: Misc, Crypto, Steganography
- **Points**: 200
- **Teams Solved**: 8
- **Flag Format**: 

## Challenge Description

> Not all languages are simple as Python or fundamental like C, some are a path to the Dark Side.
> 
> **Hint**: Everything is there, just waiting to be found. capture the flag it will be in EOF{} format, focus on @NGFYU.txt

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Challenge Description](#challenge-description)
- [Solution Steps](#-solution-steps)
  - [Step 1: Initial File Analysis](#step-1-initial-file-analysis)
  - [Step 2: Pattern Analysis](#step-2-pattern-analysis)
  - [Step 3: Testing Various Decoding Approaches](#step-3-testing-various-decoding-approaches)
  - [Step 4: Discovery of Hidden Links](#step-4-discovery-of-hidden-links)
  - [Step 5: NGFYU Esoteric Language Discovery](#step-5-ngfyu-esoteric-language-discovery)
  - [Step 6: Running the NGFYU Code](#step-6-running-the-ngfyu-code)
  - [Step 7: Google Drive Link Discovery](#step-7-google-drive-link-discovery)
  - [Step 8: Download and Analyze the Flag Image](#step-8-download-and-analyze-the-flag-image)
  - [Step 9: Flag Extraction Attempts](#step-9-flag-extraction-attempts)
- [Key Insights](#key-insights)
- [Commands Summary](#commands-summary)
- [Flag](#flag)

---

## 🔍 Solution Steps

### Step 1: Initial File Analysis

```bash
# Check the file size
cat /home/uttam/Downloads/NGFYU.txt | wc -l
# Output: 9168 lines

# Check the end of the file
tail -n 20 /home/uttam/Downloads/NGFYU.txt
```

**Result**: File contains what appears to be "Never Gonna Give You Up" lyrics repeated in various orders.

### Step 2: Pattern Analysis

```bash
# Search for patterns
grep -n "Never gonna give you up" /home/uttam/Downloads/NGFYU.txt | head -20
```

Noticed the lyrics were reordered in different sequences - suspicious pattern suggesting encoding.

### Step 3: Testing Various Decoding Approaches

Created multiple Python scripts to test different theories:

**Attempt 1**: Extract second phrases from each line
```python
# Extract second phrase after first in each line
# Tried mapping phrases to binary patterns
```

**Attempt 2**: Map unique phrases to numbers/bits
```python
# Created mapping of first phrases to bits (0-5)
# Attempted octal and binary decoding
```

### Step 4: Discovery of Hidden Links

Found special lines in the file:

```bash
# Line 509 contained a base64 encoded string
sed -n '509,511p' /home/uttam/Downloads/NGFYU.txt

# Decoded the base64:
echo "aHR0cHM6Ly9uZXZlci1nb25uYS1may15b3UtdXAudmVyY2VsLmFwcC8=" | base64 -d
# Output: https://never-gonna-fk-you-up.vercel.app/
```

### Step 5: NGFYU Esoteric Language Discovery

The URL led to an esoteric programming language called **"NGFYU"** (Never Gonna F*** You Up):
- An esoteric language based on "Never Gonna Give You Up" lyrics
- Has an online interpreter at the discovered URL
- The entire file was written in this language!

### Step 6: Running the NGFYU Code

```python
# Created script to send code to the NGFYU interpreter API
import requests
import json

with open('/home/uttam/Downloads/NGFYU.txt', 'r') as f:
    lines = f.readlines()

# Filter out special lines (509, 511, 1751 contain metadata)
code_lines = []
for line in non_empty:
    if "Checkout" not in line and "aHR0c" not in line:
        code_lines.append(line.lower())

code = " ".join(code_lines)

# Send to NGFYU interpreter
response = requests.post(
    "https://never-gonna-fk-you-up.vercel.app/api/run",
    headers={"Content-Type": "application/json"},
    json={"action": "run", "code": code, "input": ""}
)
```

### Step 7: Google Drive Link Discovery

Another line contained a Google Drive link:

```bash
# Line 1751 had another base64 string
echo "aHR0cHM6Ly9kcml2ZS5nb29nbGUuY29tL2ZpbGUvZC8xVElyZGlpemFsRUdwTlU1YjRGUTlrMlhMUjRKc08xenAvdmlldz91c3A9c2hhcmluZw==" | base64 -d
# Output: https://drive.google.com/file/d/1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp/view?usp=sharing
```

### Step 8: Download and Analyze the Flag Image

```bash
# Download from Google Drive
FILE_ID="1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp"
curl -L "https://drive.google.com/uc?export=download&id=${FILE_ID}" -o /tmp/flag_file

# Check file type
file /tmp/flag_file
# Output: PNG image

# Copy to Downloads
cp /tmp/flag_file /home/uttam/Downloads/flag.png
ls -lh /home/uttam/Downloads/flag.png
# Output: 82K Oct 30 23:56 flag.png
```

### Step 9: Flag Extraction Attempts

Flag was written on the image. Change brightness, contrast, etc. to reveal it.

The flag.png image contains the flag either visibly or hidden using steganography tools like `zsteg`.

---

## Key Insights

### What is NGFYU Language?

- **NGFYU** (Never Gonna F*** You Up) is a custom esoteric programming language
- Uses phrases from "Never Gonna Give You Up" as programming instructions
- The interpreter is hosted at: https://never-gonna-fk-you-up.vercel.app/
- The entire challenge file is a valid NGFYU program

### Hidden Information

The file contained hidden metadata on specific lines:
- **Line 509**: Base64 encoded URL to the NGFYU interpreter
- **Line 1751**: Base64 encoded Google Drive link to flag.png

### Multi-Stage Challenge

1. Recognize it's an esoteric language (not steganography initially)
2. Find the hidden interpreter URL
3. Find the hidden Google Drive link
4. Download the flag image
5. Extract the flag from the image (likely visible or using steganography tools)

---

## Commands Summary

```bash
# File analysis
wc -l NGFYU.txt
tail -n 20 NGFYU.txt
grep -n "pattern" NGFYU.txt

# Decode base64 strings
echo "base64_string" | base64 -d

# Download from Google Drive
curl -L "https://drive.google.com/uc?export=download&id=FILE_ID" -o output.png

# Image analysis
file image.png
strings image.png | grep "flag"
exiftool image.png
```

---

## Flag

The flag is contained in the downloaded `flag.png` - either visible in the image or extractable using steganography tools (`zsteg`, `steghide`, etc.)

**Format**: `EOF{...}`

---

## Summary

This challenge cleverly combined:
- Custom esoteric programming language (NGFYU)
- Base64 encoding
- Rick Astley meme/rickroll as misdirection
- Multi-stage puzzle solving
- Steganography for final flag extraction
