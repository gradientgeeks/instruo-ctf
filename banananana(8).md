# Banananana - CTF Writeup

**Category:** Steganography
**Points:** 200 pts
**Solves:** 11

---

## 🧩 Challenge Description

> Obama loves banana. But the peels are scattered everywhere. Can you clean this mess and reveal what's lurking beneath all this?

We were given an audio file named `banananana.wav`. The description and title both hinted at something being hidden within the file — most likely a simple steganographic hint or embedded text.

---

## 🔍 Initial Thoughts

The word *banana* being repeated and the reference to *peels* suggested that the data might be hidden in the file’s metadata or text strings rather than deep frequency analysis. The challenge was in the **Steg** category, so the first step was to extract readable text.

---

## 🧠 Approach

I decided to use the `strings` command — a simple yet effective tool to extract printable characters from binary files:

```bash
strings banananana.wav | grep EOF
```

This command looks for any lines containing the keyword `EOF`, which is often used in CTF challenges to denote hidden messages or flag formats.

---

## 💡 Discovery

The output revealed the following lines:

```
EOF_BEC
;EOF{hidden_among_bananananananana}
```

Clearly, the flag was right there, hidden among the extracted text — just as the challenge hinted.

---

## 📸 Evidence

Here’s the terminal screenshot showing the discovery:

# Banananana - CTF Writeup

**Category:** Steganography
**Points:** 200 pts
**Solves:** 11

---

## 🧩 Challenge Description

> Obama loves banana. But the peels are scattered everywhere. Can you clean this mess and reveal what's lurking beneath all this?

We were given an audio file named `banananana.wav`. The description and title both hinted at something being hidden within the file — most likely a simple steganographic hint or embedded text.

---

## 🔍 Initial Thoughts
The challenge was in the **Steg** category, so the first step was to extract readable text.

---

## 🧠 Approach

I decided to use the `strings` command — a simple yet effective tool to extract printable characters from binary files:

```bash
strings banananana.wav | grep EOF
```

This command looks for any lines containing the keyword `EOF`, which is often used in CTF challenges to denote hidden messages or flag formats.

---

## 💡 Discovery

The output revealed the following lines:

```
EOF_BEC
;EOF{hidden_among_bananananananana}
```

Clearly, the flag was right there, hidden among the extracted text — just as the challenge hinted.

---

## 📸 Evidence

Here’s the terminal screenshot showing the discovery:
![WhatsApp Image 2025-10-30 at 19 03 11_45e4879a](https://github.com/user-attachments/assets/746a7a69-955c-4eec-9ff1-34d62232dcf7)


---


---

## 🏁 Flag

```
EOF{hidden_among_bananananananana}
```

---

## 🧾 Summary

| Step | Action                           | Result                |
| ---- | -------------------------------- | --------------------- |
| 1    | Analyzed the `.wav` file         | Contained hidden data |
| 2    | Used `strings` with `grep EOF`   | Found embedded text   |
| 3    | Extracted flag in `EOF{}` format | Success!              |
