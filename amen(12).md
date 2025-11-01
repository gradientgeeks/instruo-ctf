# Amen

## 📋 Challenge Information

- **Challenge Name**: Amen (Binary: "a (3)")
- **Category**: Reverse Engineering
- **Points**: Unknown
- **File**: 32-bit ELF executable
- **Hint**: "strings lol.. zsteg the file bro"
- **Flag**: `EOF{wh3r3_ar3_my_po1n+5}`

## 📑 Table of Contents

- [Challenge Information](#-challenge-information)
- [Solution Methodology](#-solution-methodology)
  - [Step 1: Initial Binary Analysis](#step-1-initial-binary-analysis)
  - [Step 2: Disassembly and Function Discovery](#step-2-disassembly-and-function-discovery)
  - [Step 3: Understanding the Algorithm](#step-3-understanding-the-algorithm)
  - [Step 4: Extracting the Data Array](#step-4-extracting-the-data-array)
  - [Step 5: Replicating the Flag Generation](#step-5-replicating-the-flag-generation)
- [Key Insights](#key-insights)
- [Tools Used](#tools-used)
- [Complete Solution](#complete-solution)

---

## 🔍 Solution Methodology

### Step 1: Initial Binary Analysis

```bash
file "a (3)"
# Output: ELF 32-bit LSB executable, Intel 80386

strings "a (3)" | grep -i "flag\|eof"
# Found hint: "strings lol.. zsteg the file bro"
```

**Observation**: The binary is a 32-bit executable with a misleading hint about zsteg (which is for images).

### Step 2: Disassembly and Function Discovery

Using a disassembler (Ghidra/IDA), key functions identified:
- **`main()`**: Prompts for a number input
- **`recursive_fibonacci_mask()`**: Complex recursive function
- **`print_flag()`**: Generates and prints the flag
- **`dump()`**: Helper function (returns 0)

**Critical Flow**:
```c
if (input > 10) {
    seed = recursive_fibonacci_mask(input);
    print_flag(seed);
}
```

### Step 3: Understanding the Algorithm

#### The `print_flag()` Function

```c
void print_flag(unsigned int seed) {
    unsigned int data[24] = { /* hardcoded array */ };
    srand(seed);
    
    for (int i = 0; i < 24; i++) {
        int r = rand();
        char c = (r - data[i]) & 0xFF;
        printf("%c", c);
    }
}
```

**Key Discovery**: The seed value is hardcoded as `0xff10ca3b` in the binary's logic!

#### The Data Array Location

The data array is stored at virtual address **0x0804a0a0** in the binary:
- Contains 24 unsigned 32-bit integers (96 bytes total)
- Values are stored in little-endian format

### Step 4: Extracting the Data Array

```python
import struct

with open("a (3)", "rb") as f:
    content = f.read()

# Search for the data pattern
target = bytes.fromhex("80033018e240063f")
offset = content.find(target)
print(f"Found at offset: 0x{offset:x}")

# Extract 96 bytes (24 integers)
data = content[offset:offset+96]
values = [struct.unpack('<I', data[i:i+4])[0] for i in range(0, 96, 4)]

# Display as C array
print("unsigned int data[] = {")
for i in range(0, len(values), 4):
    line = ", ".join(f"0x{v:08x}" for v in values[i:i+4])
    print(f"    {line},")
print("};")
```

**Extracted Data Array**:
```c
unsigned int data[] = {
    0x18300380, 0x3f0640e2, 0x47c88dae, 0x4770cb65,
    0x70868fee, 0x5887f01e, 0x07b695b3, 0x7e5fe4f7,
    0x2b2bcab8, 0x7b1c25a5, 0x6cc1d210, 0x1029aafa,
    0x2b07785e, 0x45c80fee, 0x2d96388c, 0x0135865e,
    0x4eb1e13d, 0x5182204f, 0x21f78a34, 0x212d3340,
    0x40e64e84, 0x1c66c1b7, 0x6712a7ce, 0x4252dd56
};
```

### Step 5: Replicating the Flag Generation

```c
#include <stdio.h>
#include <stdlib.h>

unsigned int data[] = {
    0x18300380, 0x3f0640e2, 0x47c88dae, 0x4770cb65,
    0x70868fee, 0x5887f01e, 0x07b695b3, 0x7e5fe4f7,
    0x2b2bcab8, 0x7b1c25a5, 0x6cc1d210, 0x1029aafa,
    0x2b07785e, 0x45c80fee, 0x2d96388c, 0x0135865e,
    0x4eb1e13d, 0x5182204f, 0x21f78a34, 0x212d3340,
    0x40e64e84, 0x1c66c1b7, 0x6712a7ce, 0x4252dd56
};

int main() {
    unsigned int seed = 0xff10ca3b;
    printf("Flag: ");
    srand(seed);
    
    for (int i = 0; i < 24; i++) {
        int r = rand();
        unsigned int val = data[i];
        char c = (r - val) & 0xFF;
        printf("%c", c);
    }
    printf("\n");
    
    return 0;
}
```

**Compilation and Execution**:
```bash
gcc -o solve_final solve_final.c
./solve_final
```

**Output**: `EOF{wh3r3_ar3_my_po1n+5}`

---

## Key Insights

### Why This Challenge Was Clever

1. **Misleading Hint**: The "zsteg" hint was a red herring (zsteg is for image steganography)
2. **Hardcoded Seed**: The seed `0xff10ca3b` was embedded in the binary's logic
3. **PRNG-Based Encryption**: Used C's `rand()` function for pseudo-random character generation
4. **Data Extraction**: Required understanding of binary structure and memory layout

### Leetspeak Translation

**Flag**: `EOF{wh3r3_ar3_my_po1n+5}`  
**Meaning**: "where are my points?" - A humorous complaint about CTF scoring!

---

## Tools Used

- **Disassembler**: Ghidra or IDA Pro
- **Python**: For data extraction
- **GCC**: To compile the solution
- **hexdump/xxd**: For binary analysis
- **strings**: Initial reconnaissance

---

## Complete Solution

```bash
# 1. Disassemble binary to understand logic
# Use Ghidra/IDA to find print_flag() and data array location

# 2. Extract data array
python3 extract_data.py  # Extract 24 integers from offset

# 3. Compile and run solver
gcc -o solve solve.c
./solve

# Output: EOF{wh3r3_ar3_my_po1n+5}
```

This challenge demonstrates the importance of reverse engineering skills, understanding C standard library functions (`rand()`, `srand()`), and the ability to extract and analyze binary data structures!
