# Hiding in Plain Sight - CTF Writeup

**Category:** Steganography
**Points:** 150 pts
**Solves:** 11

---

## 🧩 Challenge Description

> Got this PDF from a crazy guy, wonder what he wants to tell me?
> **Hint:** Not all is what it seems.

We were given a seemingly normal PDF file. The hint suggests that something might be hidden inside the file in plain sight, probably using simple steganographic or textual tricks.

---

## 🔍 Initial Analysis

First, I tried opening the PDF normally — it showed nothing meaningful or just blank content. This hinted that the real information might not be visible through a regular PDF viewer.

To investigate further, I listed the file details:

```bash
ls -l
```

It confirmed that the file had a reasonable size, suggesting hidden text or embedded data.

---

## 🧠 Approach

Given the hint and the category (Steg), I decided to **inspect the raw content** of the file instead of viewing it normally.

In Kali Linux, this can be done simply by using the `cat` command:

```bash
cat Nothing_hidden_inside.pdf
```

However, since PDF files can be quite verbose, I filtered for the end section (where PDF metadata or extra text might be hidden):

```bash
cat Nothing_hidden_inside.pdf | grep EOF
```

---

## 💡 Discovery

The command output revealed a series of characters just before the `%%EOF` marker:

```
{u_r_@_ch!ck3n}%
```

Following the given flag format (`EOF{}`), the flag becomes:

```
EOF{u_r_@_ch!ck3n}
```

---

## 📸 Evidence

Below is the screenshot showing the command and the discovered text:
<img width="803" height="333" alt="image" src="https://github.com/user-attachments/assets/47766835-adea-4261-8520-48ca380566c5" />


---

## 🏁 Flag

```
EOF{u_r_@_ch!ck3n}
```

---

## 🧾 Summary

| Step | Action                           | Result               |
| ---- | -------------------------------- | -------------------- |
| 1    | Opened PDF normally              | Nothing visible      |
| 2    | Used `cat` and `grep EOF`        | Revealed hidden text |
| 3    | Extracted flag in `EOF{}` format | Success!             |


