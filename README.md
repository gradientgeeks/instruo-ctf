# Instruo CTF Challenge 2025 Solution

Welcome to our **IIEST Instruo CTF Challenge 2025 Solution** repository! This repository contains detailed writeups and solutions for various Capture The Flag (CTF) challenges from the Instruo 2025 competition organized by IIEST (Indian Institute of Engineering Science and Technology).

## 📋 About

This repository serves as a comprehensive resource for understanding and solving the CTF challenges presented during Instruo 2025. Each challenge writeup includes step-by-step methodologies, tools used, and detailed explanations to help both beginners and experienced CTF players learn advanced techniques.

## 🎯 Challenge Categories

The challenges cover various categories of cybersecurity:
- **Steganography**: Hidden data extraction and analysis
- **Reverse Engineering**: Binary analysis and code decompilation
- **Web**: Web application security and reconnaissance
- **Cryptography**: Encryption and decoding techniques
- **Miscellaneous**: Mixed-discipline challenges combining multiple skills

## 📚 Available Challenges

| Challenge Name | Category | Difficulty | Points | Teams Solved | Status |
|---------------|----------|------------|--------|--------------|--------|
| [Like Finding a Needle in the Hay Stack](#like-finding-a-needle-in-the-hay-stack) | Steganography | Hard | 500 | 0 | ✅ Solved |
| [Fooled](#fooled) | Steganography, Reverse Engineering | Hard | 600 | 1 | ✅ Solved |
| [Random Gibberish](#random-gibberish) | Misc, Crypto, Steganography | Medium | 200 | 8 | ✅ Solved |
| [Recursive Hell](#recursive-hell) | Steganography | Expert | - | - | ✅ Solved |
| [Amen](#amen) | Reverse Engineering | Medium | - | - | ✅ Solved |
| [Cannon Ball](#cannon-ball) | Web, Steganography | Medium | - | - | ✅ Solved |

## 🔍 Challenge Summaries

### Like Finding a Needle in the Hay Stack
**File**: [absolutely-normal.md](./absolutely-normal.md)  
**Flag**: `EOF{b3war3_!t$_c0m!ng_f0r_u}`

A multi-layered steganography challenge involving:
- PNG file analysis with embedded data
- MP3 extraction from images using binwalk
- Metadata analysis with exiftool
- Caesar cipher decryption
- Multiple fake flags as decoys

**Key Tools**: `binwalk`, `exiftool`, `dd`, `strings`, Python

---

### Fooled
**File**: [fooled.md](./fooled.md)  
**Flag**: `EOF{not_a_foolish_person_ig}`

A reverse engineering challenge featuring:
- ELF binary analysis with Ghidra
- Custom encryption algorithm
- Binary-to-decimal conversion
- Base64 decoding
- Hint-based cryptanalysis

**Key Tools**: Ghidra, Python, `file`, `strings`

---

### Random Gibberish
**File**: [random-gibberish.md](./random-gibberish.md)  
**Flag**: Found in extracted image

An esoteric programming language challenge involving:
- NGFYU (Never Gonna Give You Up) language recognition
- Hidden base64-encoded URLs
- Google Drive file extraction
- Multi-stage puzzle solving
- Image steganography

**Key Tools**: Base64 decoding, curl, NGFYU interpreter

---

### Recursive Hell
**File**: [recursive_hell.md](./recursive_hell.md)  
**Flag**: `EOF{its_a_damn_loop}`

An extreme recursion challenge featuring:
- 68 nested ZIP archives
- 48 layers of Base64 encoding
- Automated extraction scripting
- Binary data extraction from PNG
- 116 total iterations to reach the flag

**Key Tools**: `binwalk`, `dd`, `unzip`, `base64`, Bash scripting

---

### Amen
**File**: [amen.md](./amen.md)  
**Flag**: `EOF{wh3r3_ar3_my_po1n+5}`

A reverse engineering challenge featuring:
- 32-bit ELF binary analysis
- Pseudo-random number generator (PRNG) based flag generation
- Data array extraction from binary
- Understanding C's `rand()` and `srand()` functions
- Misleading hints as misdirection

**Key Tools**: Ghidra, Python, GCC, `strings`, `hexdump`

---

### Cannon Ball
**File**: [cannon-ball.md](./cannon-ball.md)  
**Flag**: `EOF{F0und_!t}`

A multi-stage web and steganography challenge featuring:
- Web reconnaissance and hidden resource discovery
- Base64-encoded data URIs
- Multiple website layers
- LSB steganography in PNG images
- Game interface as misdirection

**Key Tools**: `curl`, `zsteg`, `tesseract`, `base64`, `exiftool`

## 🛠️ Tools & Prerequisites

To solve these challenges, you'll need the following tools installed:

### Essential Tools
- **binwalk**: Firmware analysis and file extraction
- **exiftool**: Metadata analysis
- **strings**: Extract printable strings from binaries
- **file**: File type identification
- **hexdump**: Hexadecimal viewer

### Installation (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install binwalk exiftool file binutils unzip curl python3
```

### Optional Tools
- **Ghidra**: Reverse engineering framework
- **Python 3**: For scripting and automation
- **steghide/zsteg**: Additional steganography tools


## 📖 Learning Resources

### Steganography
- Understanding PNG/JPEG file structures
- Using binwalk for embedded file detection
- Metadata analysis techniques
- Audio steganography

### Reverse Engineering
- Binary analysis with Ghidra
- Understanding ELF executables
- Decompilation and disassembly

### Cryptography
- Caesar cipher and substitution ciphers
- Base64 encoding/decoding
- Custom encryption algorithms



## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**⚠️ Disclaimer**: These writeups are for educational purposes only. Always follow responsible disclosure practices and respect the rules of CTF competitions.

Happy hacking! 🎉
