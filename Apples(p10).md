# Apples - CTF Writeup

**Category:** OSINT
**Points:** 300 pts
---

## 🧩 Challenge Description

> An apple a day keeps a shinigami awake.

We were given a Python file named `light_and_ryuk.py`. The hint refers to *Death Note*, connecting to the theme of apples and shinigamis. The challenge required combining simple OSINT steps with light cryptography and file inspection.

---

## 🔍 Step-by-step Walkthrough

### 1) Running the Python Script

We started by running the given Python file:

```bash
python3 light_and_ryuk.py
```

This printed a YouTube video link in the terminal.

---

### 2) Inspecting the YouTube Video

Opening the YouTube link revealed something interesting in the **comments section** — there was a **Google Drive link**, but it appeared to be **encrypted** using a **Caesar cipher**.

---

### 3) Decrypting the Caesar Cipher

Instead of writing a script, we used an **online Caesar cipher decryption tool**. Trying different shifts revealed the decrypted Google Drive link that pointed to an image file named **`kira.png`**.

---

### 4) Downloading and Analyzing the Image

We downloaded the file from Google Drive. The image looked normal, but we suspected hidden data, so we used the `strings` command to search for the flag pattern:

```bash
strings kira.png | grep EOF
```

---

## 💡 Discovery

The output revealed the following:

```
EOF{apples_apples_everywhere_raaaah}
```

This was the hidden flag, embedded at the end of the PNG file.

---

## 📸 Evidence

Screenshot of the terminal output showing the discovered flag:

<img width="662" height="282" alt="image" src="https://github.com/user-attachments/assets/378a7992-03b8-43ab-ae4d-1d2bde47517d" />


---

## 🏁 Flag

```
EOF{apples_apples_everywhere_raaaah}
```

---

## 🧾 Summary

| Step | Action                   | Tool/Command                | Result                            |            |
| ---- | ------------------------ | --------------------------- | --------------------------------- | ---------- |
| 1    | Run the Python script    | `python3 light_and_ryuk.py` | Got YouTube link                  |            |
| 2    | Checked YouTube comments | Browser                     | Found Caesar-encrypted Drive link |            |
| 3    | Decrypted Drive link     | Online Caesar tool          | Got real Drive URL                |            |
| 4    | Downloaded image         | Google Drive                | Got `kira.png`                    |            |
| 5    | Extracted hidden text    | `strings kira.png           | grep EOF`                         | Found flag |

