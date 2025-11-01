# Instruo CTF 2025 - Solved Solutions & Writeups

<div align="center">

![Instruo CTF](https://img.shields.io/badge/CTF-Instruo%202025-blue?style=for-the-badge)
![Challenges Solved](https://img.shields.io/badge/Challenges%20Solved-14-brightgreen?style=for-the-badge)
![Categories](https://img.shields.io/badge/Categories-7-orange?style=for-the-badge)

**Comprehensive writeups and solutions for the Instruo 2025 CTF Competition**

[🌐 View Website](https://gradientgeeks.github.io/instruo-ctf/) • [📚 Challenges](#-challenges) • [🛠️ Tools](#-tools--prerequisites)

</div>

---

## 📋 About

Welcome to the **IIEST Instruo CTF 2025 Solutions** repository! This comprehensive collection contains detailed writeups, methodologies, and solutions for all challenges from the Instruo 2025 Capture The Flag competition organized by IIEST (Indian Institute of Engineering Science and Technology).

Each writeup includes:
- ✅ Step-by-step solution methodology
- 🔧 Tools and techniques used
- 💡 Key insights and learning points
- 📝 Complete command sequences
- 🎯 Alternative solution methods

Perfect for both beginners learning CTF techniques and experienced players looking for advanced problem-solving approaches.

---

## 🎯 Challenge Categories

The challenges span **7 major cybersecurity domains**:

| Category | Description | Challenges |
|----------|-------------|------------|
| 🔍 **Steganography** | Hidden data extraction, file analysis, metadata forensics | 5 |
| 🔧 **Reverse Engineering** | Binary analysis, decompilation, algorithm reconstruction | 2 |
| 🌐 **Web** | Web recon, hidden resources, client-side analysis | 2 |
| 🔐 **Cryptography** | Ciphers, encoding, cryptanalysis | 2 |
| 🕵️ **OSINT** | Open-source intelligence, profile tracking | 2 |
| 📋 **General** | Mandatory challenges, documentation | 1 |

---

## 📚 Challenges

### 🟢 Easy Challenges (150 pts each)

| # | Challenge Name | Category | Flag | Writeup | HTML |
|---|----------------|----------|------|---------|------|
| 1 | **Welcome Everyone** | Web | `EOF{f0und_m3_f!nally}` | [📖 MD](weclome-everyone(1).md) | [🌐 HTML](src/welcome-everyone.html) |
| 2 | **Sanity Check** ⚠️ | General (Mandatory) | `EOF{h3r3_w3_90_4941n}` | [📖 MD](sanity-check(2).md) | [🌐 HTML](src/sanity-check.html) |
| 3 | **Hiding in Plain Sight** | Steganography | `EOF{u_r_@_ch!ck3n}` | [📖 MD](nothing-hidden-inside(3).md) | [🌐 HTML](src/nothing-hidden-inside.html) |
| 4 | **Wrong Number** | Crypto, Misc | `EOF{4nd4n_w4_d1nw4v4w}` | [📖 MD](wrong-number(p4).md) | [🌐 HTML](src/wrong-number.html) |
| 5 | **A Noob's First Milestone** | OSINT | `EOF{script_kiddie@eofool.com}` | [📖 MD](gitlab-repo(5).md) | [🌐 HTML](src/gitlab-repo.html) |
| 6 | **Timeless Melodies** | Cryptography | `EOF{decrypted_text}` | [📖 MD](timeless-melodies(6).md) | [🌐 HTML](src/timeless-melodies.html) |

### 🟡 Medium Challenges (200 pts)

| # | Challenge Name | Category | Flag | Writeup | HTML |
|---|----------------|----------|------|---------|------|
| 7 | **Random Gibberish** | Misc, Crypto, Steg | `EOF{@stley}` | [📖 MD](random-gibberish(7).md) | [🌐 HTML](src/random-gibberish.html) |
| 8 | **Banananana** | Steganography | `EOF{hidden_among_bananananananana}` | [📖 MD](banananana(8).md) | [🌐 HTML](src/banananana.html) |
| 11 | **Cannon Ball** | Web, Steganography | `EOF{F0und_!t}` | [📖 MD](cannon-ball(11).md) | [🌐 HTML](src/cannon-ball.html) |
| 12 | **Amen** | Reverse Engineering | `EOF{wh3r3_ar3_my_po1n+5}` | [📖 MD](amen(12).md) | [🌐 HTML](src/amen.html) |

### 🔴 Hard & Expert Challenges (300-600 pts)

| # | Challenge Name | Category | Difficulty | Flag | Writeup | HTML |
|---|----------------|----------|------------|------|---------|------|
| 9 | **Recursive Hell** | Steganography | Expert | `EOF{its_a_damn_loop}` | [📖 MD](recursive-hell(9).md) | [🌐 HTML](src/recursive_hell.html) |
| 10 | **Apples** | OSINT | Hard (300 pts) | `EOF{apples_apples_everywhere_raaaah}` | [📖 MD](apples(10).md) | [🌐 HTML](src/apples.html) |
| 15 | **Like Finding a Needle in the Hay Stack** | Steganography | Hard (500 pts) | `EOF{b3war3_!t$_c0m!ng_f0r_u}` | [📖 MD](absolutely-normal(15).md) | [🌐 HTML](src/absolutely-normal.html) |
| 16 | **Fooled** | Reverse Engineering | Hard (600 pts) | `EOF{not_a_foolish_person_ig}` | [📖 MD](fooled(16).md) | [🌐 HTML](src/fooled.html) |

---

## 🔥 Featured Challenges

### 🎯 Welcome Everyone (Challenge 1)
**Category**: Web | **Difficulty**: Easy | **Points**: 150

Your first CTF challenge! Find the flag hidden in the Instruo website's JavaScript bundle.

**Key Techniques**:
- Web source code inspection
- JavaScript bundle analysis
- React SPA reconnaissance

**Flag**: `EOF{f0und_m3_f!nally}`

[📖 Full Writeup](weclome-everyone(1).md) | [🌐 HTML Version](src/absolutely-normal.html)

---

### 🔁 Recursive Hell (Challenge 9)
**Category**: Steganography | **Difficulty**: Expert

The ultimate recursion nightmare! Navigate through **68 nested ZIP files** and **48 layers of Base64 encoding** (116 total iterations!) to find the flag.

**Key Techniques**:
- Binwalk for embedded file detection
- Automated bash scripting for recursion
- Base64 multi-layer decoding
- Pattern recognition

**Flag**: `EOF{its_a_damn_loop}`

[📖 Full Writeup](recursive-hell(9).md) | [🌐 HTML Version](src/recursive_hell.html)

---

### 🎭 Random Gibberish (Challenge 7)
**Category**: Misc, Crypto, Steganography | **Difficulty**: Medium | **Points**: 200

An elaborate rickroll-themed challenge involving the esoteric NGFYU programming language!

**Key Techniques**:
- NGFYU (Never Gonna Give You Up) language recognition
- Base64-encoded URL extraction (lines 509 & 1751)
- Google Drive file downloads
- Brightness/contrast image manipulation

**Flag**: `EOF{@stley}` (Rick Astley reference!)

[📖 Full Writeup](random-gibberish(7).md) | [🌐 HTML Version](src/random-gibberish.html)

---

### 🪡 Like Finding a Needle in the Hay Stack (Challenge 15)
**Category**: Steganography | **Difficulty**: Hard | **Points**: 500 | **Solves**: 0 ⭐

The hardest steganography challenge with multiple fake flags!

**Key Techniques**:
- PNG structure analysis (data after IEND marker)
- MP3 extraction with binwalk
- Metadata analysis with exiftool (critical: "Needle" field)
- Caesar cipher (+1 shift) with noise obfuscation

**Real Flag**: `EOF{b3war3_!t$_c0m!ng_f0r_u}` (Beware, it's coming for you)

**Fake Flags**: 
- ❌ `EOF{this_is_not_a_real_flag}`
- ❌ `EOF{F00l'$_3rr@nd}` (Fool's Errand)

[📖 Full Writeup](absolutely-normal(15).md) | [🌐 HTML Version](src/absolutely-normal.html)

---

### 👨‍💻 Fooled (Challenge 16)
**Category**: Reverse Engineering | **Difficulty**: Hard | **Points**: 600 | **Solves**: 1 ⭐

The hardest reverse engineering challenge requiring deep binary analysis!

**Key Techniques**:
- ELF binary decompilation with Ghidra
- Custom encryption algorithm reverse engineering
- Binary-to-decimal conversion logic
- ASCII hint interpretation (E=69)
- Base64 decoding of flag parts

**Flag**: `EOF{not_a_foolish_person_ig}`

[📖 Full Writeup](fooled(16).md) | [🌐 HTML Version](src/fooled.html)

---

## 🛠️ Tools & Prerequisites

### 📦 Essential Tools

#### Steganography & Forensics
```bash
sudo apt install binwalk exiftool steghide zsteg
```
- **binwalk** - Detect and extract embedded files
- **exiftool** - Metadata analysis for images/audio
- **steghide** - Hide/extract data in images
- **zsteg** - PNG/BMP LSB steganography detection

#### Reverse Engineering
```bash
# Ghidra (Download from NSA official site)
# https://ghidra-sre.org/

sudo apt install gdb radare2 objdump ltrace strace
```
- **Ghidra** - GUI decompiler and disassembler
- **GDB** - GNU debugger
- **radare2** - Command-line reverse engineering framework

#### Cryptography
```bash
sudo apt install hashcat john openssl
pip install pycryptodome
```
- **CyberChef** - Web-based crypto Swiss Army knife
- **hashcat** - Password cracking
- **john** - John the Ripper password cracker

#### Web & Network
```bash
sudo apt install curl wget nmap nikto sqlmap
```
- **curl/wget** - HTTP clients
- **Browser DevTools** - JavaScript debugging
- **Burp Suite** - Web proxy and security testing

#### General Utilities
```bash
sudo apt install file strings hexdump xxd dd unzip 7zip
```
- **file** - File type identification
- **strings** - Extract printable strings
- **hexdump/xxd** - Hex viewers
- **dd** - Binary data extraction

### 🐍 Python Libraries
```bash
pip install requests pillow pycryptodome
```

### 📚 Installation Script

```bash
#!/bin/bash
# Install all CTF tools at once

sudo apt update
sudo apt install -y binwalk exiftool steghide file strings hexdump \
    xxd dd unzip p7zip-full curl wget python3 python3-pip \
    gdb radare2 hashcat openssl nmap

pip3 install requests pillow pycryptodome base64
```

---

## 📖 Learning Resources

### 🎓 Steganography
- [File structure analysis (PNG, JPEG, MP3)](https://en.wikipedia.org/wiki/Portable_Network_Graphics)
- [Binwalk tutorial](https://github.com/ReFirmLabs/binwalk/wiki)
- [Audio steganography techniques](https://www.youtube.com/watch?v=TWEXCYQKyDc)
- [LSB (Least Significant Bit) steganography](https://github.com/RobinDavid/LSB-Steganography)

### 🔧 Reverse Engineering
- [Ghidra basics](https://ghidra-sre.org/CheatSheet.html)
- [Understanding ELF binaries](https://refspecs.linuxbase.org/elf/elf.pdf)
- [Crackmes.one - Practice platform](https://crackmes.one/)

### 🔐 Cryptography
- [Classical ciphers](https://www.dcode.fr/en)
- [CyberChef recipes](https://gchq.github.io/CyberChef/)
- [Crypto challenges on CryptoPals](https://cryptopals.com/)

### 🌐 Web Security
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)

---

## 📈 Statistics

| Metric | Value |
|--------|-------|
| **Total Challenges** | 14 |
| **Categories Covered** | 7 |
| **Total Points** | 3,900+ |
| **Tools Used** | 25+ |
| **Lines of Writeups** | 5,000+ |
| **HTML Pages** | 14 |

---

## 🏅 Difficulty Breakdown

```
Easy     (150 pts): ████████ 8 challenges
Medium   (200 pts): ████ 4 challenges
Hard  (300-600 pts): ██ 2 challenges
Expert:              █ 1 challenge (Recursive Hell)
```

---

## 🌐 Website

Visit our interactive website to explore all challenges with beautiful UI:

**🔗 [https://gradientgeeks.github.io/instruo-ctf/](https://gradientgeeks.github.io/instruo-ctf/)**

Features:
- 🎨 Beautiful glassmorphism UI
- 📱 Fully responsive design
- 🔍 Syntax-highlighted code blocks
- 📊 Challenge statistics
- 🏷️ Category badges
- 💾 Downloadable writeups

---

## 🤝 Contributing

Found an alternative solution? Want to add a challenge? Contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-challenge`)
3. Commit your changes (`git commit -m 'Add new challenge writeup'`)
4. Push to the branch (`git push origin feature/new-challenge`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⚠️ Disclaimer

These writeups are for **educational purposes only**. 

- Always follow responsible disclosure practices
- Respect CTF rules and intellectual property
- Do not use these techniques for unauthorized access
- CTF skills should be used ethically and legally

---

## 🙏 Acknowledgments

- **IIEST (Indian Institute of Engineering Science and Technology)** - For organizing Instruo 2025
- **CTF Challenge Creators** - For designing engaging and educational challenges
- **Gradient Geeks** - For maintaining this repository
- **Open Source Community** - For providing amazing tools like Ghidra, binwalk, and more

---

## 📞 Contact

- **GitHub**: [@gradientgeeks](https://github.com/gradientgeeks)
- **Website**: [https://gradientgeeks.github.io/instruo-ctf/](https://gradientgeeks.github.io/instruo-ctf/)

---

<div align="center">

**Made with ❤️ by Gradient Geeks**

⭐ Star this repo if you found it helpful!

[🔝 Back to Top](#-instruo-ctf-2025---complete-solutions--writeups)

</div>
