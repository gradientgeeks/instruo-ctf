# Wrong Number - CTF Writeup

**Category:** Crypto, Misc  
**Points:** 150 pts  
**Solves:** 15

---

## 🧩 Challenge Description

*For the past couple of days, don't know who, but a random person calls me. Don't want to talk to him.*  
*Can you help me find him?*

We were provided with a zip file (`WrongNumber.zip`) containing two files that would help us identify the mysterious caller.

---

## 🔍 Initial Analysis

First, I extracted the main zip file to see what we're working with:

```bash
unzip -l WrongNumber.zip
```

**Contents:**
```
Archive: WrongNumber.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
      246  2025-10-21 18:39   take_it.zip
 35995736  2025-10-20 13:42   wrong_number.wav
---------                     -------
 35995982                     2 files
```

Two files were found:
- `wrong_number.wav` - An audio file (~36 MB)
- `take_it.zip` - A small encrypted zip file (246 bytes)

The challenge clearly involves:
1. Decoding information from the audio file
2. Using that information to unlock the second zip file

---

## 🎵 Step 1: Analyzing the Audio File

Upon listening to the song, the number **`2441139`** was embedded in the lyrics!

This was straightforward - no need for DTMF decoding, spectrograms, or complex audio analysis. The password was simply sung as part of the song lyrics.

This number appears to be the password for the encrypted zip file.

---

## 🔐 Step 2: Extracting the Encrypted Zip

Next, I attempted to extract `take_it.zip`:

```bash
unzip take_it.zip
```

**Output:**
```
Archive: take_it.zip
  skipping: finally.txt    unsupported compression method 99
```

### Understanding Compression Method 99

Compression method 99 indicates **AES encryption** in ZIP files. The standard `unzip` command doesn't support this, so I needed to use **7-Zip**.

### Using 7-Zip with the Password

```bash
7z x take_it.zip -p2441139
```

**Success!** The zip extracted a file called `finally.txt`.

---

## 📄 Step 3: Reading the Flag File

```bash
cat finally.txt
```

**Output:**
```
YIZ{4hd4h_x4_d1hx4v4x}
```

This doesn't match the expected `EOF{...}` format, indicating it's encrypted with a **substitution cipher**.

---

## 🔑 Step 4: Decrypting the Cipher

### Identifying the Cipher Type

Looking at the pattern:
- `YIZ{...}` should be `EOF{...}`
- This suggests: `Y → E`, `I → O`, `Z → F`

This is a **Caesar/ROT cipher** with a shift.

### Calculating the Shift

- Y (position 25) → E (position 5) = shift of **-20** (or +6)

### Decoding with ROT-20

Using an online ROT cipher decoder (or CyberChef) with a shift of **-20**:

**Input:** `YIZ{4hd4h_x4_d1hx4v4x}`  
**Output:** `EOF{4nd4n_w4_d1nw4v4w}`

---

## 🏁 Flag

```
EOF{4nd4n_w4_d1nw4v4w}
```

---

## 🧾 Summary

| Step | Action | Result |
|------|--------|--------|
| 1 | Extracted `WrongNumber.zip` | Found `wrong_number.wav` and `take_it.zip` |
| 2 | Decoded DTMF tones from audio | Got password: `2441139` |
| 3 | Extracted AES-encrypted zip with 7-Zip | Obtained `finally.txt` |
| 4 | Decrypted ROT-20 cipher | Retrieved final flag |

---
