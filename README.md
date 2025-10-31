# Instruo CTF Challenge 2025

Welcome to the **IIEST Instruo CTF Challenge 2025** repository! This repository contains detailed writeups and solutions for various Capture The Flag (CTF) challenges from the Instruo 2025 competition organized by IIEST (Indian Institute of Engineering Science and Technology).

## 📋 About

This repository serves as a comprehensive resource for understanding and solving the CTF challenges presented during Instruo 2025. Each challenge writeup includes step-by-step methodologies, tools used, and detailed explanations to help both beginners and experienced CTF players learn advanced techniques.

## 🎯 Challenge Categories

The challenges cover various categories of cybersecurity:
- **Steganography**: Hidden data extraction and analysis
- **Cryptography**: Encryption and decoding techniques
- **Miscellaneous**: Mixed-discipline challenges combining multiple skills

## 📚 Available Challenges

| Challenge Name | Category | Difficulty | Points | Teams Solved | Status |
|---------------|----------|------------|--------|--------------|--------|
| [Like Finding a Needle in the Hay Stack](#like-finding-a-needle-in-the-hay-stack) | Steganography | Hard | 500 | 0 | ✅ Solved |
| [Fooled](#fooled) | Steganography, Reverse Engineering | Hard | 600 | 1 | ✅ Solved |
| [Random Gibberish](#random-gibberish) | Misc, Crypto, Steganography | Medium | 200 | 8 | ✅ Solved |
| [Recursive Hell](#recursive-hell) | Steganography | Expert | - | - | ✅ Solved |

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

## 🚀 Getting Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/gradientgeeks/instruo-ctf.git
   cd instruo-ctf
   ```

2. **Choose a challenge**: Browse the markdown files to select a challenge.

3. **Read the writeup**: Each file contains a complete step-by-step solution.

4. **Practice**: Try to solve similar challenges using the techniques learned.

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

## 🤝 Contributing

Contributions are welcome! If you have:
- Additional solution methods
- Optimizations to existing solutions
- New challenge writeups
- Tool recommendations

Please feel free to open a pull request or issue.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🏆 Credits

**Event**: Instruo CTF 2025  
**Organizer**: IIEST (Indian Institute of Engineering Science and Technology)  
**Repository Maintainer**: Gradient Geeks

## 📧 Contact

For questions or discussions about these challenges:
- Open an issue in this repository
- Reach out to the Gradient Geeks team

---

**⚠️ Disclaimer**: These writeups are for educational purposes only. Always follow responsible disclosure practices and respect the rules of CTF competitions.

Happy hacking! 🎉
