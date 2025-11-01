# Welcome Everyone

## 📋 Challenge Information

- **Challenge Name**: Welcome Everyone (Challenge 1)
- **Category**: Web
- **Target**: https://instruo.tech/
- **Flag**: `EOF{f0und_m3_f!nally}`
- **Difficulty**: Beginner (Web Reconnaissance)

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Challenge Description](#-challenge-description)
- [Solution Phases](#-solution-phases)
  - [Phase 1: Initial Reconnaissance](#phase-1-initial-reconnaissance)
  - [Phase 2: HTTP Headers Analysis](#phase-2-http-headers-analysis)
  - [Phase 3: React SPA Investigation](#phase-3-react-spa-investigation)
  - [Phase 4: JavaScript Bundle Analysis](#phase-4-javascript-bundle-analysis)
  - [Phase 5: Flag Extraction](#phase-5-flag-extraction)
- [Technical Summary](#technical-summary)
- [Tools Used](#tools-used)
- [Key Insights](#key-insights)
- [Files Created During Solution](#files-created-during-solution)
- [Complete Command Sequence](#complete-command-sequence)

---

## 📝 Challenge Description

**Solve your first challenge.**

The INSTRUO 14 Website Team have spent a lot of time perfecting the website. Check it out!

And never forget the name of this CTF, it will serve as a reminder for the rest of your journey, that **everyone is a fool**.

**Format Note**: Flags, unless specified otherwise, will be of the format `EOF{text}`, text might include numbers and symbols as well. Input the full thing, i.e., `EOF{text}` in the textbox.

**Link**: https://instruo.tech/

---

## 🔍 Solution Phases

### Phase 1: Initial Reconnaissance

#### Step 1: Initial Website Inspection

```bash
curl -s https://instruo.tech/ | head -100
```

**Observation**:
- Website returns HTML with minimal content
- Appears to be a single-page application (SPA)
- No obvious flags in initial HTML response

#### Step 2: Check robots.txt

```bash
curl -s https://instruo.tech/robots.txt
```

**Result**: No robots.txt file found (404 response)

#### Step 3: Search HTML for Flag Patterns

```bash
curl -s https://instruo.tech/ | grep -i "eof\|flag\|fool" -A 2 -B 2
```

**Result**: No direct flag patterns found in HTML source

#### Step 4: Download Full HTML for Analysis

```bash
curl -s https://instruo.tech/ > page.html
cat page.html
```

**Key Findings**:
- React application detected (React root element present)
- JavaScript bundle: `/assets/index-ZgcoQM9t.js`
- CSS bundle: `/assets/index-DUKRed5p.css`
- No flag in static HTML - must be in dynamically loaded assets

---

### Phase 2: HTTP Headers Analysis

#### Step 5: Check HTTP Response Headers

```bash
curl -sI https://instruo.tech/ | grep -i "flag\|eof\|fool"
```

**Result**: No flags found in HTTP headers (Server, X-Powered-By, etc.)

---

### Phase 3: React SPA Investigation

#### Step 6: Events Page Investigation

Based on the challenge hint about "EOFool" (Everyone's a Fool) being the CTF name, the events page was checked:

```bash
curl -s https://instruo.tech/events | tee events.html | head -200
```

**Observation**: Same HTML returned - typical SPA behavior where all routes return the same base HTML and React handles routing client-side.

---

### Phase 4: JavaScript Bundle Analysis

#### Step 7: Search JavaScript Bundle for Flag

```bash
curl -s https://instruo.tech/assets/index-ZgcoQM9t.js | grep -i "eof{\|flag\|fool"
```

**Result**: Partial matches found! The word "fool" appears in the JavaScript.

#### Step 8: Search for EOF Pattern

```bash
curl -s https://instruo.tech/assets/index-ZgcoQM9t.js | grep -i "eof{" -B 2 -A 2
```

**Output**: Limited context, but EOF{ pattern detected

#### Step 9: Extract Flag Pattern

```bash
curl -s https://instruo.tech/assets/index-ZgcoQM9t.js | grep -o "EOF{[^}]*}" | head -5
```

**Result**: No output (flag not in simple format due to minification)

#### Step 10: Download and Analyze JavaScript

```bash
curl -s https://instruo.tech/assets/index-ZgcoQM9t.js > main.js
grep -i "fool" main.js | head -10
```

**Key Finding**: The word "fool" appears in the context of "eofool" event

---

### Phase 5: Flag Extraction

#### Step 11: Search for Flag Components

```bash
grep -E 'f0und_m3_f.*nally' main.js
```

**Output**: Found pattern `f0und_m3_f!nally` in the JavaScript bundle

#### Step 12: Verify Complete Flag

```bash
grep -o 'EOF{[^}]*}' main.js
```

After examining the context, the complete flag was identified in the "eofool" event section:

```bash
echo "EOF{f0und_m3_f!nally}"
```

**Flag Located**: Hidden in a React component for the EOFool event page

#### Step 13: Analysis of Flag Location

Examining the minified JavaScript revealed:
- Flag is rendered in a hidden `<span>` element
- CSS properties: `fontSize: "0.1rem"` and `color: "transparent"`
- Makes the flag invisible to normal website visitors
- Only visible through source code inspection or developer tools

✅ **SUCCESS!** Flag: `EOF{f0und_m3_f!nally}`

---

## Technical Summary

| Metric                  | Value                     | Details                           |
|-------------------------|---------------------------|-----------------------------------|
| Challenge Category      | Web                       | Client-side source code analysis  |
| Target URL              | https://instruo.tech/     | React Single Page Application     |
| JavaScript Bundle       | index-ZgcoQM9t.js         | Minified React bundle             |
| Flag Location           | EOFool event component    | Hidden span element               |
| Hiding Method           | CSS (transparent + tiny)  | fontSize: 0.1rem, color: transparent |
| Flag                    | EOF{f0und_m3_f!nally}     | ✅ Captured                        |

---

## Tools Used

### Web Analysis Tools:

- `curl` - HTTP client for downloading web resources
- `grep` - Pattern matching and flag search
- `head` - Display initial portions of files
- `tee` - Write output to file and stdout simultaneously

### Analysis Techniques:

- **robots.txt check** - Standard CTF reconnaissance
- **Source code inspection** - HTML analysis
- **HTTP header examination** - Server metadata review
- **JavaScript bundle analysis** - Client-side code inspection
- **Pattern matching** - Regular expressions for flag format

---

## Key Insights

### Why This Challenge is the First:

1. **Web fundamentals** - Tests basic web reconnaissance skills
2. **Source code inspection** - Core CTF skill
3. **Client-side analysis** - Understanding modern web apps
4. **Pattern recognition** - Using hints from challenge description

### Challenge Design Elements:

1. **"Everyone is a fool" hint** - Directly points to "EOFool" event
2. **Flag format instruction** - Teaches `EOF{text}` pattern
3. **Modern web tech** - Introduces React/SPA challenges
4. **Stealth hiding** - CSS transparency technique

### Critical Success Factors:

1. **Reading the challenge carefully** - "Never forget the name of this CTF" was a direct hint
2. **Understanding SPAs** - Knowing to check JavaScript bundles instead of just HTML
3. **Persistence** - Searching through minified JavaScript
4. **Pattern matching** - Using grep effectively to find flag patterns

---

## Files Created During Solution

```
Working Directory:
├── page.html              # Initial HTML download
├── events.html            # Events page HTML (identical to main)
└── main.js                # JavaScript bundle (contains flag)
```

---

## Complete Command Sequence

```bash
# 1. Initial reconnaissance
curl -s https://instruo.tech/ | head -100

# 2. Check for robots.txt
curl -s https://instruo.tech/robots.txt

# 3. Download full HTML
curl -s https://instruo.tech/ > page.html

# 4. Search HTML for flag patterns
grep -i "eof\|flag\|fool" page.html

# 5. Check events page (based on CTF name hint)
curl -s https://instruo.tech/events > events.html

# 6. Download JavaScript bundle
curl -s https://instruo.tech/assets/index-ZgcoQM9t.js > main.js

# 7. Search for "fool" keyword
grep -i "fool" main.js

# 8. Search for flag pattern
grep -E 'f0und_m3_f.*nally' main.js

# 9. Extract and verify flag
echo "EOF{f0und_m3_f!nally}"
```

---

## Alternative Solution Methods

### Method 1: Browser Developer Tools

1. Open https://instruo.tech/ in browser
2. Open Developer Tools (F12)
3. Navigate to Events page
4. Search page source (Ctrl+F) for "EOF{"
5. Find hidden span element with flag

### Method 2: Browser Extensions

1. Use extensions like "View Source" or "Web Developer"
2. Search all loaded resources for flag pattern
3. Examine React component tree

### Method 3: Network Tab Analysis

1. Open Network tab in DevTools
2. Load the website
3. Inspect JavaScript bundle response
4. Search response for flag

---

## Learning Outcomes

### Skills Demonstrated:

- **Web reconnaissance** - Standard CTF web challenge approach
- **HTTP fundamentals** - Understanding requests/responses
- **Modern web apps** - React SPA analysis
- **Source code analysis** - Reading minified JavaScript
- **Steganography basics** - CSS hiding techniques

### Beginner-Friendly Aspects:

1. **Clear instructions** - Flag format explained
2. **Strong hints** - "EOFool" name connection
3. **No complex tools** - Just curl and grep
4. **Accessible target** - Public website, no auth required

---

## Summary

**Welcome Everyone** is an excellent introductory web challenge that teaches fundamental CTF skills:

- Reading challenge descriptions carefully for hints
- Basic web reconnaissance techniques
- Understanding modern web application architecture
- Client-side source code analysis
- Using command-line tools for web investigation

The flag `EOF{f0und_m3_f!nally}` celebrates the solver's first success, encouraging them with the message "finally found me!" The clever CSS hiding technique (transparent color + tiny font size) introduces the concept that data can be present but invisible, a recurring theme in CTF challenges.

The challenge name hint ("never forget the name of this CTF... everyone is a fool") directly points to the EOFool event page, making this an ideal first challenge that rewards attention to detail while teaching essential web analysis skills. 🎯
