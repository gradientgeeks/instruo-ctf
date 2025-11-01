# Timeless Melodies - CTF Writeup

**Category:** Cryptography  
**Points:** 150 pts  
**Solves:** 12  

---

## 🧩 Challenge Description

> Blaise is excited to share his favourite classical composition with everyone. Join him and find the flag.

**Note:** *THIS IS NOT A NORMAL QUESTION.*  
The flag text which you will ultimately find here consists only of lowercase letters and does **not** contain `EOF{}`.  
If the raw flag you recover is `xyz`, submit it as `EOF{xyz}`.

We were given an audio file:

🔗 A zip file containing [Timeless Melodies (tune.wav)] and a.txt(the ciphertext) (https://drive.google.com/file/d/1O9BlF92hFVwtEs_D-CkOTLHqfaw5Hkob/view?usp=sharing)

---

## 🔍 Initial Thoughts

- The mention of **Blaise** immediately brings to mind **Blaise de Vigenère**, hinting that a **Vigenère cipher** might be involved.  
- The `.wav` file could contain the ciphertext, the key, or additional hints within its audio content or metadata.  
- The text `ybviemjrff` appeared in the challenge context — that’s a good candidate for the ciphertext.  

---

## 🧠 Approach

1. **Extract possible ciphertext or clues**  
   The string `ybviemjrff` appears to be our ciphertext. (or key maybe- which becomes clear as we proceed)
   The tune.wav was the famous "Für Elise" by Ludwig van Beethoven superimposed with a morse code( beeps). Extracted the morse code from the classic tune as beep.wav, used an online Morse code decoder to get the phrase
   ## "For wisdom names where fools mistrust."
   


3. **Analyze the hints**  
    What does wisdom do? It Names- Name of the classical piece was: Für Elise *(a clue maybe)* 
4. **Attempt Vigenère decryption**  
   Try decrypting `ybviemjrff` with candidate keys such as:
   wisdom, fools, blaise, classical, music, timeless, melody, piano, and ofcourse FurElise 
   The goal: find an all-lowercase meaningful word — that would be the raw flag (to be wrapped in `EOF{}`).
### Success with FurElise as a key used to decode the ciphertext in the .txt file (Vigenere Cipher).
---

## 💻 Tools Used

| Tool / Command | Purpose |
| --------------- | -------- |
| `strings tune.wav` | Check for embedded ASCII or hidden text |
| `exiftool tune.wav` | Inspect metadata for keywords |
| `sox` / `audacity` | Visualize frequency patterns and spectrogram |
| `python3` | For Vigenère decryption script |
| `https://morse-coder.com/decoders/decode-audio` | for Audio Morse Code decoder|

---
