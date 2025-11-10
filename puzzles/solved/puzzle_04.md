# Puzzle Weave 4

## Metadata
- **Status**: Solved
- **Announced**: May 29, 2019
- **Solved**: November 10, 2019 (5.5 months later)
- **Solver**: arpox
- **Prize**: 500 AR
- **Difficulty**: Medium
- **ARweave URL**: [ojducxyzj2dirbt7xt2jod7dkwfqolxjre6tzp63fycuq5477vta.arweave.net](https://ojducxyzj2dirbt7xt2jod7dkwfqolxjre6tzp63fycuq5477vta.arweave.net/ckdBXxlOhoiGf7z0lw_jVYsHLumJPTy_2y4FSHef_WY)

## Solution
```
1225%Odette0x00000000000000000000000000000000000000000e
```

## Puzzle Structure
This puzzle contained 5 riddles with no spaces in the final solution format. The solution combines numerical answers, text answers, and hexadecimal notation.

---

## Sub-Puzzles & Solutions

### 1. AR Distribution Problem (Algebra)
**Question**: India, Sophie, Lev and Martin have 100 AR altogether. Each two of them have at least 41 AR. What is the lowest possible number of AR India has?

**Solution**: **12** AR

**Method**:
Let's denote: I = India, S = Sophie, L = Lev, M = Martin

Given:
- I + S + L + M = 100
- Any pair sums to at least 41

To minimize I, we need to maximize the others while satisfying constraints:
- I + S ≥ 41
- I + L ≥ 41
- I + M ≥ 41
- S + L ≥ 41
- S + M ≥ 41
- L + M ≥ 41

If I = 12, then S, L, M must each be ≥ 29 (to satisfy I + X ≥ 41)
- Let S = L = M = 29.33... (approximately)
- Check: 12 + 29 + 29 + 30 = 100 ✓
- All pairs: 12+29=41 ✓, 12+30=42 ✓, 29+29=58 ✓, etc.

Answer: **12**

**Technique**: Constraint optimization, algebraic reasoning

---

### 2. Probability Problem (Probability Theory)
**Question**: Three droids need to choose a leader. Only two of them are suitable for the function. However, droids have no idea about politics and they will vote randomly. What is the chance (%) that the same candidate gets all the votes?

**Solution**: **25%**

**Method**:
Let's call the two suitable candidates A and B, and assume there's a third unsuitable candidate C (or they just vote for A or B).

Since only 2 are suitable, each droid randomly picks from {A, B}:
- Total possible outcomes: 2³ = 8
  - AAA, AAB, ABA, ABB, BAA, BAB, BBA, BBB

- Unanimous votes (all same): AAA or BBB = 2 outcomes
- Probability = 2/8 = 1/4 = 25%

Answer: **25**

**Technique**: Combinatorial probability, counting outcomes

---

### 3. Name Riddle (Logic Puzzle)
**Question**: Odette's mother has five daughters: Mag, Meg, Mig, Mog. What is the name of the fifth daughter?

**Solution**: **Odette**

**Method**:
Classic trick question - the puzzle states "Odette's mother has five daughters"
- Daughter 1: Mag
- Daughter 2: Meg
- Daughter 3: Mig
- Daughter 4: Mog
- Daughter 5: Odette (stated at the beginning!)

The pattern Mag, Meg, Mig, Mog, Mug is a red herring.

Answer: **Odette**

**Technique**: Reading comprehension, logic, avoiding misdirection

---

### 4-5. Additional Puzzles
The solution includes **%** and **0x00000000000000000000000000000000000000000e** which suggests:
- A percentage symbol separator
- A hexadecimal value: 0x0e (14 in decimal) padded with zeros
- The hex format suggests blockchain/Ethereum address style formatting

---

## Solution Format
```
12 + 25 + % + Odette + 0x00000000000000000000000000000000000000000e
= 1225%Odette0x00000000000000000000000000000000000000000e
```

**No spaces** - all components concatenated directly

---

## Techniques Used
1. **Constraint Optimization** - Finding minimum values under multiple constraints
2. **Probability Calculation** - Combinatorial analysis of random events
3. **Logic Puzzles** - Reading comprehension and avoiding trick questions
4. **Hexadecimal Notation** - Understanding blockchain-style hex formatting
5. **Format Concatenation** - Combining different data types (numbers, text, hex)

## Difficulty Assessment
Medium - The individual puzzles are not overly complex, but the solution format with no spaces and mixed data types (decimal, text, hex) adds complexity. The 5.5 month gap between announcement and solution suggests moderate difficulty.

## Key Learning Points
- Solution format can be as important as solving the puzzles
- Mix of mathematical, logical, and technical knowledge required
- Hexadecimal padding suggests blockchain/technical context
- No spaces in solution = precise format matching required
- "Trick questions" test careful reading, not just computation

## Notes
The presence of hexadecimal notation with Ethereum-style 0x prefix suggests this puzzle may have had a blockchain/cryptocurrency technical component beyond pure logic puzzles.
