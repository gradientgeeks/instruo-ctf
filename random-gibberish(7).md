# Random Gibberish

## 📋 Challenge Information

- **Challenge Name**: Random Gibberish (Challenge 7)
- **Category**: Misc, Crypto, Steganography
- **Points**: 200
- **Teams Solved**: 8
- **Source File**: NGFYU.txt (9168 lines)
- **Flag**: `EOF{@stley}`
- **Difficulty**: Medium (Multi-stage puzzle)

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Challenge Description](#-challenge-description)
- [Solution Phases](#-solution-phases)
  - [Phase 1: Initial File Analysis](#phase-1-initial-file-analysis)
  - [Phase 2: Pattern Recognition](#phase-2-pattern-recognition)
  - [Phase 3: Hidden Link Discovery](#phase-3-hidden-link-discovery)
  - [Phase 4: NGFYU Esoteric Language Discovery](#phase-4-ngfyu-esoteric-language-discovery)
  - [Phase 5: Image Download and Steganography](#phase-5-image-download-and-steganography)
- [Technical Summary](#technical-summary)
- [Tools Used](#tools-used)
- [Key Insights](#key-insights)
- [Files Created During Solution](#files-created-during-solution)
- [Complete Command Sequence](#complete-command-sequence)

---

## 📝 Challenge Description

> **"Not all languages are simple as Python or fundamental like C, some are a path to the Dark Side."**

**Hint**: Everything is there, just waiting to be found. Capture the flag it will be in `EOF{}` format, focus on `NGFYU.txt`

**Challenge Files**: NGFYU.txt

---

## 🔍 Solution Phases

### Phase 1: Initial File Analysis

#### Step 1: File Size and Content Check

```bash
cd /home/uttam/Downloads
cat NGFYU.txt | wc -l
# Output: 9168 lines
```

**Observation**: Extremely large file with 9168 lines - suspicious for a text file

#### Step 2: Examine File Contents

```bash
head -20 NGFYU.txt
tail -20 NGFYU.txt
```

**Key Finding**: File contains what appears to be "Never Gonna Give You Up" lyrics repeated in various orders

**Initial Impression**: 
- Looks like Rick Astley song lyrics
- Multiple repetitions in different sequences
- Could be a rickroll, but the reordering suggests encoding

---

### Phase 2: Pattern Recognition

#### Step 3: Pattern Search

```bash
grep -n "Never gonna give you up" NGFYU.txt | head -20
```

**Observation**: Lyrics are reordered in different sequences - suspicious pattern suggesting some form of encoding or steganography

#### Step 4: Testing Decoding Theories

Created multiple Python scripts to test different theories:

**Attempt 1**: Extract second phrases from each line
```python
# Hypothesis: Second phrase in each line might encode information
with open('NGFYU.txt', 'r') as f:
    for line in f:
        # Extract second phrase after first
        # Tried mapping phrases to binary patterns
```

**Result**: No meaningful output

**Attempt 2**: Map unique phrases to numbers/bits
```python
# Hypothesis: Each unique phrase represents a bit or number
phrases = [
    "Never gonna give you up",
    "Never gonna let you down",
    "Never gonna run around",
    # ... etc
]
# Created mapping of first phrases to bits (0-5)
# Attempted octal and binary decoding
```

**Result**: No clear pattern emerged

---

### Phase 3: Hidden Link Discovery

#### Step 5: Search for Anomalies

While analyzing the file, discovered lines that didn't match the pattern:

```bash
sed -n '509,511p' NGFYU.txt
```

**Critical Discovery**: Line 509 contained a base64 encoded string!

```bash
# Line 509: Checkout: aHR0cHM6Ly9uZXZlci1nb25uYS1may15b3UtdXAudmVyY2VsLmFwcC8=
```

#### Step 6: Decode Base64 String

```bash
echo "aHR0cHM6Ly9uZXZlci1nb25uYS1may15b3UtdXAudmVyY2VsLmFwcC8=" | base64 -d
# Output: https://never-gonna-fk-you-up.vercel.app/
```

**Breakthrough!** This is the key to understanding the file format.

---

### Phase 4: NGFYU Esoteric Language Discovery

#### Step 7: Visit the Discovered URL

Navigating to `https://never-gonna-fk-you-up.vercel.app/` revealed:

**NGFYU Language** (Never Gonna F*** You Up)
- Custom esoteric programming language
- Based on "Never Gonna Give You Up" lyrics
- Online interpreter available on the website
- Each lyric phrase is a programming instruction!

**Realization**: The entire NGFYU.txt file is a valid NGFYU program!

#### Step 8: Understanding NGFYU Syntax

The language uses Rick Astley lyrics as commands:
- `Never gonna give you up` - one instruction
- `Never gonna let you down` - another instruction
- `Never gonna run around` - yet another instruction
- etc.

The interpreter hosted at the URL can execute NGFYU code.

#### Step 9: Attempt to Run NGFYU Code

Created a Python script to send code to the NGFYU interpreter:

```python
import requests
import json

# Read the file
with open('/home/uttam/Downloads/NGFYU.txt', 'r') as f:
    lines = f.readlines()

# Remove empty lines
non_empty = [line.strip() for line in lines if line.strip()]

# Filter out special lines (509, 511, 1751 contain metadata, not code)
code_lines = []
for line in non_empty:
    if "Checkout" not in line and "aHR0c" not in line:
        code_lines.append(line.lower())

code = " ".join(code_lines)

# Send to NGFYU interpreter API
response = requests.post(
    "https://never-gonna-fk-you-up.vercel.app/api/run",
    headers={"Content-Type": "application/json"},
    json={"action": "run", "code": code, "input": ""}
)

print(response.text)
```

**Note**: Running the code may not directly give the flag, but it confirms the file is valid NGFYU code.

#### Step 10: Second Hidden Link Discovery

Continued searching for more base64 strings:

```bash
grep -n "aHR0c" NGFYU.txt
# Found another match at line 1751
```

```bash
# Extract line 1751
sed -n '1751p' NGFYU.txt

# Decode the base64
echo "aHR0cHM6Ly9kcml2ZS5nb29nbGUuY29tL2ZpbGUvZC8xVElyZGlpemFsRUdwTlU1YjRGUTlrMlhMUjRKc08xenAvdmlldz91c3A9c2hhcmluZw==" | base64 -d
# Output: https://drive.google.com/file/d/1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp/view?usp=sharing
```

**Major Discovery**: A Google Drive link to a file!

---

### Phase 5: Image Download and Steganography

#### Step 11: Download File from Google Drive

```bash
FILE_ID="1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp"
curl -L "https://drive.google.com/uc?export=download&id=${FILE_ID}" -o /tmp/flag_file

# Check file type
file /tmp/flag_file
# Output: PNG image data, 1920 x 1080, 8-bit/color RGBA, non-interlaced

# Copy to permanent location
cp /tmp/flag_file /home/uttam/Downloads/flag.png
ls -lh /home/uttam/Downloads/flag.png
# Output: 82K Oct 30 23:56 flag.png
```

**Result**: Downloaded a PNG image (82KB, 1920x1080 resolution)

#### Step 12: Initial Image Analysis

```bash
# Try basic steganography tools
strings flag.png | grep -i "eof"
exiftool flag.png | grep -i "flag\|eof"
```

**Result**: No obvious flags in metadata or strings

#### Step 13: Advanced Image Analysis - Brightness/Contrast Adjustment

**The Key Discovery**: The flag is hidden in the image but not visible with normal settings!

**Method 1: Using GIMP (GUI)**

1. Open `flag.png` in GIMP
2. Navigate to: **Colors → Brightness-Contrast**
3. Increase both brightness and contrast to maximum
4. **The flag becomes visible!**

**Steps**:
```
Colors > Brightness-Contrast
- Brightness: +100
- Contrast: +100
```

**Method 2: Using ImageMagick (Command Line)**

```bash
# Adjust brightness and contrast
convert flag.png -brightness-contrast 50x50 flag_adjusted.png

# Alternative: Use auto-level for automatic adjustment
convert flag.png -auto-level flag_adjusted.png

# View the adjusted image
xdg-open flag_adjusted.png
```

**Method 3: Using Photoshop**

1. Open `flag.png` in Photoshop
2. Navigate to: **Image → Adjustments → Brightness/Contrast**
3. Increase brightness: +100
4. Increase contrast: +100
5. Flag revealed!

#### Step 14: Flag Extraction

After adjusting brightness/contrast, the flag becomes clearly visible on the image:

```
EOF{@stley}
```

**Flag Breakdown**:
- `@stley` = "@stley" (Rick Astley reference!)
- The @ symbol represents "At" + "stley" = Astley
- A tribute to Rick Astley and the "Never Gonna Give You Up" theme

✅ **SUCCESS!** Flag: `EOF{@stley}`

---

## Technical Summary

| Metric                    | Value                                  | Details                                      |
|---------------------------|----------------------------------------|----------------------------------------------|
| Challenge Category        | Misc, Crypto, Steganography            | Multi-discipline challenge                   |
| Source File               | NGFYU.txt                              | 9168 lines of lyrics                         |
| File Size                 | ~450 KB                                | Unusually large text file                    |
| Esoteric Language         | NGFYU (Never Gonna F*** You Up)        | Rick Astley lyrics as programming language   |
| Interpreter URL           | never-gonna-fk-you-up.vercel.app       | Found via base64 on line 509                 |
| Hidden Link 1 (Line 509)  | NGFYU interpreter URL                  | Base64 encoded                               |
| Hidden Link 2 (Line 1751) | Google Drive link                      | Base64 encoded                               |
| Downloaded File           | flag.png (82 KB, 1920x1080)            | PNG image with hidden flag                   |
| Steganography Method      | Low brightness/contrast text           | Invisible without adjustment                 |
| Flag Reveal Technique     | Brightness/Contrast adjustment         | GIMP, Photoshop, or ImageMagick              |
| Flag                      | EOF{@stley}                            | ✅ Captured (Rick Astley reference)           |

---

## Tools Used

### File Analysis Tools:

- `wc` - Line count for file size analysis
- `head` / `tail` - File content examination
- `grep` - Pattern searching and base64 string discovery
- `sed` - Extract specific lines (509, 1751)
- `file` - File type identification

### Decoding Tools:

- `base64` - Decode hidden URLs
- `curl` - Download files from Google Drive
- Python `requests` - API calls to NGFYU interpreter

### Image Analysis Tools:

- `strings` - String extraction from binary files
- `exiftool` - EXIF metadata examination
- **GIMP** - **Critical**: Brightness/contrast adjustment
- **ImageMagick (`convert`)** - Command-line image manipulation
- **Photoshop** - Alternative GUI image editor

### Programming:

- Python - Custom scripts for NGFYU code testing
- Bash - Command-line automation

---

## Key Insights

### What is NGFYU Language?

**NGFYU** (Never Gonna F*** You Up) is a custom esoteric programming language:
- Uses phrases from "Never Gonna Give You Up" as programming instructions
- Each lyric line represents a command or operation
- The interpreter is hosted at: https://never-gonna-fk-you-up.vercel.app/
- The entire NGFYU.txt file is a valid NGFYU program
- Part of the "esolang" (esoteric language) family like Brainfuck, Whitespace, etc.

### Hidden Information Strategy

The challenge uses multiple layers of obfuscation:

1. **Line 509**: Base64 encoded URL to NGFYU interpreter
   - Hidden as "Checkout: [base64]"
   - Decodes to: https://never-gonna-fk-you-up.vercel.app/

2. **Line 1751**: Base64 encoded Google Drive link
   - Hidden among thousands of lyric lines
   - Decodes to: Google Drive link for flag.png

### Multi-Stage Challenge Breakdown

This challenge required solving **5 distinct stages**:

1. **File Analysis** - Recognize 9168 lines is suspicious
2. **Pattern Recognition** - Notice reordered lyrics suggest encoding
3. **Base64 Discovery** - Find hidden links on lines 509 and 1751
4. **Esoteric Language** - Understand NGFYU programming language
5. **Image Steganography** - Adjust brightness/contrast to reveal flag

### Why Brightness/Contrast Was Critical

The flag extraction technique:
- Flag text written in **very light gray** on **light background**
- Nearly invisible to the naked eye (low contrast)
- Requires brightness/contrast adjustment to see
- Common steganography technique: **hiding in plain sight with low visibility**
- Could also be revealed by:
  - Inverting colors
  - Adjusting levels/curves
  - Increasing saturation
  - Using different color channels

### Rick Astley Theme

The entire challenge is a elaborate rickroll:
- **NGFYU** = "Never Gonna F*** You Up" (play on song title)
- **9168 lines** of "Never Gonna Give You Up" lyrics
- **Flag**: `@stley` = Rick Astley
- **Theme**: Misdirection through humor (rickrolling)

---

## Files Created During Solution

```
Working Directory Structure:
/home/uttam/Downloads/
├── NGFYU.txt                    # Original challenge file (9168 lines)
├── test_decode.py               # Python script for phrase mapping
├── ngfyu_runner.py              # Python script for NGFYU interpreter API
├── /tmp/flag_file               # Downloaded file from Google Drive
├── flag.png                     # Original flag image (82K)
└── flag_adjusted.png            # Brightness/contrast adjusted image (reveals flag)
```

---

## Complete Command Sequence

```bash
# Phase 1: Initial Analysis
cd /home/uttam/Downloads
wc -l NGFYU.txt                  # Check file size
head -20 NGFYU.txt               # Examine start
tail -20 NGFYU.txt               # Examine end
grep -n "Never gonna" NGFYU.txt | head -20  # Pattern search

# Phase 2: Search for Anomalies
grep -n "Checkout" NGFYU.txt     # Find line 509
sed -n '509p' NGFYU.txt          # Extract line 509

# Phase 3: Decode First Base64
echo "aHR0cHM6Ly9uZXZlci1nb25uYS1may15b3UtdXAudmVyY2VsLmFwcC8=" | base64 -d
# Output: https://never-gonna-fk-you-up.vercel.app/

# Phase 4: Find Second Base64
grep -n "aHR0c" NGFYU.txt        # Find line 1751
sed -n '1751p' NGFYU.txt         # Extract line 1751

# Phase 5: Decode Second Base64
echo "aHR0cHM6Ly9kcml2ZS5nb29nbGUuY29tL2ZpbGUvZC8xVElyZGlpemFsRUdwTlU1YjRGUTlrMlhMUjRKc08xenAvdmlldz91c3A9c2hhcmluZw==" | base64 -d
# Output: https://drive.google.com/file/d/1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp/view?usp=sharing

# Phase 6: Download Flag Image
FILE_ID="1TIrdiizalEGpNU5b4FQ9k2XLR4JsO1zp"
curl -L "https://drive.google.com/uc?export=download&id=${FILE_ID}" -o flag.png

# Phase 7: Verify File
file flag.png                    # Confirm PNG image
ls -lh flag.png                  # Check size (82K)

# Phase 8: Try Basic Steganography
strings flag.png | grep -i "eof"
exiftool flag.png

# Phase 9: Adjust Brightness/Contrast (Command Line)
convert flag.png -brightness-contrast 50x50 flag_adjusted.png
# OR
convert flag.png -auto-level flag_adjusted.png

# Phase 10: View Adjusted Image
xdg-open flag_adjusted.png       # Flag revealed: EOF{@stley}
```

---

## Alternative Solution Methods

### Method 1: Python Script for Complete Automation

```python
import requests
import base64
import subprocess

# Step 1: Read NGFYU.txt
with open('NGFYU.txt', 'r') as f:
    content = f.read()
    lines = content.split('\n')

# Step 2: Find and decode base64 strings
base64_strings = []
for i, line in enumerate(lines, 1):
    if 'aHR0c' in line:
        # Extract base64 part
        b64 = line.split('aHR0c')[1].split()[0]
        b64 = 'aHR0c' + b64
        decoded = base64.b64decode(b64).decode()
        print(f"Line {i}: {decoded}")
        base64_strings.append((i, decoded))

# Step 3: Download from Google Drive
drive_link = base64_strings[1][1]  # Second link
file_id = drive_link.split('/d/')[1].split('/')[0]
download_url = f"https://drive.google.com/uc?export=download&id={file_id}"

response = requests.get(download_url)
with open('flag.png', 'wb') as f:
    f.write(response.content)

# Step 4: Adjust brightness/contrast
subprocess.run([
    'convert', 'flag.png',
    '-brightness-contrast', '50x50',
    'flag_revealed.png'
])

print("Flag image adjusted! Check flag_revealed.png")
```

### Method 2: Manual GUI Approach

1. **Open NGFYU.txt in text editor**
2. **Search for "Checkout" or "aHR0c"** (Ctrl+F)
3. **Copy base64 strings and decode**:
   - Use online base64 decoder: https://www.base64decode.org/
   - Or use: `echo "string" | base64 -d`
4. **Visit first URL**: Learn about NGFYU language
5. **Download from second URL**: Get flag.png from Google Drive
6. **Open in GIMP/Photoshop**: Adjust brightness/contrast
7. **Read flag**: `EOF{@stley}`

### Method 3: Using zsteg (Alternative)

```bash
# Sometimes zsteg can reveal hidden data
zsteg flag.png

# Try different bit planes
zsteg -a flag.png

# Extract LSB data
zsteg -E flag.png
```

**Note**: For this challenge, brightness/contrast adjustment is the intended solution, but exploring other steganography methods is good practice.

---

## Learning Outcomes

### Skills Demonstrated:

- **Esoteric programming languages** - Understanding non-mainstream languages
- **Base64 encoding/decoding** - Finding and decoding hidden data
- **File analysis** - Examining large text files for patterns
- **Pattern recognition** - Noticing anomalies in data
- **Image steganography** - Brightness/contrast manipulation
- **Multi-stage problem solving** - Connecting multiple clues
- **API interaction** - Testing online interpreters

### Key Techniques Learned:

1. **Hidden data in plain sight** - Base64 strings embedded in normal text
2. **Esoteric language recognition** - NGFYU as a custom language
3. **Google Drive downloads** - Using direct download links
4. **Image manipulation** - Brightness/contrast reveals hidden text
5. **Multi-layer challenges** - Solving 5 connected stages

---

## Common Pitfalls and How to Avoid Them

### ❌ Mistake 1: Trying to Decode Lyrics as Data
**Problem**: Assuming lyrics encode the flag directly
**Solution**: Look for anomalies (base64 strings) instead

### ❌ Mistake 2: Missing Hidden Base64 Strings
**Problem**: Not searching the entire 9168-line file
**Solution**: Use grep to find "Checkout" or "aHR0c" patterns

### ❌ Mistake 3: Not Adjusting Image Settings
**Problem**: Assuming flag.png is blank or needs complex steganography
**Solution**: Always try simple image adjustments first (brightness/contrast)

### ❌ Mistake 4: Using Wrong Steganography Tools
**Problem**: Trying `steghide`, `stegsolve`, etc. when not needed
**Solution**: Visual inspection + brightness adjustment was sufficient

### ❌ Mistake 5: Overthinking the NGFYU Code
**Problem**: Trying to execute/debug the NGFYU program
**Solution**: The code was a red herring; real flag was in the image

---

## Summary

**Random Gibberish** is a sophisticated multi-stage challenge that cleverly combines:

1. **Esoteric Programming Language** - NGFYU (Never Gonna F*** You Up)
2. **Base64 Steganography** - Hidden URLs on lines 509 and 1751
3. **Rick Astley Rickroll Theme** - 9168 lines of lyrics as misdirection
4. **Image Steganography** - Low-contrast text requiring brightness adjustment
5. **Multi-Stage Puzzle** - 5 distinct phases to solve

The flag `EOF{@stley}` is a tribute to Rick Astley, tying the entire rickroll theme together. The challenge teaches that not all obfuscation is cryptographic - sometimes the answer is hidden in plain sight with simple visual tricks.

**Critical Success Factors**:
- Finding anomalies in large datasets
- Recognizing base64 encoding patterns
- Understanding esoteric programming languages exist
- Trying simple image adjustments before complex steganography
- Connecting multiple clues across different mediums

The name "Random Gibberish" perfectly describes the initial appearance of 9168 lines of reordered lyrics - what seems like gibberish is actually a carefully crafted multi-layer puzzle! 🎵

---

✅ **Flag**: `EOF{@stley}` 🎯

**Reference**: "@stley" = Rick Astley (the NGFYU rickroll theme!)

Never gonna give you up, never gonna let you down! 🎵
