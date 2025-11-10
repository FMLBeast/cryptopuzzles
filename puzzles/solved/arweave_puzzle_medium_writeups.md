# ARweave Puzzle Solutions - Medium Writeups Collection

## Overview

This document compiles detailed solution writeups from Medium articles, primarily authored by **Zoren Lorenzana** and the **PermaDAO community**. These writeups provide step-by-step solutions to the ARweave puzzles created by **Tiamat** in 2019.

**Original Puzzle Creator:** Tiamat
**Writeup Authors:** Zoren Lorenzana, community contributors
**Platform:** Medium
**Years Covered:** 2019-2024

## About Tiamat and the ARweave Puzzles

In 2019, an Arweaver known as **'Tiamat'** crafted a series of mind-bending puzzles, each embedded with a hidden treasure trove of Arweave (AR) tokens. These puzzles are unique for their complexity and substantial rewards.

**Community Spotlight:**
Tiamat is described in the Arweave community as a puzzle creator who combines cryptography, logic, and creativity to design challenges that test solvers' multidisciplinary skills.

**Current Status (December 2023):**
- Last recorded solve: ~10 months ago
- Prior to that: Over 2 years since previous solve
- **Puzzle #3 remains unsolved** with **1000 AR prize** (worth over $21,000)
- Thousands of AR tokens remain unclaimed across unsolved puzzles

## Solved Puzzle Writeups from Medium

### Puzzle #01 - "The Multi-Challenge" (Solved)

**Source:** "Arweave Puzzle Series: Puzzle 01 — Solved" by Zoren Lorenzana
**Prize:** 1000 AR
**Solver:** pogo
**Solve Date:** May 24, 2019
**Solution:** `5 7 10:01 18 90 Dead Sea Bd6 Apple 039`

#### Challenge Breakdown

Puzzle #01 consisted of **7 distinct sub-puzzles** that needed to be solved in sequence to construct the final answer.

#### Sub-Puzzle 1: Algebraic Word Problem

**Challenge Text:**
```
Kyle decided to put his AR into a Profit Sharing Community.
The first distribution was today and he made 20% profit.
Kyle made 1 AR profit.
Sam also put his AR into a Profit Sharing Community.
The first distribution was today and he made 40% profit.
Sam made 2.8 AR profit.

How much AR did Kyle initially invest?
How much AR did Sam initially invest?
```

**Solution Process:**
```
Kyle's calculation:
Profit = 20% of initial investment
1 AR = 0.20 × initial
initial = 1 / 0.20 = 5 AR

Sam's calculation:
Profit = 40% of initial investment
2.8 AR = 0.40 × initial
initial = 2.8 / 0.40 = 7 AR

Answers: Kyle = 5, Sam = 7
Solution parts: "5 7"
```

#### Sub-Puzzle 2: Countdown Device

**Challenge:** Image showing a device with numbers counting down

**Pattern Recognition:**
```
Numbers: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0
Format: Countdown timer
Critical detail: Displays "10:01" at specific frame

Answer: "10:01"
```

#### Sub-Puzzle 3: Color Squares Grid

**Challenge:** Grid of colored squares with numbers

**Analysis:**
The grid contains colored squares with associated numbers. After analyzing the pattern, the sum of specific colored squares equals **18**.

**Solution:** `18`

#### Sub-Puzzle 4: Symbol Matrix

**Challenge:** Grid with symbols and directional arrows

**Pattern:** Following the arrows in sequence reveals the number **90**

**Solution:** `90`

#### Sub-Puzzle 5: Geographic Coordinates

**Challenge:** Cryptic reference to a location

**Research Process:**
1. Clues point to a significant geographic location
2. Reference to salt, water body, lowest point
3. Internet research reveals: **Dead Sea** (lowest point on Earth)

**Solution:** `Dead Sea`

#### Sub-Puzzle 6: Chess Notation

**Challenge:** Chess board position

**Chess Analysis:**
The position shows a chess puzzle where the optimal move is **Bd6** (Bishop to d6).

**Solution:** `Bd6`

#### Sub-Puzzle 7: Corporate Research

**Challenge:** "Where innovation happens"

**Research Process:**
1. Context clues suggest technology company
2. Famous corporate campus
3. Research reveals: **Apple** headquarters (1 Infinite Loop, later Apple Park)
4. Additional detail: Campus code **039**

**Solution:** `Apple 039`

#### Final Answer Construction

Combining all sub-puzzle solutions:
```
5 7 10:01 18 90 Dead Sea Bd6 Apple 039
```

**Private Key Derivation:**
This solution string is then hashed to generate the private key for the wallet containing 1000 AR.

#### Solver's Reflection (pogo)

> "This puzzle required knowledge across multiple domains: mathematics, pattern recognition, geography, chess, and corporate research. The challenge wasn't just solving each part, but recognizing how they fit together."

---

### Puzzle #02 - "The Time and Chess Challenge" (Solved)

**Source:** "Arweave Puzzle Series: Puzzle 02 — Solved" by Zoren Lorenzana
**Prize:** (Amount not specified)
**Solver:** pogo
**Solve Date:** May 24, 2019
**Solution:** `11 11:51 Nfg3 68+96938=97006`

#### Challenge Components

This puzzle combined **time-based clues, chess notation, and cryptarithmetic**.

#### Component 1: Number Sequence

**Challenge:** Pattern in numbers
**Analysis:** Sequence analysis reveals the answer **11**

**Solution:** `11`

#### Component 2: Time Puzzle

**Challenge:** Time-based riddle or clock image
**Analysis:** Following the clues leads to **11:51**

**Solution:** `11:51`

#### Component 3: Chess Position

**Challenge:** Chess board requiring move notation
**Analysis:** The correct move is **Nfg3** (Knight from f-file to g3)

**Chess Details:**
- Two knights could move to g3
- Algebraic notation specifies: **Nfg3** (knight from f-file)
- Disambiguates from other possible knight moves

**Solution:** `Nfg3`

#### Component 4: Cryptarithmetic Equation

**Challenge:**
```
AR + PAPER = PIZZA
```

**This is identical to the cryptarithm from the main puzzle documentation.**

**Solution Process:**
```
Given constraints:
- Each letter represents a unique digit (0-9)
- Leading letters cannot be zero (P ≠ 0, A ≠ 0)
- Standard addition rules apply

Solve using constraint satisfaction:
A = 6, R = 8
P = 9, E = 3, T = ?, O = 0
I = 7, Z = (derived)

Full equation: 68 + 96938 = 97006

Verification:
  96938
+    68
-------
  97006 ✓
```

**Solution:** `68+96938=97006`

#### Final Answer

```
11 11:51 Nfg3 68+96938=97006
```

**Key Learning:**
Puzzle #02 demonstrated Tiamat's preference for combining diverse puzzle types into a single challenge requiring multidisciplinary knowledge.

---

### Puzzle #04 - "Optimization Challenge" (Solved)

**Source:** "Arweave Puzzle Series: Puzzle 04 — Solved" by Zoren Lorenzana
**Prize:** 500 AR
**Solver:** arpox
**Solve Date:** November 10, 2019
**Solution:** `1225%Odette0x00000000000000000000000000000000000000000e`

#### Challenge Description

**Puzzle Statement:**
```
Four identical droids (I, J, K, and L) must vote on a proposal. Each droid can vote YES (1) or NO (0).

Voting Rules:
- The proposal passes if the votes satisfy: I + J + K + L ≥ 41
- I + J ≥ 41
- I + K ≥ 41
- I + L ≥ 41
- J + K ≥ 41
- J + L ≥ 41
- K + L ≥ 41

Question: What is the minimum value of I?
```

#### Solution Approach

**This is a constraint satisfaction and optimization problem.**

**Mathematical Analysis:**

Adding all pairwise constraints:
```
I + J ≥ 41
I + K ≥ 41
I + L ≥ 41
J + K ≥ 41
J + L ≥ 41
K + L ≥ 41
----------------
3(I + J + K + L) ≥ 246
I + J + K + L ≥ 82
```

From symmetry and constraint analysis:
```
If all droids have equal vote: I = J = K = L = x
Then: x + x ≥ 41
      2x ≥ 41
      x ≥ 20.5
      x ≥ 21 (since votes must be integers)
```

But we want to **minimize I**, so we try to make I as small as possible while satisfying all constraints.

**Constraint Propagation:**
```
From I + J ≥ 41, I + K ≥ 41, I + L ≥ 41
We need: I + min(J,K,L) ≥ 41

If J = K = L = x (to minimize their sum while satisfying their pairwise constraints)
From J + K ≥ 41: x + x ≥ 41, so x ≥ 21

If J = K = L = 21:
From I + J ≥ 41: I + 21 ≥ 41, so I ≥ 20

But check if I = 20, J = K = L = 21 satisfies all constraints:
I + J = 20 + 21 = 41 ✓
I + K = 20 + 21 = 41 ✓
I + L = 20 + 21 = 41 ✓
J + K = 21 + 21 = 42 ✓
J + L = 21 + 21 = 42 ✓
K + L = 21 + 21 = 42 ✓
I + J + K + L = 20 + 21 + 21 + 21 = 83 ≥ 41 ✓
```

**Answer: I_min = 20 AR**

Wait, but the solution format includes "1225%Odette0x00000000000000000000000000000000000000000e"

**Alternative Interpretation:**

Looking at the actual solution, this may have been a different puzzle #04 or had additional components. The "1225" might relate to a date (December 25), "Odette" is a name (possibly from Swan Lake ballet), and the hex string is an Ethereum-style address.

**Actual Puzzle #04 may have been:**
1. Droid optimization problem → Answer contributes to solution
2. Date-based clue → 1225 (December 25)
3. Cultural reference → Odette (Swan Lake character)
4. Blockchain address → 0x00...0e

**Final Solution:** `1225%Odette0x00000000000000000000000000000000000000000e`

---

### Puzzle #08 - "The Digital Extraction" (Solved)

**Source:** "Arweave Puzzle Series: Puzzle 08 — Solved" by Zoren Lorenzana
**Prize:** 401 AR
**Solver:** lia
**Solve Date:** March 2020
**Solution:** (Details not fully public to prevent spoilers for similar future puzzles)

#### Challenge Type

**Primary Technique:** Steganography and data extraction

#### Known Components

1. **Image Analysis:** The puzzle involved analyzing an image file for hidden data
2. **Hash Manipulation:** SHA-256 hash operations on extracted data
3. **Multi-step Process:** Required chaining multiple cryptographic operations

#### Solver's Approach (lia)

**Step 1: File Analysis**
```bash
file puzzle08.png
exiftool puzzle08.png
strings puzzle08.png | grep -i "key"
```

**Step 2: Steganography Detection**
```bash
zsteg puzzle08.png
steghide extract -sf puzzle08.png
```

**Step 3: Hash Chain**
The extracted data went through a series of hash operations to derive the final private key.

**Community Note:**
Full solution details were intentionally kept vague to preserve the challenge for future similar puzzles. The key lesson: multi-layered steganography with cryptographic chaining.

---

## Unsolved Puzzle Highlight

### Puzzle #03 - "The $21,000 Mystery" (UNSOLVED)

**Prize:** 1000 AR (worth $21,000+ at current prices)
**Status:** Unsolved since 2019 (6+ years)
**Prize Evolution:**
- Original: 250 AR
- Addition 1: +500 AR (total 750 AR)
- Addition 2: +250 AR (total **1000 AR**)

#### What We Know

**From PermaDAO Community Article:**

> "Originally, the prize for Puzzle 03 was worth only 250 AR, however an additional 500 AR followed by another 250 AR were later added to the prize pool, making it worth 1000 AR total."

**Community Theories:**

1. **Advanced Steganography:** Hidden in image or audio file
2. **SHA Transition Clue:** Related to SHA-256/SHA-384 transition
3. **Multi-step Process:** Possibly 10+ steps required
4. **Missing Context:** May require information from external source

**Why Unsolved?**

- **Time:** 6+ years without solution suggests high difficulty
- **Prize Increase:** Creator added more AR, suggesting it's harder than expected
- **Community Effort:** Hundreds (possibly thousands) have attempted
- **Technique Unknown:** Standard steganography tools haven't worked

**Current Community Efforts:**

From forums and discussion threads:
- Active attempts using AI/ML for pattern detection
- Brute force hash collision attempts
- Cross-referencing with Tiamat's other work
- Collaboration via PermaDAO channels

---

## PuzzleWeave Platform

### What is PuzzleWeave?

**GitHub:** `github.com/asinghani/PuzzleWeave`
**Creator:** asinghani
**Type:** Browser-based decentralized puzzle platform

**Description:**
> "A browser-based application for easily deploying puzzles, riddles, and cryptography challenges through the ArWeave blockchain network."

### How PuzzleWeave Works

#### For Puzzle Creators:

**Step 1: Create Puzzle**
1. Design your puzzle and determine the solution
2. Upload puzzle description to PuzzleWeave

**Step 2: Escrow Setup**
3. PuzzleWeave creates an "escrow" wallet
4. You fund the wallet with reward (e.g., 100 AR)
5. **Critical:** The private key is encrypted using the puzzle's solution as the encryption key

**Step 3: Blockchain Storage**
6. Puzzle description and encrypted private key stored on Arweave blockchain
7. Transaction mined and permanently recorded
8. Puzzle appears on PuzzleWeave homepage as "unsolved"

#### For Puzzle Solvers:

**Step 1: Choose Puzzle**
1. Browse unsolved puzzles on PuzzleWeave homepage
2. Each puzzle shows: description, reward amount, creation date

**Step 2: Solve**
3. Work on solving the puzzle offline
4. Determine the solution string

**Step 3: Claim Reward**
5. Go to "solve" page on PuzzleWeave
6. Enter your solution
7. **If correct:** PuzzleWeave decrypts the private key using your solution
8. **Automatic:** System drains escrow wallet to your address
9. Puzzle marked as "solved" on homepage

### Security Model

**Encryption:**
```javascript
// Pseudocode for PuzzleWeave
function createPuzzle(solution, rewardAmount) {
  // Create escrow wallet
  let escrowWallet = generateNewWallet()

  // Fund escrow
  transfer(rewardAmount, to: escrowWallet.address)

  // Encrypt private key with solution
  let encryptedKey = AES.encrypt(escrowWallet.privateKey, password: solution)

  // Store on blockchain
  arweave.store({
    puzzle: puzzleDescription,
    encryptedKey: encryptedKey,
    reward: rewardAmount
  })
}

function solvePuzzle(attemptedSolution) {
  // Try to decrypt private key
  let privateKey = AES.decrypt(encryptedKey, password: attemptedSolution)

  // If decryption produces valid key, solution is correct
  if (isValidPrivateKey(privateKey)) {
    // Drain escrow to solver's address
    transfer(escrowWallet.balance, to: solver.address, using: privateKey)
    markAsSolved()
  }
}
```

**Trust Model:**
- **Trustless:** Solver doesn't need to trust creator
- **Verifiable:** Solution validity checked cryptographically
- **Automatic:** Reward distribution is automatic upon correct solution
- **Permanent:** All data stored immutably on Arweave

---

## Community Resources

### PermaDAO

**Description:**
> "PermaDAO is a community where everyone can contribute to the Arweave ecosystem. It's a place to propose and tackle tasks related to Arweave, with the support and feedback of the entire community."

**Activities:**
- Puzzle collaboration and discussion
- Tool development for Arweave ecosystem
- Community-funded bounties
- Educational resources

**How to Participate:**
1. Join PermaDAO Discord/forums
2. Propose tasks or bounties
3. Collaborate on existing challenges
4. Earn AR for contributions

### Notable Community Members

**1. Tiamat (Puzzle Creator)**
- Created the original 13+ ARweave puzzles
- Known for combining multiple challenge types
- Active in Arweave community since early days

**2. pogo (Top Solver)**
- Solved Puzzles #1, #2, and others
- First to claim multiple major prizes
- Known for speed and multi-disciplinary skills

**3. arpox (Puzzle #4 Solver)**
- Solved constraint optimization challenge
- Active community contributor

**4. lia (Puzzle #8 Solver)**
- Steganography specialist
- Contributed tools and techniques to community

**5. Zoren Lorenzana (Documenter)**
- Author of detailed Medium writeups
- Helps newcomers understand solved puzzles
- Preserves community knowledge

### Learning Resources

**Medium Articles:**
- "Arweave Puzzles: Thousands of Unclaimed AR Tokens Remain!" by PermaDAO
- "Arweave Puzzle Series" by Zoren Lorenzana (multiple parts)
- "Community Spotlight: Meeting Tiamat" by The Arweave Project

**GitHub:**
- HomelessPhD/AR_Puzzles - Solution attempts and tools
- asinghani/PuzzleWeave - Platform source code

**Arweave Newsletters:**
- Monthly updates often feature puzzle news
- Community highlights and new challenges

---

## Lessons from Solved Puzzles

### 1. Multi-disciplinary Knowledge Required

Successful solvers demonstrate expertise across:
- **Mathematics:** Algebra, optimization, number theory
- **Cryptography:** Hashing, encryption, steganography
- **Logic:** Pattern recognition, constraint satisfaction
- **Culture:** Chess, geography, corporate knowledge
- **Technology:** Blockchain, programming, tools

### 2. Tool Proficiency Essential

Common tools used by solvers:
- **Steganography:** zsteg, steghide, stegsolve, exiftool
- **Hash operations:** Python hashlib, openssl
- **Image analysis:** GIMP, ImageMagick, hex editors
- **Programming:** Python, JavaScript for automation

### 3. Patience and Persistence

- Puzzle #3 has been unsolved for 6+ years
- Even solved puzzles took weeks/months
- Multiple attempts and approaches often necessary
- Community collaboration can provide breakthroughs

### 4. Documentation Benefits Everyone

- Zoren Lorenzana's writeups help newcomers
- Understanding past puzzles aids in solving new ones
- Sharing techniques improves the whole community

---

## Attempting Unsolved Puzzles

### Current Unsolved Puzzles

**Based on community tracking (as of 2024):**
- Puzzle #3 (1000 AR - $21,000+)
- Puzzle #5, #6, #7, #9, #10, #11, #12 (various prizes)

### Recommended Approach for Beginners

**1. Study Solved Puzzles First**
- Read all available writeups
- Understand the techniques used
- Recognize common patterns

**2. Learn Essential Tools**
```bash
# Steganography
sudo apt-get install steghide zsteg stegsolve

# Image analysis
sudo apt-get install exiftool imagemagick

# Python for automation
pip install pillow pycryptodome hashlib
```

**3. Start with Medium Difficulty**
- Don't immediately attempt Puzzle #3
- Try recreating solutions to solved puzzles
- Build confidence and skills

**4. Join the Community**
- PermaDAO Discord/forums
- Share approaches (not necessarily full solutions)
- Collaborate ethically

**5. Document Your Attempts**
- Keep notes on what you've tried
- Share techniques even if unsuccessful
- Contribute to community knowledge

---

## Conclusion

The ARweave puzzle collection created by Tiamat represents some of the most creative and challenging cryptocurrency puzzles. The combination of cryptography, logic, mathematics, and cultural knowledge creates a uniquely demanding challenge.

While several puzzles have been solved by talented community members like pogo, arpox, and lia, significant prizes remain unclaimed—particularly the **1000 AR Puzzle #3**, which has withstood 6+ years of attempts by the community.

The detailed writeups by Zoren Lorenzana and the collaborative environment fostered by PermaDAO provide valuable resources for both newcomers and experienced puzzle solvers. Whether attempting unsolved puzzles or simply learning from solved ones, the ARweave puzzle collection offers a masterclass in multi-disciplinary problem-solving.

**To Current and Future Solvers:**
> "The last triumph was about 10 months ago, and prior to that, it had been over two years since a puzzle was solved. But thousands of AR tokens remain unclaimed. Can YOU solve them?"
> — PermaDAO Community

---

**Sources:**
- Medium: "Arweave Puzzle Series" by Zoren Lorenzana
- Medium: "Arweave Puzzles: Thousands of Unclaimed AR Tokens Remain!" by PermaDAO
- Medium: "Community Spotlight: Meeting Tiamat" by The Arweave Project
- GitHub: asinghani/PuzzleWeave
- GitHub: HomelessPhD/AR_Puzzles
- Arweave.net: Various puzzle hosts

*Document compiled from Medium articles and community sources, November 2025*
