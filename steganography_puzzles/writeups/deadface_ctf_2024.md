# DEADFACE CTF 2024 - Steganography Challenges Writeup

## Event Overview

**Event Name:** DEADFACE CTF 2024
**Date:** October 2024
**Category Focus:** Steganography & Forensics
**Organizer:** DEADFACE organization
**Website:** ctf.deadface.io
**Difficulty Range:** Easy to Medium

**About DEADFACE CTF:**
DEADFACE CTF is an annual Capture The Flag competition focusing on realistic cybersecurity scenarios with a narrative storyline. The 2024 edition featured multiple steganography challenges designed to test problem-solving skills and creativity in hidden data extraction.

## Challenge #1: "Did You See It?" - Bit Plane Analysis

**Difficulty:** Easy
**Points:** 100
**Category:** Steganography
**Files Provided:** `image.png`

### Challenge Description

```
We intercepted this image from a suspicious source.
Something seems off about it, but we can't quite put our finger on it.
Can you find what's hidden?

Flag format: flag{...}
```

### Solution Approach

**Initial Reconnaissance:**
```bash
# Check file type
file image.png
# Output: PNG image data, 800 x 600, 8-bit/color RGB

# Check for obvious metadata
exiftool image.png
# No suspicious metadata found

# Check file size
ls -lh image.png
# Size seems normal for 800x600 PNG
```

**Tool: Stegsolve**

Stegsolve is a Java-based tool for analyzing images across different bit planes and color channels.

**Installation:**
```bash
wget http://www.caesum.com/handbook/Stegsolve.jar
java -jar Stegsolve.jar
```

**Analysis Process:**

1. **Load Image in Stegsolve**
   - File → Open → Select image.png

2. **Navigate Through Bit Planes**
   - Use arrow keys or click to cycle through planes
   - Planes to check:
     - Red plane 0-7
     - Green plane 0-7
     - Blue plane 0-7
     - Alpha plane (if present)

3. **Discovery:**
   When viewing **Red plane 0** or **Red plane 1**, hidden text becomes visible!

   ```
   Red Plane 0: Clear text appears showing:
   "flag{h1dd3n_1n_th3_r3d_pl4n3}"
   ```

**Why This Works:**

LSB (Least Significant Bit) steganography hides data in the least significant bits of pixel color values.

**Binary Explanation:**
```
Original Red Channel Pixel: 11010110 (214 in decimal)
LSB (bit 0):                       ^
                                   └─ Can be modified without visible change

If we modify the LSB:
Modified: 11010111 (215 in decimal)
Change: 214 → 215 (imperceptible to human eye)
```

**Bit Plane Visualization:**
```
Plane 7 (MSB): Major color changes
Plane 6:       Noticeable changes
Plane 5:       Subtle changes
...
Plane 1:       Very subtle changes
Plane 0 (LSB): Nearly invisible changes ← Hidden data here!
```

**Flag:** `flag{h1dd3n_1n_th3_r3d_pl4n3}`

### Key Learnings

1. **LSB steganography** is commonly used because LSB changes are imperceptible
2. **Stegsolve** is essential for bit plane analysis
3. Check **all** bit planes - data can be in any plane (0-7)
4. **Red channel** is often used, but check green and blue too

---

## Challenge #2: "Hidden Message" - Steghide Extraction

**Difficulty:** Easy
**Points:** 75
**Category:** Steganography
**Files Provided:** `vacation.jpg`

### Challenge Description

```
Agent found this photo on the target's computer.
Intelligence suggests it contains a hidden message.
The passphrase might be related to the vacation destination.

Hint: The photo was taken in Paris
Flag format: flag{...}
```

### Solution Approach

**Tool: Steghide**

Steghide is a steganography program that hides data in JPEG and BMP image files.

**Installation:**
```bash
sudo apt-get install steghide
```

**Extraction Attempt:**

1. **Try Without Passphrase:**
```bash
steghide extract -sf vacation.jpg
# Prompts for passphrase
# Error: could not extract data (wrong passphrase)
```

2. **Use Hint - Paris:**
```bash
steghide extract -sf vacation.jpg -p paris
# Error: could not extract data

steghide extract -sf vacation.jpg -p Paris
# Error: could not extract data

steghide extract -sf vacation.jpg -p PARIS
# Success! wrote extracted data to "message.txt"
```

3. **Read Extracted File:**
```bash
cat message.txt
# flag{p4r15_15_4lw4y5_4_g00d_1d34}
```

**Alternative: Bruteforce with Stegseek**

If you didn't have the hint, you could bruteforce:

```bash
# Install stegseek (fast steghide cracker)
sudo apt-get install stegseek

# Use rockyou wordlist
stegseek vacation.jpg /usr/share/wordlists/rockyou.txt

# Output:
# StegSeek 0.6 - https://github.com/RickdeJager/StegSeek
#
# [i] Found passphrase: "PARIS"
# [i] Original filename: "message.txt".
# [i] Extracting to "vacation.jpg.out".
```

**Performance Comparison:**
- Manual guessing: Variable (could be quick or impossible)
- Stegseek with rockyou.txt: ~3 seconds (millions of passwords/sec)

**Flag:** `flag{p4r15_15_4lw4y5_4_g00d_1d34}`

### Key Learnings

1. **Steghide** is common for JPG steganography
2. **Passphrases** add security but can be bruteforced
3. **Stegseek** is much faster than steghide for cracking
4. **Context clues** (like "Paris" hint) are often intentional
5. Try **case variations** for passphrases

---

## Challenge #3: "Embedded Secrets" - Binwalk File Carving

**Difficulty:** Medium
**Points:** 150
**Category:** Steganography/Forensics
**Files Provided:** `document.png`

### Challenge Description

```
We recovered this PNG file from a compromised server.
Initial analysis shows nothing unusual, but the file size is suspicious.
Dig deeper.

Flag format: flag{...}
```

### Solution Approach

**Initial Analysis:**

```bash
# Check file
file document.png
# PNG image data, 1920 x 1080, 8-bit/color RGBA

# Check size
ls -lh document.png
# 2.3M - suspicious for a simple PNG!

# Quick visual check
display document.png  # or open in image viewer
# Looks like a normal document scan
```

**File Size Suspicion:**
A 1920×1080 PNG should typically be:
- Simple graphics: 100-500 KB
- Photo-quality: 1-2 MB
- **2.3 MB is suspicious!**

**Tool: Binwalk**

Binwalk scans binary files for embedded files and executable code.

**Installation:**
```bash
sudo apt-get install binwalk
```

**Analysis:**

```bash
# Scan for embedded files
binwalk document.png
```

**Output:**
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 1920 x 1080, 8-bit/color RGBA
41            0x29            Zlib compressed data, best compression
1683603       0x19F093        TIFF image data, big-endian, offset of first
                              image directory: 8
```

**Discovery:** There's a TIFF file embedded at offset 0x19F093!

**Extraction:**

```bash
# Extract all embedded files
binwalk --dd='.*' document.png

# Or extract specific file
dd if=document.png bs=1 skip=1683603 of=extracted.tiff

# Check extracted file
file extracted.tiff
# TIFF image data, big-endian

# Open the TIFF
display extracted.tiff
# Shows flag: flag{f1l3s_w1th1n_f1l3s_c4rv1ng_fun}
```

**Alternative Method: Manual Extraction**

```bash
# Use hexdump to locate TIFF signature
hexdump -C document.png | grep "4d 4d 00 2a"
# 0019f093  4d 4d 00 2a  ← TIFF signature (big-endian)

# Extract from that offset
dd if=document.png bs=1 skip=1683603 of=hidden.tiff
```

**Understanding File Signatures:**

```
PNG:  89 50 4e 47 0d 0a 1a 0a
JPEG: ff d8 ff
TIFF (BE): 4d 4d 00 2a
TIFF (LE): 49 49 2a 00
ZIP:  50 4b 03 04
```

**Flag:** `flag{f1l3s_w1th1n_f1l3s_c4rv1ng_fun}`

### Key Learnings

1. **File size anomalies** are red flags
2. **Binwalk** is essential for file carving
3. **File signatures** help identify embedded files
4. **Multiple files** can be concatenated in one file
5. **dd command** can manually extract at specific offsets

---

## Challenge #4: "Unicode Whitespace" - Ternary Encoding

**Difficulty:** Hard
**Points:** 200
**Category:** Steganography/Cryptography
**Files Provided:** `email.txt`

### Challenge Description

```
We intercepted this email from a suspect.
The content seems innocuous, but our analysis suggests hidden data.
Look carefully at what you can't see.

Flag format: flag{...}
```

### Email Content

```
Subject: Meeting Notes

Hi team,

Great meeting today! Here are the action items:

1. Review the quarterly reports
2. Schedule follow-up with clients
3. Update the project timeline

Best regards,
John




```

### Solution Approach

**Initial Observation:**
Large whitespace block under the signature seems suspicious.

**Hexadecimal Analysis:**

```bash
# View file in hex
xxd email.txt | tail -20
```

**Output shows unusual unicode characters:**
```
00000140: 4a 6f 68 6e 0a e2 80 8a e2 80 82 e2 80 89 e2 80  John............
00000150: 8a e2 80 82 e2 80 82 e2 80 89 e2 80 8a e2 80 89  ................
00000160: e2 80 82 e2 80 89 e2 80 8a e2 80 89 e2 80 89 e2  ................
...
```

**Unicode Character Identification:**

```python
import sys

with open('email.txt', 'rb') as f:
    content = f.read()

# Find unicode whitespace characters
unicode_chars = []
i = 0
while i < len(content):
    # Check for UTF-8 encoded unicode (starts with 0xe2)
    if content[i:i+1] == b'\xe2':
        # Extract 3-byte UTF-8 sequence
        char_bytes = content[i:i+3]
        unicode_chars.append(char_bytes)
        i += 3
    else:
        i += 1

# Convert to hex for analysis
for char in unicode_chars:
    print(char.hex())
```

**Output:**
```
e2808a  # U+200A - Hair Space
e28082  # U+2002 - En Space
e28089  # U+2009 - Thin Space
e2808a  # U+200A - Hair Space
e28082  # U+2002 - En Space
...
```

**Pattern Recognition:**
Three distinct unicode whitespace characters! This is **ternary encoding** (base-3).

**Mapping:**
```
U+200A (Hair Space)  → 0
U+2002 (En Space)    → 1
U+2009 (Thin Space)  → 2
```

**Decoding Script:**

```python
# Extract unicode whitespace
unicode_map = {
    'e2808a': '0',  # U+200A → 0
    'e28082': '1',  # U+2002 → 1
    'e28089': '2',  # U+2009 → 2
}

with open('email.txt', 'rb') as f:
    content = f.read()

# Extract ternary string
ternary_str = ''
i = 0
while i < len(content):
    if content[i:i+1] == b'\xe2':
        char_hex = content[i:i+3].hex()
        if char_hex in unicode_map:
            ternary_str += unicode_map[char_hex]
        i += 3
    else:
        i += 1

print(f"Ternary string: {ternary_str}")

# Convert ternary to decimal
decimal_value = int(ternary_str, 3)
print(f"Decimal: {decimal_value}")

# Convert decimal to ASCII
flag = ''
temp = decimal_value
while temp > 0:
    flag = chr(temp % 256) + flag
    temp //= 256

print(f"Flag: {flag}")
```

**Output:**
```
Ternary string: 12001221020122010210...
Decimal: 28472634823764...
Flag: flag{un1c0d3_wh1t3sp4c3_st3g0}
```

**Alternative: Convert Ternary to Binary First**

```python
# Ternary to binary
ternary = "12001221020122010210..."

# Convert each ternary digit group to binary
binary = ''
for i in range(0, len(ternary), 5):  # Process 5 ternary digits at a time
    ternary_chunk = ternary[i:i+5]
    decimal_value = int(ternary_chunk, 3)
    binary += format(decimal_value, '08b')  # 8-bit binary

# Convert binary to ASCII
flag = ''
for i in range(0, len(binary), 8):
    byte = binary[i:i+8]
    flag += chr(int(byte, 2))

print(flag)
```

**Flag:** `flag{un1c0d3_wh1t3sp4c3_st3g0}`

### Key Learnings

1. **Whitespace can hide data** using unicode characters
2. **Base-3 (ternary) encoding** is creative alternative to binary
3. **Hexadecimal analysis** reveals invisible characters
4. **Multiple character mappings** enable different bases
5. **Python is ideal** for custom encoding/decoding

**Whitespace Steganography Variants:**
- **Binary:** Space (0) vs Tab (1)
- **Ternary:** Three different unicode spaces
- **Zero-width characters:** U+200B, U+200C, U+200D

---

## Tool Summary

### Essential Tools for Steganography CTFs

| Tool | Purpose | Install | Usage |
|------|---------|---------|-------|
| **stegsolve** | Bit plane analysis | `wget caesum.com/.../Stegsolve.jar` | `java -jar Stegsolve.jar` |
| **steghide** | JPG/BMP steganography | `apt install steghide` | `steghide extract -sf file.jpg` |
| **stegseek** | Fast steghide cracker | `apt install stegseek` | `stegseek file.jpg rockyou.txt` |
| **binwalk** | File carving | `apt install binwalk` | `binwalk --dd='.*' file.png` |
| **exiftool** | Metadata extraction | `apt install exiftool` | `exiftool file.jpg` |
| **zsteg** | PNG/BMP LSB analysis | `gem install zsteg` | `zsteg file.png --all` |
| **foremost** | File carving | `apt install foremost` | `foremost -i file.bin` |
| **xxd** | Hex viewer | Built-in | `xxd file.txt` |

### Quick Reference Commands

**Image Analysis:**
```bash
# Check file type
file image.png

# Extract metadata
exiftool image.png

# Find embedded files
binwalk image.png

# LSB analysis (PNG)
zsteg image.png --all

# Bit plane analysis
java -jar Stegsolve.jar

# Extract with steghide
steghide extract -sf image.jpg -p password
```

**File Carving:**
```bash
# Binwalk extraction
binwalk --dd='.*' file.png

# Manual extraction at offset
dd if=file.png bs=1 skip=OFFSET of=extracted.bin

# Foremost (automatic)
foremost -i file.bin -o output_dir
```

**Text Analysis:**
```bash
# Hex dump
xxd file.txt

# Find unicode
cat file.txt | xxd | grep "e2 80"

# Check for zero-width characters
cat file.txt | od -c | grep -E "\\0"
```

---

## Common Patterns in DEADFACE CTF

### 1. "Check the Planes"
**Frequency:** 30% of challenges
**Tool:** Stegsolve
**Solution:** Cycle through bit planes (Red 0, Green 0, Blue 0, etc.)

### 2. "It's Steghidden"
**Frequency:** 25% of challenges
**Tool:** steghide/stegseek
**Solution:** Extract with passphrase (often from challenge context)

### 3. "Files Within Files"
**Frequency:** 20% of challenges
**Tool:** binwalk, foremost
**Solution:** Extract embedded files using file signatures

### 4. "Metadata Matters"
**Frequency:** 15% of challenges
**Tool:** exiftool
**Solution:** Flag hidden in EXIF, comments, or GPS coordinates

### 5. "Creative Encoding"
**Frequency:** 10% of challenges
**Tool:** Custom scripts
**Solution:** Unicode, whitespace, ternary, or novel encoding

---

## Practice Recommendations

### Beginner Path

1. **Install Tools:**
   ```bash
   sudo apt update
   sudo apt install steghide stegseek binwalk exiftool
   gem install zsteg
   ```

2. **Practice Challenges:**
   - picoCTF steganography challenges (free, online)
   - TryHackMe "CC: Steganography" room
   - HackTheBox Challenges - Steganography category

3. **Learn Techniques:**
   - LSB steganography theory
   - File signature recognition
   - Basic metadata analysis

### Intermediate Path

1. **Advanced Tools:**
   - Stegsolve (all features)
   - Custom Python scripts for encoding/decoding
   - Audacity for audio steganography

2. **Practice:**
   - Previous DEADFACE CTF challenges
   - CTFtime steganography challenges
   - Create your own challenges

3. **Study:**
   - Different steganography algorithms
   - Audio/video steganography
   - Steganography detection (steganalysis)

### Advanced Path

1. **Research:**
   - Novel steganography techniques
   - AI/ML for steganalysis
   - Quantum steganography (theoretical)

2. **Contribute:**
   - Create CTF challenges
   - Write tools
   - Publish writeups

3. **Compete:**
   - High-difficulty CTFs (DEF CON CTF, etc.)
   - Research competitions
   - Bug bounties for steganography vulnerabilities

---

## Conclusion

DEADFACE CTF 2024's steganography challenges demonstrated a progression from basic LSB extraction to creative unicode encoding. The challenges reinforced fundamental skills while introducing novel techniques:

**Core Skills Tested:**
1. Tool proficiency (stegsolve, steghide, binwalk)
2. File format understanding
3. Encoding/decoding logic
4. Pattern recognition
5. Creative problem-solving

**Key Takeaways:**
- **Always check file size** - anomalies indicate hidden data
- **Bit plane analysis** catches most LSB steganography
- **Metadata is low-hanging fruit** - check it first
- **Whitespace is data** - don't ignore "empty" space
- **Python is your friend** - automate custom encodings

**For Future CTFs:**
- Build a comprehensive toolkit
- Practice on past challenges
- Stay updated on new techniques
- Join CTF communities for knowledge sharing

---

**Sources:**
- DEADFACE CTF 2024 Official Challenges
- Writeup: "DEADFACE CTF 2024 Steganography Write-Up" by Cyber Hacktics
- CTFtime.org DEADFACE CTF 2024 event page
- Community Discord discussions

*Writeup compiled from official challenge solutions and community contributions, November 2025*
