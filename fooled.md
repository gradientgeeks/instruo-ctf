
  ---
  Detailed Solution for "Fooled" CTF Challenge

  Challenge Information

  - Name: Fooled
  - Category: Steganography
  - Points: 600 pts
  - Teams Solved: 1
  - File: fooled.bin (31KB ELF 64-bit executable)
  - Hint: "The ASCII value of 'E' is author's favourite number" (E = 69)
  - Flag: EOF{not_a_foolish_person_ig}

  ---
  Solution Methodology

  Step 1: Binary Analysis

  file fooled.bin
  # ELF 64-bit LSB pie executable, x86-64

  Step 2: Reverse Engineering with Ghidra

  The binary contains several key functions:
  - printFlag() - Contains 32 encrypted bytes
  - check() - Validates three input parameters
  - binToDec() - Converts binary strings to decimal

  Step 3: Understanding the Validation Logic

  From disassembly, the check function requires:
  binToDec(arg1) + binToDec(arg2) + binToDec(arg3) = 218 (0xda)
  binToDec(arg3) = 70 (ASCII 'F')
  Therefore: binToDec(arg1) + binToDec(arg2) = 148

  Step 4: Encryption Algorithm Discovery

  The flag is encrypted using:
  sum_value = ((string[0] >> 1) << 1) + 1 + ((string[1] >> 1) << 1)

  # First 16 bytes: encrypted_byte = original_byte + sum_value
  # Last 16 bytes: encrypted_byte = original_byte - string[0]

  Step 5: Finding Correct Inputs

  Using the hint (ASCII 'E' = 69):
  - String input: "EOF" (E=69, O=79, F=70)
  - Verification: 69 + 79 + 70 = 218 ✓

  Binary inputs needed:
  - 10010011 → 147
  - 1 → 1
  - 1000110 → 70

  Step 6: Decryption Script

  encrypted_bytes = [
      0x1d, 0x28, 0xf4, 0xeb, 0x13, 0xed, 0x01, 0x21,
      0x15, 0x28, 0xf4, 0x31, 0x1d, 0xfc, 0xf8, 0xf8,
      0x82, 0x67, 0x5a, 0x98, 0x7b, 0x79, 0x6b, 0x9b,
      0x83, 0x53, 0x56, 0x87, 0x82, 0x78, 0x84, 0x5e
  ]

  def sum_func(s):
      c0, c1 = ord(s[0]), ord(s[1])
      return ((c0 // 2) * 2) + 1 + ((c1 // 2) * 2)

  s = "EOF"
  sum_val = sum_func(s)  # = 147

  # Decrypt first 16 bytes
  first_half = ''.join(chr((encrypted_bytes[i] - sum_val) & 0xff) for i in range(16))

  # Decrypt last 16 bytes  
  second_half = ''.join(chr((encrypted_bytes[i] + ord(s[0])) & 0xff) for i in range(16, 32))

  # Decode base64 parts
  flag = base64_decode(first_half) + base64_decode(second_half)

  Step 7: Running the Binary

  ./fooled.bin

  Step 8: Flag Extraction

  The decrypted bytes yield base64-encoded strings:
  - First part: "not_a_fool"
  - Second part: "ish_person_ig"

  Final Flag: EOF{not_a_foolish_person_ig}

  ---
  Key Techniques Used

  1. Reverse Engineering - Ghidra CLI for binary disassembly
  2. Binary Number Conversion - Understanding binToDec() function
  3. Cryptanalysis - Custom encryption algorithm with bitwise operations
  4. Hint Interpretation - ASCII value of 'E' (69) was the decryption key
  5. Base64 Decoding - Flag parts were base64-encoded

  Tools

  - Ghidra (CLI mode)
  - Python (for decryption scripting)
  - file, strings, hexdump, objdump
