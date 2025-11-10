# Puzzle 13

## Metadata
- **Status**: Solved
- **Solved Date**: May 23, 2020
- **Solver**: LeFevre
- **Prize**: ETH (amount not specified)
- **Difficulty**: Hard
- **Primary Technique**: Reverse image search + SHA-256 hashing

## Solution
```
Private Key: c79eac48c3334fc967d5aecb37222d9a4307027d0ec2bcd6f914417cf78d3c82
```

## Puzzle Structure
This puzzle contained **8 images**, each with **8 hexadecimal characters** nearby. Solvers needed to identify what each image represented, then perform cryptographic operations to derive the final private key.

---

## The Challenge

**Format**: 8 images + 8 hex strings → Private key

**Key Clue**: "Tail is your friend"

This cryptic hint was crucial to solving the puzzle.

---

## Images & Solutions

### Image 1: Terminator 2
**What it represented**: The movie "Terminator 2: Judgment Day"
**Solution word**: "Terminator 2"

---

### Image 2: Bitcoin Genesis Block
**What it represented**: The first Bitcoin block (Genesis Block)
**Solution word**: "Bitcoin Genesis Block"

---

### Image 3: Tuberculosis
**What it represented**: The disease tuberculosis
**Solution word**: "Tuberculosis"

---

### Image 4: Big Brother
**What it represented**: The concept/character from Orwell's 1984 or the TV show
**Solution word**: "Big Brother"

---

### Image 5: Arweave
**What it represented**: The Arweave project itself
**Solution word**: "Arweave"

---

### Image 6: Terror From the Deep
**What it represented**: The game "X-COM: Terror From the Deep"
**Solution word**: "Terror From the Deep"

---

### Image 7: Dyatlov
**What it represented**: The Dyatlov Pass incident (mysterious 1959 deaths in Ural Mountains)
**Solution word**: "Dyatlov"

---

### Image 8: Vitalik Buterin
**What it represented**: Vitalik Buterin, co-founder of Ethereum
**Solution word**: "Vitalik Buterin"

---

## Solution Method

### Step 1: Reverse Image Search
**Technique**: Upload each image to Google Images or TinEye

For each image:
1. Download/capture the puzzle image
2. Upload to reverse image search engine
3. Identify what the image represents
4. Record the name/phrase

**Why this works**: The images were either famous or specific enough to be identified through reverse image search.

---

### Step 2: Understanding "Tail is your friend"

The clue means: take the **last 8 hexadecimal characters** of something.

But 8 hex characters from what?

---

### Step 3: SHA-256 Hashing

For each identified term:
1. Take the solution word/phrase (e.g., "Terminator 2")
2. Compute SHA-256 hash of the text
3. Take the **last 8 hexadecimal characters** of the hash
4. These should match or relate to the 8 hex characters shown with the image

Example process:
```
Word: "Terminator 2"
SHA-256: [full hash...]...c79eac48
Last 8 chars (tail): c79eac48
```

---

### Step 4: Concatenate All Tails

After computing SHA-256 for all 8 words and extracting the last 8 hex digits from each:

```
Image 1 (Terminator 2):         c79eac48
Image 2 (Bitcoin Genesis Block): c3334fc9
Image 3 (Tuberculosis):         67d5aecb
Image 4 (Big Brother):          37222d9a
Image 5 (Arweave):              4307027d
Image 6 (Terror From the Deep): 0ec2bcd6
Image 7 (Dyatlov):              f914417c
Image 8 (Vitalik Buterin):      f78d3c82
```

**Concatenated Private Key**:
```
c79eac48c3334fc967d5aecb37222d9a4307027d0ec2bcd6f914417cf78d3c82
```

This is a valid 64-character hexadecimal private key (32 bytes = 256 bits), suitable for Ethereum or other cryptocurrency wallets.

---

## Techniques Used

### 1. Reverse Image Search
**Tools**: Google Images, TinEye, Yandex Images
**Skill**: Image identification, visual recognition
**Why important**: First step to convert visual→text

### 2. SHA-256 Cryptographic Hashing
**Function**: SHA-256(text) → 64 hex character hash
**Application**: Generate deterministic hex values from text
**Understanding**: Secure hash function used in Bitcoin and many blockchains

### 3. Hex Manipulation
**Operation**: Extract last 8 characters from 64-char hex string
**Format**: Hexadecimal (0-9, a-f)
**Purpose**: Create manageable segments that concatenate to private key

### 4. Private Key Format Recognition
**Format**: 64 hex characters = 256-bit key
**Usage**: Ethereum, Bitcoin (uncompressed), many cryptocurrencies
**Validation**: Correct length and hex format

### 5. Cultural & Technical Knowledge
Required knowledge domains:
- **Movies**: Terminator 2
- **Cryptocurrency**: Bitcoin Genesis Block, Arweave, Ethereum/Vitalik
- **History**: Dyatlov Pass incident
- **Gaming**: X-COM series
- **Literature**: Big Brother (1984)
- **Medicine**: Tuberculosis

---

## Difficulty Assessment

**Hard** - This puzzle requires:
1. **Reverse image search skills** - not everyone knows this technique
2. **Cryptographic knowledge** - understanding SHA-256 hashing
3. **Programming ability** - computing hashes programmatically
4. **Clue interpretation** - understanding "tail is your friend"
5. **Broad cultural knowledge** - identifying diverse image subjects
6. **Technical assembly** - concatenating results into valid private key format

---

## Tools Needed

### Image Search:
- Google Images (images.google.com)
- TinEye (tineye.com)
- Yandex Images

### SHA-256 Hashing:
```python
import hashlib

def get_tail(text):
    hash_result = hashlib.sha256(text.encode()).hexdigest()
    return hash_result[-8:]

words = [
    "Terminator 2",
    "Bitcoin Genesis Block",
    "Tuberculosis",
    "Big Brother",
    "Arweave",
    "Terror From the Deep",
    "Dyatlov",
    "Vitalik Buterin"
]

private_key = ''.join([get_tail(word) for word in words])
print(private_key)
```

### Online Tools:
- SHA-256 calculators (many available online)
- Hex editors/validators

---

## Key Learning Points

1. **"Tail" in crypto** = last characters of a hash
2. **Reverse image search** is a powerful reconnaissance tool
3. **SHA-256 is deterministic** - same input always produces same output
4. **Private keys are concatenated hashes** - creative construction method
5. **Cultural knowledge matters** - diverse reference recognition required
6. **Clues can be cryptic** - "tail is your friend" requires interpretation

---

## Security Note

The solved puzzle revealed an actual private key, which means the wallet was drained immediately upon solution. This demonstrates:
- **Race condition**: First solver wins
- **Public verification**: Anyone can verify the solution
- **Irreversible**: Once claimed, puzzle is permanently solved

---

## Comparison to Previous Puzzles

**More technical** than Puzzles 1, 2, 4, 8:
- Requires programming/scripting
- Uses cryptographic functions
- Image processing + text processing
- More "hacker-like" skillset

**Similar to modern CTF challenges**:
- OSINT (Open Source Intelligence) via image search
- Cryptography (hashing)
- Format recognition (private keys)
- Clue interpretation

This puzzle bridges **traditional puzzle-solving** with **technical cryptocurrency knowledge**.
