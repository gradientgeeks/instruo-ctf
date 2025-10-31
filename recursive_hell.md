
  Challenge Information

  - Challenge Name: recursive_hell.png
  - Category: Steganography
  - Initial File: recursive_hell.png (17 MB PNG image)
  - Flag: EOF{its_a_damn_loop}
  - Difficulty: High (68 nested ZIPs + 48 Base64 layers)

  ---
  PHASE 1: Initial Reconnaissance

  Step 1: File Analysis

  file /home/uttam/Downloads/recursive_hell.png
  # Output: PNG image data, 680 x 512, 16-bit/color RGB, non-interlaced
  # Observation: File size 17 MB - suspiciously large for a simple PNG

  Step 2: EXIF Metadata Examination

  exiftool /home/uttam/Downloads/recursive_hell.png
  Key Finding:
  - Warning: "Text/EXIF chunk(s) found after PNG IDAT"
  - This indicated additional data appended after the image data

  Step 3: Initial String Search

  strings /home/uttam/Downloads/recursive_hell.png | grep -E "EOF\{.*\}"
  Result: No readable flag found (flag was deeply embedded)

  ---
  PHASE 2: Embedded Data Detection

  Step 4: Binwalk Analysis (Critical Discovery)

  binwalk /home/uttam/Downloads/recursive_hell.png

  Output:
  DECIMAL       HEXADECIMAL     DESCRIPTION
  --------------------------------------------------------------------------------
  0             0x0             PNG image, 680 x 512, 16-bit/color RGB
  296306        0x48572         Zip archive data

  Key Discovery: ZIP archive embedded at byte offset 296306 (0x48572)

  Step 5: Extract Embedded ZIP

  dd if=recursive_hell.png of=extracted.zip bs=1 skip=296306
  Parameters:
  - if = input file (PNG)
  - of = output file (ZIP)
  - bs=1 = block size 1 byte (for precise extraction)
  - skip=296306 = skip PNG data, start at ZIP offset

  ---
  PHASE 3: Recursive ZIP Extraction (68 Levels)

  Step 6: First ZIP Extraction

  unzip -q extracted.zip
  ls -lh
  Result: Extracted file named temp_68.txt

  Step 7: Identify Nested ZIP Pattern

  file temp_68.txt
  # Output: Zip archive data, at least v2.0 to extract
  Realization: The .txt file is actually another ZIP! This is a recursive nesting challenge.

  Step 8: Automated Recursive Extraction Script

  Created: extract_recursive.sh

  #!/bin/bash
  # Script to extract 68 nested ZIP files

  for i in {67..1}; do
    if [ -f "temp_$i.txt" ]; then
      file_type=$(file temp_$i.txt)

      if echo "$file_type" | grep -q "Zip archive"; then
        echo "Extracting temp_$i.txt..."
        mv temp_$i.txt temp_$i.zip
        unzip -q temp_$i.zip
      else
        echo "Found non-ZIP file: temp_$i.txt"
        file temp_$i.txt
        break
      fi
    fi
  done

  echo "Extraction complete. Final file:"
  ls -lh temp_0.txt

  Step 9: Execute Extraction

  chmod +x extract_recursive.sh
  ./extract_recursive.sh

  Output:
  Extracting temp_67.txt...
  Extracting temp_66.txt...
  Extracting temp_65.txt...
  ... (continues through all 68 levels) ...
  Extracting temp_1.txt...
  Extraction complete. Final file:
  -rw-r--r-- 1 uttam uttam 1.2K Oct 30 19:45 temp_0.txt

  Result: Successfully extracted 68 nested ZIP archives, reaching temp_0.txt

  ---
  PHASE 4: Base64 Decoding (48 Iterations)

  Step 10: Initial Base64 Detection

  head temp_0.txt
  Observation: File contains Base64-encoded data (alphanumeric + / + =)

  base64 -d temp_0.txt > decoded_1.txt
  head decoded_1.txt
  Result: Still Base64! Multiple layers of encoding detected.

  Step 11: Recursive Base64 Decoder Script

  Created: recursive_decode.sh

  #!/bin/bash
  # Script to decode multiple layers of Base64 encoding

  input="temp_0.txt"
  counter=0

  while true; do
    output="decoded_$counter.txt"

    # Attempt Base64 decoding
    base64 -d "$input" > "$output" 2>/dev/null

    if [ $? -ne 0 ]; then
      echo "Decoding failed at iteration $counter"
      break
    fi

    # Check if output is different from input
    if cmp -s "$input" "$output"; then
      echo "No change at iteration $counter"
      break
    fi

    # Check if output is still Base64
    if head -c 100 "$output" | grep -qE '^[A-Za-z0-9+/=]+$'; then
      echo "Iteration $counter: Still Base64"
      input="$output"
      counter=$((counter + 1))
    else
      echo "Iteration $counter: Not Base64 anymore!"
      file "$output"
      echo "Searching for flag..."
      grep -o "EOF{[^}]*}" "$output"
      break
    fi
  done

  Step 12: Execute Recursive Decoder

  chmod +x recursive_decode.sh
  ./recursive_decode.sh

  Output:
  Iteration 0: Still Base64
  Iteration 1: Still Base64
  Iteration 2: Still Base64
  Iteration 3: Still Base64
  ...
  Iteration 46: Still Base64
  Iteration 47: Still Base64
  Iteration 48: Not Base64 anymore!
  decoded_48.txt: ASCII text, with no line terminators
  Searching for flag...
  EOF{its_a_damn_loop}

  Step 13: Flag Verification

  cat decoded_48.txt
  Output: EOF{its_a_damn_loop}

  SUCCESS! Flag captured after 68 ZIP extractions + 48 Base64 decodings = 116 total iterations!

  ---
  TECHNICAL SUMMARY

  | Metric                 | Value                | Details                  |
  |------------------------|----------------------|--------------------------|
  | Initial File Size      | 17 MB                | Unusually large PNG      |
  | ZIP Archive Offset     | 296306 bytes         | Found via binwalk        |
  | Nested ZIP Levels      | 68                   | temp_68.txt → temp_0.txt |
  | Base64 Encoding Layers | 48                   | Decoded iteratively      |
  | Total Iterations       | 116                  | 68 + 48                  |
  | Final Flag Location    | decoded_48.txt       | ASCII text file          |
  | Flag                   | EOF{its_a_damn_loop} | ✅ Captured               |

  ---
  TOOLS USED

  Analysis Tools:

  - file - File type identification
  - exiftool - EXIF metadata examination
  - binwalk - Critical: Detected embedded ZIP
  - strings - String extraction attempts

  Extraction Tools:

  - dd - Binary data extraction at specific offset
  - unzip - ZIP archive extraction
  - base64 - Base64 decoding

  Automation:

  - bash - Shell scripting for automation
  - grep - Pattern matching for Base64 and flag
  - cmp - File comparison

  ---
  KEY INSIGHTS

  Why This Challenge is Called "recursive_hell":

  1. 68 nested ZIPs - Each ZIP contains another ZIP (classic recursion)
  2. 48 Base64 layers - Each decode reveals another encoded layer
  3. Total 116 iterations - Manual extraction would be impractical
  4. Flag name confirms it: "its_a_damn_loop" acknowledges the recursive nature

  Critical Success Factors:

  1. Binwalk detection - Without finding the ZIP offset, challenge couldn't be solved
  2. Automation - Manual extraction of 116 layers would take hours
  3. Pattern recognition - Recognizing the recursive structure early
  4. Scripting skills - Creating robust extraction/decoding loops

  ---
  FILES CREATED DURING SOLUTION

  /home/uttam/Downloads/
  ├── recursive_hell.png          # Original challenge file
  ├── extracted.zip               # Extracted from PNG offset
  ├── extract_recursive.sh        # ZIP extraction script
  ├── recursive_decode.sh         # Base64 decoder script
  ├── temp_68.txt → temp_0.txt   # 68 extracted ZIP files
  └── decoded_0.txt → decoded_48.txt  # 48 Base64 decode iterations

  ---
  COMPLETE COMMAND SEQUENCE

  # 1. Analyze PNG
  binwalk recursive_hell.png

  # 2. Extract embedded ZIP
  dd if=recursive_hell.png of=extracted.zip bs=1 skip=296306

  # 3. Initial extraction
  unzip extracted.zip

  # 4. Run recursive ZIP extractor
  bash extract_recursive.sh

  # 5. Run recursive Base64 decoder
  bash recursive_decode.sh

  # 6. Verify flag
  cat decoded_48.txt
  # Output: EOF{its_a_damn_loop}

  ---
  This was an excellent steganography challenge testing:
  - Binary analysis skills (binwalk, dd)
  - Pattern recognition (identifying recursion)
  - Automation abilities (bash scripting)
  - Persistence (116 iterations!)

  The flag "its_a_damn_loop" perfectly captures the frustration and eventual triumph of solving this recursive nightmare! 🎯
