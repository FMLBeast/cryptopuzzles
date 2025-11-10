# Bitcoin Puzzle #135 - Unsolved High-Value Target

## Overview

**Prize:** 13.5 BTC (~$350,000 at current prices)
**Difficulty:** 135 bits (brute force) → ~67.5 bits effective (with Kangaroo)
**Status:** UNSOLVED (as of November 2025)
**Technique Required:** Pollard's Kangaroo Algorithm
**Special Feature:** **Public key exposed** via outgoing transaction

## Why This Puzzle is Special

Puzzle #135 is one of the "every 5th" puzzles where the creator made a small outgoing transaction, which exposed the public key on the blockchain. This exposure is **critical** because it enables the use of Pollard's Kangaroo algorithm instead of brute force.

**The Game Changer:**
- **Brute Force:** 2^135 operations (~4.3 × 10^40) → **IMPOSSIBLE**
- **Pollard's Kangaroo:** √(2^135) = 2^67.5 operations (~2.1 × 10^20) → **CHALLENGING BUT FEASIBLE**

This reduces the computational complexity by the square root—a difference between impossible and theoretically solvable with sufficient resources.

## Challenge Specifications

### Address and Keys

```
Address: 1MVDYgVaBtp8yL4FHcfY9dvQ1aWpTfJQBU
Balance: 13.5 BTC

Public Key: (exposed via blockchain transaction)
  - Available from blockchain explorers
  - Revealed through outgoing transaction made by puzzle creator
  - Enables ECDLP-based attacks

Private Key Range: [2^134, 2^135 - 1]
  Minimum: 21,778,071,482,940,061,661,655,974,875,633,165,533,184
  Maximum: 43,556,142,965,880,123,323,311,949,751,266,331,066,367
```

### Search Space Analysis

**Brute Force (Without Public Key):**
```
Search Space: 2^134 keys
Decimal: 2.18 × 10^40 keys
Estimated Time (10,000 RTX 4090s @ 2,500 MKey/s each):
  = 2.18 × 10^40 / (2 × 10,000 × 2.5 × 10^9)
  = 4.36 × 10^26 seconds
  = 1.38 × 10^19 years
  (13.8 billion times the age of the universe!)
```

**Pollard's Kangaroo (With Public Key):**
```
Effective Search: √(2^135) = 2^67.5 operations
Decimal: ~2.1 × 10^20 operations

With optimized Kangaroo implementation:
  - Single GPU (RTX 4090): ~100-200 Mop/s (millions of operations/sec)
  - 1,000 GPUs: ~150,000 Mop/s = 1.5 × 10^11 op/s

Estimated Time (1,000 GPUs):
  = 2.1 × 10^20 / (1.5 × 10^11)
  = 1.4 × 10^9 seconds
  = ~44 years

With 10,000 GPUs: ~4.4 years
With 100,000 GPUs: ~160 days
```

## Mathematical Foundation

### The Elliptic Curve Discrete Logarithm Problem (ECDLP)

Given:
- Elliptic curve: secp256k1 (Bitcoin's curve)
- Generator point: G
- Public key: Q
- Known range: k ∈ [a, b] where a = 2^134, b = 2^135 - 1

Find: Private key k such that Q = k · G

**Without public key Q:** Must try every k and check if k·G produces the target address
**With public key Q:** Can solve ECDLP using Pollard's Kangaroo

### Pollard's Kangaroo Algorithm

Pollard's Kangaroo solves ECDLP in O(√N) time where N is the range size.

**The Metaphor:**
- **Tame Kangaroo:** Starts from known point a·G, makes pseudo-random jumps
- **Wild Kangaroo:** Starts from target Q, makes same pseudo-random jumps
- **Collision:** When kangaroos meet, we can compute the discrete log

**Algorithm Overview:**

```
1. Define jumping function f(P):
   - Based on some bits of P, return a jump size
   - Must be deterministic (same P → same jump)
   - Average jump size ≈ √N

2. Tame Kangaroo:
   T = a·G  (start from beginning of range)
   For i = 1 to ∞:
     T = T + f(T)·G
     Store (T, total_distance) in hash table

3. Wild Kangaroo:
   W = Q  (start from target)
   For j = 1 to ∞:
     W = W + f(W)·G
     Check if W in hash table
     If found: compute k from collision

4. When T and W collide:
   They're at the same point P
   T = (a + d_tame)·G
   W = Q + d_wild·G = k·G + d_wild·G
   Therefore: k = a + d_tame - d_wild
```

**Expected Collisions:**
After ~2√N steps total (split between tame and wild), kangaroos collide.

### Distinguished Points Optimization

To reduce memory, only store "distinguished points"—points with specific properties (e.g., first k bits are zero).

```
Instead of storing every point:
1. Only store points where hash(point) starts with zeros
2. Tame and wild continue until hitting distinguished point
3. Check for collision in distinguished point table

Memory reduction: 1000× or more
Trade-off: Slightly more operations
```

## Technical Implementation

### Tool: Kangaroo by JeanLucPons

The most popular implementation for Bitcoin puzzle solving.

**Installation:**
```bash
git clone https://github.com/JeanLucPons/Kangaroo.git
cd Kangaroo
make
```

**Usage for Puzzle #135:**
```bash
./kangaroo \
  -t 8 \                           # CPU threads
  -d 0,1 \                         # GPU devices
  -w work.txt \                    # Work file (for checkpointing)
  -wi 60 \                         # Work file save interval (seconds)
  -o found.txt \                   # Output file for solution
  -rangemin 15555555555555555555555555555555555 \  # 2^134 in hex
  -rangemax 2aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa \  # 2^135-1 in hex
  puzzle135_pubkey.txt             # File with public key
```

**Public Key File Format (`puzzle135_pubkey.txt`):**
```
# Puzzle #135 public key (get from blockchain)
02[x-coordinate]  # or 03 for odd y
```

To get the public key:
1. Find the outgoing transaction from address `1MVDYgVaBtp8yL4FHcfY9dvQ1aWpTfJQBU`
2. Extract the scriptSig (contains public key for standard transactions)
3. Format as compressed public key (33 bytes: prefix + x-coordinate)

### Performance Optimization

**GPU Selection:**
Kangaroo benefits from high memory bandwidth:
- **RTX 3090:** ~150 Mop/s per GPU
- **RTX 4090:** ~200 Mop/s per GPU
- **A100:** ~250 Mop/s per GPU

**Parameters to Tune:**
1. **Distinguished Point Bits:** Balance memory vs operations
2. **Jump Function:** Quality affects collision rate
3. **GPU Count:** Near-linear scaling
4. **CPU Threads:** For distinguished point checking

### Distributed Kangaroo

**Challenge:** Unlike brute force, Kangaroo is trickier to distribute because both kangaroos need access to the same collision table.

**Solutions:**

**Approach 1: Client-Server Architecture**
```
Central Server:
  - Maintains distinguished point database
  - Receives distinguished points from clients
  - Checks for collisions
  - Alerts on solution found

Clients (Many GPUs):
  - Generate tame or wild kangaroos
  - Jump until hitting distinguished point
  - Report distinguished point to server
  - Continue from new random starting point
```

**Approach 2: Hybrid Search**
```
Split the 2^135 range into sub-ranges:
- Range 1: [2^134, 2^134 + 2^127]
- Range 2: [2^134 + 2^127, 2^134 + 2*2^127]
- ...

Run independent Kangaroo on each sub-range
Disadvantage: Loses some sqrt efficiency
Advantage: Easier coordination
```

## Feasibility Analysis

### Economic Viability

**Prize Value:**
- 13.5 BTC × $26,000 = $351,000 (at BTC=$26k)
- 13.5 BTC × $100,000 = $1,350,000 (if BTC reaches $100k)

**Cost Estimates (Using AWS p3.16xlarge with 8x V100):**
- Cost: ~$24/hour for 8 GPUs
- Performance: ~800 Mop/s total
- Expected time: 2.1×10^20 / 8×10^8 = 2.6×10^11 seconds = 8,300 years
- **Single instance: NOT VIABLE**

**Cost Estimates (1,000 Optimized GPUs):**
- Rental cost: ~$0.50/hour per GPU
- Total: $500/hour
- Expected time: ~44 years
- Total cost: 44 × 365 × 24 × $500 = $192,720,000
- **Not economically viable at current BTC prices**

**Cost Estimates (10,000 GPUs for 4.4 years):**
- Total: $5,000/hour
- Expected time: ~4.4 years
- Total cost: 4.4 × 365 × 24 × $5,000 = $192,720,000
- **Still not economically viable**

### Why Hasn't It Been Solved?

Despite theoretical feasibility, several factors prevent solution:

1. **Massive Capital Required:** $50M-$200M in GPU costs
2. **Coordination Complexity:** Managing 10,000+ GPUs
3. **Long Time Horizon:** Multi-year commitment
4. **Mempool Risk:** Solution could be stolen
5. **Competition Risk:** Multiple parties might compete
6. **Opportunity Cost:** Capital could earn more elsewhere
7. **Implementation Risk:** Bugs could waste months of computation

### Potential Game Changers

**Scenario 1: Bitcoin Price Surge**
- If BTC reaches $500,000: Prize = $6.75M
- Makes 1,000 GPU cluster viable for 5 years
- Expected profit: $6.75M - $200M = Still negative!
- Need BTC > $15M for break-even

**Scenario 2: GPU Performance Breakthrough**
- 100× faster Kangaroo implementation: 44 years → 160 days
- Cost with 1,000 GPUs: $192k
- **PROFITABLE at current prices!**
- Requires algorithmic or hardware breakthrough

**Scenario 3: Distributed Volunteer Network**
- Community coordinates 10,000+ volunteer GPUs
- Zero rental cost (only electricity)
- Time: ~4.4 years
- Profit: Split among participants
- **VIABLE if coordination solved**

**Scenario 4: Quantum Computing**
- Shor's algorithm: Polynomial time ECDLP
- Would solve instantly
- Timeline: 10-30 years for practical quantum computers

## Comparison with Other Unsolved Puzzles

| Puzzle | BTC | Bits | Public Key? | Kangaroo Feasible? | Est. Time (1k GPUs) |
|--------|-----|------|-------------|-------------------|-------------------|
| #71    | 7.1 | 71  | ❌ No        | ❌ No              | Impossible        |
| #75    | 7.5 | 75  | ✅ Yes       | ✅ Maybe           | Months-Years      |
| #80    | 8.0 | 80  | ✅ Yes       | ✅ Maybe           | Years             |
| #130   | 13.0| 130 | ✅ Yes       | ⚠️ Challenging     | Decades           |
| #135   | 13.5| 135 | ✅ Yes       | ⚠️ Very Hard       | Decades           |
| #140   | 14.0| 140 | ✅ Yes       | ❌ Infeasible      | Centuries         |

**Strategic Priority:**
Most efficient to target **Puzzle #75 or #80** first:
- Lower difficulty
- Similar Kangaroo advantage
- More reasonable time horizon (months-years vs decades)

## Alternative Attack Vectors

### 1. Weak RNG Hypothesis

If the puzzle creator used a weak random number generator, keys might have patterns.

**Investigations:**
- Check if keys follow linear congruential generator
- Look for low Hamming weight (few 1 bits)
- Test common "random" seeds

**Verdict:** Unlikely; puzzles #1-125 showed no pattern

### 2. Side-Channel Analysis

Could there be additional information on the blockchain?

**Investigations:**
- Transaction timing analysis
- Signature nonce analysis (k value in ECDSA)
- Relationship between puzzles

**Verdict:** No exploitable side-channels found

### 3. Mathematical Breakthrough

Novel algorithm better than Kangaroo?

**Theoretical Limits:**
- Generic ECDLP: Ω(√N) lower bound proven
- Specific to secp256k1: No known weaknesses
- Quantum: Shor's algorithm (exponential speedup)

**Verdict:** Unlikely without quantum computers

## Community Efforts

### Current Status

As of November 2025, no organized effort to solve puzzle #135:
- Too expensive for individuals
- Too risky for companies
- No volunteer coordination

### What Would It Take?

**Option 1: Well-Funded Organization**
- $50M-$200M budget
- 5-10 year timeline
- Expert cryptography team
- Custom hardware/software

**Option 2: Decentralized Pool**
- 10,000+ volunteers contribute GPU time
- Central coordination server
- Reward split proportionally
- Challenges: Trust, coordination, long timeline

**Option 3: Wait for Technology**
- GPU performance improves 10-100×
- Bitcoin price increases 10-100×
- Quantum computers become available

## Conclusion

Bitcoin Puzzle #135 represents the frontier of what's theoretically possible with current cryptographic attacks. While the exposed public key reduces the problem from impossible to merely extremely hard, the computational resources required (decades of GPU time on thousands of GPUs) make it economically infeasible at current Bitcoin prices.

The puzzle demonstrates:
1. **Power of Public Key Exposure:** Turns 2^135 → 2^67.5 effective difficulty
2. **Limits of Pollard's Kangaroo:** Even with √N advantage, still requires massive resources
3. **Economic Barrier:** Prize must exceed computational cost
4. **Security of ECDSA:** Properly-sized keys (135+ bits) are secure against current attacks

**Strategic Recommendation:** Focus efforts on lower puzzles (#75, #80) where Kangaroo is more practical, or wait for technological advances (better GPUs, quantum computers) or price increases (BTC > $100k) to make #135 viable.

The real value of studying puzzle #135 isn't in solving it, but in understanding the mathematical elegance of Pollard's Kangaroo and the exponential security guarantees of elliptic curve cryptography.

---

**References:**
- Puzzle #135 Address: `1MVDYgVaBtp8yL4FHcfY9dvQ1aWpTfJQBU`
- Kangaroo Implementation: https://github.com/JeanLucPons/Kangaroo
- Pollard's Original Paper: "Monte Carlo Methods for Index Computation (mod p)" (1978)
- secp256k1 Specification: SEC 2 v2.0
