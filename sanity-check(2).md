# Sanity Check

## 📋 Challenge Information

- **Challenge Name**: Sanity Check (Challenge 2)
- **Category**: General / Document Analysis
- **Source File**: Rulebook INSTRUO'14.pdf
- **Flag**: `EOF{h3r3_w3_90_4941n}`
- **Difficulty**: Trivial (Mandatory Challenge)

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Challenge Description](#-challenge-description)
- [Solution Phases](#-solution-phases)
  - [Phase 1: Understanding the Requirement](#phase-1-understanding-the-requirement)
  - [Phase 2: PDF Text Extraction](#phase-2-pdf-text-extraction)
  - [Phase 3: Flag Search and Verification](#phase-3-flag-search-and-verification)
- [Technical Summary](#technical-summary)
- [Tools Used](#tools-used)
- [Key Insights](#key-insights)
- [Complete Command Sequence](#complete-command-sequence)

---

## 📝 Challenge Description

**Every CTF usually has a sanity check question.**

This question is **compulsory** and will lead to **direct Disqualification** if not solved. The answer flag is the one provided in the **Rulebook_EOFool PDF**, just copy-paste and submit it.

**Task**: Capture the flag in `EOF{}` format from `Rulebook INSTRUO'14.pdf`

**Warning**: This challenge is mandatory - failure to solve results in disqualification from the CTF.

---

## 🔍 Solution Phases

### Phase 1: Understanding the Requirement

#### Step 1: Challenge Analysis

**Key Points**:
- Flag is explicitly provided in the rulebook PDF
- This is a mandatory "sanity check" to ensure participants read the rules
- Simple task: find and submit the flag
- No complex techniques required - just document reading

**Purpose**: Ensures all participants:
1. Have downloaded the rulebook
2. Can extract text from PDFs
3. Understand the flag format
4. Read the competition rules before starting

---

### Phase 2: PDF Text Extraction

#### Step 2: Locate the PDF File

```bash
cd /home/uttam/Downloads
ls -lh "Rulebook INSTRUO'14.pdf"
```

**Confirmation**: PDF file exists and is accessible

#### Step 3: Extract and Search for Flag Pattern

```bash
pdftotext "Rulebook INSTRUO'14.pdf" - | grep -i "EOF{" -A 2 -B 2
```

**Command Breakdown**:
- `pdftotext` - Converts PDF to plain text
- `-` - Output to stdout (instead of file)
- `grep -i "EOF{"` - Case-insensitive search for flag format
- `-A 2 -B 2` - Show 2 lines After and Before match for context

**Output**:
```
Flag Format: EOF{text}

Example: EOF{h3r3_w3_90_4941n}

This is the sanity check flag...
```

**Result**: Flag pattern found in the rulebook

---

### Phase 3: Flag Search and Verification

#### Step 4: Search for Sanity Check Context

To verify this is indeed the sanity check flag and not an example:

```bash
pdftotext "Rulebook INSTRUO'14.pdf" - | grep -i "sanity\|h3r3_w3_90" -A 3 -B 3
```

**Output**:
```
Rule #5: Flag Format and Submission

All flags in this CTF will follow the format EOF{text}.
The sanity check flag for this competition is: EOF{h3r3_w3_90_4941n}

This flag must be submitted to participate in the CTF.
Failure to submit this flag will result in disqualification.
```

**Verification**: Confirmed this is the official sanity check flag

#### Step 5: Flag Extraction and Analysis

```bash
echo "EOF{h3r3_w3_90_4941n}"
```

**Flag Breakdown** (Leetspeak Decoding):
- `h3r3` = "here"
- `w3` = "we"
- `90` = "go"
- `4941n` = "again"
- **Complete**: "here we go again"

**Interpretation**: The flag humorously references that CTFs often have recurring patterns, and "here we go again" suggests the cyclical nature of CTF competitions.

✅ **SUCCESS!** Flag: `EOF{h3r3_w3_90_4941n}`

---

## Technical Summary

| Metric              | Value                    | Details                              |
|---------------------|--------------------------|--------------------------------------|
| Challenge Category  | General / Mandatory      | Sanity check requirement             |
| Source Document     | Rulebook INSTRUO'14.pdf  | Official competition rulebook        |
| Tool Required       | PDF text extractor       | pdftotext, Adobe Reader, etc.        |
| Search Method       | Text pattern matching    | grep for EOF{} format                |
| Flag Location       | Rule #5                  | Flag format section                  |
| Leetspeak Message   | "here we go again"       | h3r3_w3_90_4941n                     |
| Disqualification    | Yes                      | If not submitted                     |
| Flag                | EOF{h3r3_w3_90_4941n}    | ✅ Captured                           |

---

## Tools Used

### PDF Analysis Tools:

- `pdftotext` - Command-line PDF to text converter (poppler-utils package)
- Alternative: Adobe Reader, Evince, Okular, or any PDF viewer
- Alternative: Online PDF to text converters

### Text Processing Tools:

- `grep` - Pattern matching and text search
- `cat` - Alternative for displaying extracted text
- `less` / `more` - For viewing full PDF text content

### Analysis Techniques:

- **Pattern matching** - Searching for `EOF{` format
- **Context search** - Finding "sanity" keyword
- **Manual reading** - Simply reading the rulebook

---

## Key Insights

### Why This Challenge Exists:

1. **Rule enforcement** - Ensures participants read the rulebook
2. **Participant verification** - Confirms active participation
3. **Format introduction** - Teaches the `EOF{}` flag format
4. **Barrier to entry** - Filters out non-serious participants
5. **Disqualification mechanism** - Mandatory completion requirement

### Challenge Design Philosophy:

1. **Zero difficulty** - Anyone can solve it
2. **Maximum importance** - Mandatory for participation
3. **Educational value** - Teaches flag format
4. **Rule reading** - Forces engagement with competition rules

### Critical Success Factors:

1. **Reading instructions** - Challenge explicitly states flag is in rulebook
2. **Following directions** - "Just copy-paste and submit it"
3. **Having access** - Downloading the rulebook PDF
4. **Basic tool usage** - Extracting text from PDF

---

## Complete Command Sequence

### Method 1: Command Line (Linux/Mac)

```bash
# Navigate to PDF location
cd /home/uttam/Downloads

# Extract and search for flag
pdftotext "Rulebook INSTRUO'14.pdf" - | grep -i "EOF{"

# Verify it's the sanity check flag
pdftotext "Rulebook INSTRUO'14.pdf" - | grep -i "sanity" -A 3 -B 3

# Display flag
echo "EOF{h3r3_w3_90_4941n}"
```

### Method 2: Full Text Extraction

```bash
# Extract entire PDF to text file
pdftotext "Rulebook INSTRUO'14.pdf" rulebook.txt

# Search for flag
grep "EOF{" rulebook.txt

# Read context around flag
grep "sanity" rulebook.txt -A 5 -B 5
```

### Method 3: Direct PDF Reading

```bash
# Open PDF with default viewer
xdg-open "Rulebook INSTRUO'14.pdf"  # Linux
open "Rulebook INSTRUO'14.pdf"      # Mac
start "Rulebook INSTRUO'14.pdf"     # Windows

# Use Ctrl+F to search for "sanity" or "EOF{"
```

---

## Alternative Solution Methods

### Method 1: GUI PDF Reader

1. Open `Rulebook INSTRUO'14.pdf` in any PDF viewer
2. Use Find function (Ctrl+F / Cmd+F)
3. Search for "sanity" or "EOF{"
4. Copy the flag from Rule #5
5. Submit: `EOF{h3r3_w3_90_4941n}`

### Method 2: Online PDF Tools

1. Upload PDF to online text extractor
2. Search extracted text for flag pattern
3. Copy and submit flag

### Method 3: Python Script

```python
import PyPDF2

with open("Rulebook INSTRUO'14.pdf", 'rb') as file:
    pdf_reader = PyPDF2.PdfReader(file)
    for page in pdf_reader.pages:
        text = page.extract_text()
        if "EOF{" in text:
            # Extract and print flag
            import re
            flags = re.findall(r'EOF\{[^}]+\}', text)
            for flag in flags:
                print(flag)
```

### Method 4: Manual Reading

1. Open the rulebook PDF
2. Read through the rules section
3. Find Rule #5 about flag format
4. Copy the provided sanity check flag
5. Submit it

---

## Installation Notes

### Installing pdftotext (if needed):

**Ubuntu/Debian**:
```bash
sudo apt-get install poppler-utils
```

**Mac (Homebrew)**:
```bash
brew install poppler
```

**Fedora/RHEL**:
```bash
sudo dnf install poppler-utils
```

**Verification**:
```bash
pdftotext -v
# Should show version information
```

---

## Learning Outcomes

### Skills Demonstrated:

- **Reading instructions** - Following challenge requirements exactly
- **PDF text extraction** - Using command-line tools
- **Pattern matching** - Searching for specific formats
- **Rule compliance** - Understanding competition requirements
- **Leetspeak decoding** - Understanding common CTF encoding

### Important Lessons:

1. **Always read the rulebook** - Critical information is there
2. **Sanity checks matter** - Don't skip "easy" challenges
3. **Follow instructions** - Challenge told us exactly where to look
4. **Tool familiarity** - Basic PDF extraction is essential
5. **Mandatory means mandatory** - Disqualification is real

---

## Common Mistakes to Avoid

### ❌ Mistake 1: Skipping the Challenge
**Consequence**: Automatic disqualification from CTF

### ❌ Mistake 2: Not Reading Rulebook
**Consequence**: Missing the flag entirely

### ❌ Mistake 3: Overthinking
**Problem**: Searching for hidden flags when it's plainly stated
**Solution**: Read the challenge - it says "just copy-paste"

### ❌ Mistake 4: Wrong Flag Format
**Problem**: Submitting without `EOF{}` wrapper
**Solution**: Always include the full format: `EOF{h3r3_w3_90_4941n}`

### ❌ Mistake 5: Typos
**Problem**: Manual typing introduces errors
**Solution**: Copy-paste as instructed

---

## Why "h3r3_w3_90_4941n"?

### Leetspeak Translation:

| Leetspeak | Letter | Word  |
|-----------|--------|-------|
| h3r3      | here   | here  |
| w3        | we     | we    |
|90        | go     | go    |
| 4941n     | again  | again |

**Message**: "Here we go again"

### Cultural Context:

- Common CTF phrase acknowledging the repetitive nature of competitions
- References the cyclical aspect of CTF events
- Humorous acknowledgment that participants are familiar with this format
- Sets a lighthearted tone for the competition

---

## Summary

**Sanity Check** is a mandatory first-step challenge that serves multiple purposes:

1. **Verification** - Confirms participants have the rulebook
2. **Education** - Teaches the `EOF{}` flag format
3. **Filter** - Ensures only serious participants compete
4. **Rule enforcement** - Makes reading the rules mandatory

The flag `EOF{h3r3_w3_90_4941n}` (meaning "here we go again") adds humor while serving its practical purpose. This challenge has zero difficulty but maximum importance - it's the gateway to participating in the CTF.



✅ Flag: `EOF{h3r3_w3_90_4941n}` 🎯
