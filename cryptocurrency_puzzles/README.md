# Cryptocurrency Private Key Hunting Puzzles Collection

## Overview

This collection documents cryptocurrency private key hunting puzzles, challenges, and cryptographic treasure hunts from 2009-2025. These puzzles range from mathematical challenges to real-world scavenger hunts with substantial cryptocurrency bounties.

**Collection Statistics:**
- **Total Bitcoin Puzzle Keys:** 160 (79 solved, 81 unsolved)
- **Total Prize Value:** ~969+ BTC (~$25M+) still available
- **Time Period:** 2009-2025
- **Primary Categories:** 5
- **Documented Techniques:** 8
- **Active Bounties:** Multiple puzzles with 6-32 BTC rewards

## Major Puzzle Categories

### 1. Bitcoin Puzzle Transaction (2015-Present)

The most famous cryptocurrency puzzle, created in 2015 with ~1000 BTC distributed across 160 addresses with progressively harder private keys.

**Status:** 79/160 solved (as of 2025)
**Remaining Value:** ~969 BTC (~$25M+)
**Difficulty Range:** 1-160 bits
**Technique:** Sequential brute force, Pollard's Kangaroo for exposed keys

**Recent Solves:**
- Puzzle #69 (6.9 BTC) - Solved April 30, 2025
- Puzzle #68 (6.8 BTC) - Solved April 6, 2025
- Puzzle #67 (6.7 BTC) - Solved February 21, 2025
- Puzzle #66 (6.6 BTC) - Solved September 12, 2024

**Key Pattern:**
Private keys are sequential powers of 2 with decreasing known bits:
- Puzzle #1: Key in range [1, 2^1] → 1 bit
- Puzzle #2: Key in range [2^1, 2^2] → 2 bits
- Puzzle #N: Key in range [2^(N-1), 2^N] → N bits

**Solved Puzzles:** 1-65, 70, 75, 80, 85, 90, 95, 100, 105, 110, 115, 120, 125
**Hardest Solved:** Puzzle #125 (125-bit search space)
**Next Targets:** #66, #71, #76 (71-76 bit difficulty)

**Special Puzzles - Exposed Public Keys:**
Every 5th puzzle (70, 75, 80, 85, 90, 95, 100, 105, 110, 115, 120, 125, 130, 135, ...) had small outgoing transactions that exposed their public keys. This enables Pollard's Kangaroo algorithm with √N complexity instead of N.

**Active High-Value Targets:**
- Puzzle #135: 13.5 BTC, 135-bit range, **public key exposed** → Can use Kangaroo (~2^67.5 operations vs 2^135)
- Puzzle #130: 13.0 BTC, 130-bit range, **public key exposed** → Can use Kangaroo (~2^65 operations)

### 2. Brain Wallet Vulnerabilities (2009-Present)

Brain wallets allowed users to derive Bitcoin addresses from memorable passphrases. This created a massive attack surface for dictionary and rainbow table attacks.

**Status:** Thousands compromised
**Technique:** Dictionary attacks, rainbow tables, brute force
**Tool:** Brainflayer (DEFCON 23)
**Success Rate:** 18,000+ wallets cracked

**Attack Vectors:**
1. **Dictionary Attacks:** Common phrases, book quotes, song lyrics
2. **Pattern-Based:** Keyboard patterns, dates, names
3. **Rainbow Tables:** Pre-computed hash tables
4. **Hybrid Attacks:** Dictionary + mutations

**Notable Statistics:**
- Ryan Castellucci checked 1 trillion passwords for $55.86 in compute costs
- Recovered 18,000+ brain wallets
- Weak passphrases compromised within seconds
- Even "complex" human-memorable phrases are vulnerable

### 3. Satoshi's Treasure (2019-2020)

A $1M Bitcoin treasure hunt using Shamir's Secret Sharing, combining online and physical challenges.

**Status:** Unsolved (ended early in 2020)
**Prize:** $1M in Bitcoin (still in wallet)
**Technique:** Shamir's Secret Sharing (400 of 1000 fragments needed)
**Format:** Online puzzles (70-80%) + Physical locations (20-30%)

**How It Worked:**
- Private key split into 1,000 fragments using Shamir's algorithm
- Need 400 fragments to reconstruct the key
- Fragments hidden globally in digital and physical locations
- Early keys obtained through cryptographic exploits, QR codes, puzzles

**Notable Events:**
- Developer John Cantrell obtained first 3 keys in minutes by exploiting website weaknesses
- Game ended early after death of co-creator Adam Dupré
- Remaining funds returned to investors
- **Bitcoin still locked in wallet - treasure never claimed**

### 4. 310 BTC Visual Puzzle (2018)

A steganography challenge hiding recovery codes for 4 wallets in a single black-and-white image.

**Status:** Partially solved (some wallets claimed)
**Prize:** 310.61 BTC total (~$8M at time)
**Technique:** Visual steganography, pattern recognition
**Format:** Single image with embedded clues

### 5. CryptoHack & Educational Platforms

Modern educational platforms with progressive difficulty challenges.

**Platforms:**
- **CryptoHack:** Web-based cryptography challenges (Introduction → RSA → ECC → Misc)
- **Cryptopals:** 8 sets of real-world crypto challenges
- **Codex Protocol:** Puzzle bounties with cryptocurrency rewards

## Technique Taxonomy

### 1. Brute Force Search

**Complexity:** O(2^n) for n-bit keys
**Tools:** BitCrack, KeyHunt
**Application:** Bitcoin Puzzle #1-65
**Hardware:** GPU (CUDA/OpenCL), ASIC

**Performance Benchmarks:**
- GeForce GTX 1650: 305 MKey/s
- RTX 3090: ~1,500 MKey/s
- Top-end mining rig: ~10,000 MKey/s

**Optimization Parameters:**
- Blocks: Multiple of compute units (default: 32)
- Threads per block: Multiple of 32 (default: 256)
- Keys per thread: Asymptotic performance increase

**Estimated Solve Times (single GPU):**
- 40-bit: Minutes
- 50-bit: Hours
- 60-bit: Weeks
- 66-bit: Months
- 70-bit: Years
- 80-bit: Decades

### 2. Pollard's Kangaroo Algorithm

**Complexity:** O(√N) for known range with public key
**Tools:** JeanLucPons/Kangaroo
**Application:** Bitcoin Puzzle #70, #75, #80+  (exposed public keys)
**Requirement:** Known public key + known range

**Algorithm Overview:**
Solves the Elliptic Curve Discrete Logarithm Problem (ECDLP) for secp256k1:
- Given public key Q and generator G
- Find k such that Q = k·G where k ∈ [a, b]
- Complexity: O(√(b-a)) instead of O(b-a)

**Practical Example:**
- Puzzle #135: 135-bit range (2^134 to 2^135-1)
- Brute force: 2^135 operations (~impossible)
- Kangaroo with exposed pubkey: √(2^135) = 2^67.5 operations (~feasible with distributed effort)

**Implementation Notes:**
- Tame kangaroo: Starts from known point, makes deterministic jumps
- Wild kangaroo: Starts from target, makes same deterministic jumps
- Collision detection: When kangaroos meet, discrete log can be computed
- Memory requirement: Hash table for collision detection

### 3. Dictionary & Rainbow Table Attacks

**Complexity:** O(n) for n dictionary entries
**Tools:** Brainflayer, custom scripts
**Application:** Brain wallets, weak passphrases
**Success Rate:** 95%+ for common phrases

**Dictionary Sources:**
1. **Common passwords:** rockyou.txt, leaked databases
2. **Literature:** Books, poems, quotes (Gutenberg Project)
3. **Song lyrics:** Popular songs database
4. **Historical phrases:** Famous speeches, movie quotes
5. **Pattern-based:** Keyboard walks, repeated characters
6. **Hybrid:** Mutations, leetspeak, appended numbers

**Attack Process:**
```
For each passphrase in dictionary:
    1. Compute SHA-256 hash
    2. Derive private key (brain wallet formula)
    3. Compute public key (secp256k1)
    4. Compute Bitcoin address
    5. Check against bloom filter of funded addresses
    6. If match → Extract funds
```

**Performance:**
- Brainflayer: Optimized with libsecp256k1
- Check 1 trillion passphrases: ~$55 compute cost (2015)
- Modern hardware: 10-100x faster

### 4. Cryptanalysis & Mathematical Approaches

**Application:** Structured puzzles with mathematical clues
**Techniques:**
- Modular arithmetic
- Number theory (prime factorization, discrete log)
- Constraint satisfaction
- Pattern recognition

### 5. Steganography & Visual Analysis

**Application:** 310 BTC puzzle, Satoshi's Treasure
**Techniques:**
- LSB extraction
- Alpha channel analysis
- Frequency analysis
- QR code detection
- OCR for embedded text

### 6. Baby-Step Giant-Step (BSGS)

**Complexity:** O(√N) space and time
**Application:** Alternative to Kangaroo for small ranges
**Requirement:** Known public key

**Algorithm:**
- Compute "baby steps": Store G, 2G, 3G, ..., mG
- Compute "giant steps": Check Q, Q-mG, Q-2mG, ...
- Find collision between sets
- Memory intensive but deterministic

### 7. Distributed Computing

**Application:** Large-scale puzzle solving
**Approach:** Split search space across many machines
**Tools:** Custom pooled clients, Bitcoin Puzzle Worker

**Coordination:**
- Central server assigns ranges
- Clients report progress
- Collision/solution reporting
- Redundancy handling

### 8. Side-Channel & Implementation Attacks

**Application:** Weak implementations, exposed nonces
**Techniques:**
- Nonce reuse detection
- Timing attacks
- Weak RNG exploitation
- API/website vulnerabilities

## Tool Ecosystem

### Primary Tools

#### BitCrack
**Purpose:** GPU-accelerated Bitcoin private key brute-forcing
**Platform:** CUDA (cuBitCrack) and OpenCL (clBitCrack - experimental)
**Performance:** 100-10,000 MKey/s depending on GPU
**Best For:** Sequential search of known ranges (Puzzle #1-65)

**Features:**
- Multi-GPU support
- Customizable search patterns
- Checkpoint/resume capability
- Bloom filter integration for quick checks

**Usage Example:**
```bash
./cuBitCrack -b 32 -t 256 -p 256 \
  -o found.txt \
  --keyspace 2000000000000000:3ffffffffffffffff \
  1PXH6JaoZAu49bYHmT2whzg7o9f24e8H5z
```

#### KeyHunt
**Purpose:** Pattern-based private key discovery
**Algorithms:** BSGS, Kangaroo, Brute Force
**Best For:** Puzzles with exposed public keys (#70, #75, #80+)

**Features:**
- Multiple algorithm support
- Public key ECDLP solving
- Memory-efficient BSGS
- Vanity address generation

#### Kangaroo (JeanLucPons)
**Purpose:** Pollard's Kangaroo for ECDLP on secp256k1
**Complexity:** O(√N) for N-sized range
**Best For:** Exposed public key puzzles
**Limitation:** 125-bit interval search maximum

**Features:**
- Optimized secp256k1 operations
- Work file save/resume
- Distinguished points collision detection
- Distributed solving support

#### Brainflayer
**Purpose:** Brain wallet cracking
**Performance:** Optimized with libsecp256k1 (4x faster than original)
**Best For:** Dictionary attacks on weak passphrases

**Attack Modes:**
- Dictionary mode: Direct passphrase testing
- Brute force: Sequential exhaustive search
- Hybrid: Dictionary + mutations

**Bloom Filter Optimization:**
Uses bloom filters of funded addresses for O(1) lookup:
```bash
# Generate bloom filter from blockchain
./hex2blf.py addresses.txt > addresses.blf

# Run dictionary attack
./brainflayer -v -b addresses.blf -i dictionary.txt
```

### Supporting Tools

- **exiftool:** Metadata extraction from puzzle images
- **stegsolve:** Visual steganography analysis
- **zxing:** QR code detection and decoding
- **hashcat:** GPU-accelerated hash cracking (for hash-based puzzles)
- **Bitcoin Core:** Address balance checking, transaction analysis
- **Python libraries:** ecdsa, hashlib, secp256k1

## Difficulty Progression

### Trivial (1-40 bits)
**Solve Time:** Seconds to minutes
**Method:** Basic brute force
**Skills:** Basic scripting, command-line tools
**Examples:** Bitcoin Puzzle #1-40

### Easy (41-50 bits)
**Solve Time:** Hours to days
**Method:** GPU brute force
**Skills:** GPU programming, optimization
**Examples:** Bitcoin Puzzle #41-50

### Medium (51-65 bits)
**Solve Time:** Days to months
**Method:** Optimized GPU, distributed computing
**Skills:** Parallel programming, distributed systems
**Examples:** Bitcoin Puzzle #51-65

### Hard (66-80 bits)
**Solve Time:** Months to years
**Method:** Advanced GPU clusters, ASIC (future)
**Skills:** Cryptography, hardware optimization
**Examples:** Bitcoin Puzzle #66-69 (recently solved)

### Very Hard (81-125 bits with public key)
**Solve Time:** Years to decades (with Kangaroo)
**Method:** Pollard's Kangaroo with distributed effort
**Skills:** Advanced cryptography, algorithm optimization
**Examples:** Bitcoin Puzzle #135 (public key exposed)

### Infeasible (126+ bits without public key)
**Solve Time:** Beyond current computational capability
**Method:** Theoretical only
**Skills:** Research-level cryptography
**Examples:** Bitcoin Puzzle #126-160 (without public keys)

## Solved Puzzles Highlights

### Bitcoin Puzzle #66 (6.6 BTC) - September 2024
**Difficulty:** 66 bits (2^65 to 2^66-1)
**Search Space:** 36,893,488,147,419,103,232 keys
**Technique:** GPU brute force with BitCrack
**Estimated Effort:** Months of distributed GPU time
**Notable:** First major solve in years, reignited interest

**Private Key:** `0x2832ed74f2b5e35e` (hex)

### Bitcoin Puzzle #69 (6.9 BTC) - April 2025
**Difficulty:** 69 bits
**Search Space:** ~295 quintillion keys
**Solve Time:** <1 month
**Technique:** Advanced GPU cluster
**Transaction:** Bypassed public mempool to avoid interception

### Brain Wallet - "correct horse battery staple"
**Balance:** 0.1 BTC (drained within hours of funding)
**Passphrase:** Famous XKCD comic phrase
**Attack:** Dictionary attack with Brainflayer
**Time to Crack:** <1 second after funding

### Brain Wallet - Bitcoin Whitepaper First Line
**Passphrase:** "Bitcoin: A Peer-to-Peer Electronic Cash System"
**Status:** Compromised immediately
**Lesson:** Even long, unique phrases are in crackers' dictionaries

## Unsolved High-Value Puzzles

### Bitcoin Puzzle #130 (13.0 BTC) - Public Key Exposed
**Difficulty:** 130 bits → ~2^65 with Kangaroo
**Search Space:** 1.3 × 10^39 keys (brute force) or ~3.7 × 10^19 (Kangaroo)
**Estimated Effort:** Feasible with large distributed Kangaroo implementation
**Address:** `13zb1hQAB5xDTfASsGhUDSPe2GsuECxb2T`

**Public Key (exposed):** Available due to outgoing transaction
**Kangaroo Feasibility:** With 1,000 GPUs → several years

### Bitcoin Puzzle #135 (13.5 BTC) - Public Key Exposed
**Difficulty:** 135 bits → ~2^67.5 with Kangaroo
**Search Space:** 4.3 × 10^40 keys (brute force) or ~2.1 × 10^20 (Kangaroo)
**Estimated Effort:** Challenging but theoretically feasible
**Address:** `1MVDYgVaBtp8yL4FHcfY9dvQ1aWpTfJQBU`

### Bitcoin Puzzle #71-160 (No Public Key)
**Difficulty:** 71-160 bits
**Total Value:** 710+ BTC
**Method Required:** Pure brute force (no Kangaroo possible)
**Feasibility:** #71-75 possible with massive GPU clusters, #76+ currently infeasible

### Satoshi's Treasure ($1M)
**Prize:** ~$1,000,000 in Bitcoin
**Status:** Game ended, but **Bitcoin never claimed** (still in wallet!)
**Fragments Found:** Unknown (game ended at ~150-200 keys found)
**Required:** 400 of 1,000 Shamir fragments
**Feasibility:** Without additional keys being released, currently impossible

## Learning Path

### Beginner: Puzzle Basics
**Goal:** Understand cryptocurrency puzzle mechanics
**Time:** 1-2 weeks

**Topics:**
- Bitcoin addresses and private keys
- Public key cryptography basics
- ECDSA and secp256k1 curve
- Address derivation from private keys
- Using Bitcoin Core for balance checking

**Projects:**
- Generate random private keys and check balances
- Solve Bitcoin Puzzle #1-10 (1-10 bits)
- Write simple brute force script in Python

### Intermediate: GPU Acceleration
**Goal:** Implement efficient GPU-based solvers
**Time:** 1-3 months

**Topics:**
- CUDA/OpenCL programming
- GPU memory hierarchy
- Parallel algorithm design
- Optimization techniques (coalescing, occupancy)
- Using BitCrack effectively

**Projects:**
- Optimize BitCrack for your GPU
- Solve Bitcoin Puzzle #40-50
- Build custom GPU kernel for key generation

### Advanced: Cryptographic Algorithms
**Goal:** Understand and implement advanced algorithms
**Time:** 3-6 months

**Topics:**
- Elliptic Curve Discrete Logarithm Problem
- Pollard's Kangaroo algorithm
- Baby-Step Giant-Step
- Bloom filters and hash tables
- Distributed computing coordination

**Projects:**
- Implement Kangaroo from scratch
- Attack brain wallets with custom dictionaries
- Contribute to open-source tools

### Expert: Research & Innovation
**Goal:** Contribute novel techniques and optimizations
**Time:** 6+ months

**Topics:**
- Advanced number theory
- Cryptanalysis techniques
- Hardware optimization (FPGA, ASIC)
- Novel algorithm design
- Steganography and side-channels

**Projects:**
- Research hybrid Kangaroo/BSGS approaches
- Optimize algorithms for specific puzzles
- Solve Bitcoin Puzzle #70+ with exposed keys

## Common Pitfalls & Best Practices

### Pitfalls

1. **Mempool Sniping:** Solutions can be intercepted by bots monitoring mempool
   - **Mitigation:** Use private transaction relay, mining pool partnerships

2. **Incomplete Search Ranges:** Missing keys due to off-by-one errors
   - **Mitigation:** Careful range calculation, overlap between workers

3. **Weak Random Number Generators:** Predictable "random" searches
   - **Mitigation:** Use cryptographically secure RNG

4. **Inefficient Code:** Losing 10-100x performance
   - **Mitigation:** Profile code, optimize hot paths, use proven libraries

5. **Bloom Filter False Positives:** Wasting time on invalid matches
   - **Mitigation:** Two-stage verification (bloom filter + full check)

### Best Practices

1. **Start Small:** Solve easy puzzles to verify your setup
2. **Benchmark:** Know your hardware's realistic performance
3. **Save State:** Implement checkpointing for long searches
4. **Verify Independently:** Double-check solutions before broadcasting
5. **Collaborate:** Join communities, share techniques (not ranges!)
6. **Stay Updated:** Follow puzzle status, avoid wasted effort on solved puzzles
7. **Calculate Feasibility:** Don't waste resources on impossible targets
8. **Understand Math:** Know why algorithms work, don't just run tools

## Mathematical Foundations

### Private Key to Address Derivation

```
1. Private Key (k): Random 256-bit number, 1 to n-1 where n = secp256k1 order
2. Public Key (K): K = k × G (elliptic curve point multiplication)
   - G is the generator point of secp256k1
3. Public Key Hash: SHA-256(K), then RIPEMD-160
4. Bitcoin Address: Base58Check encoding with version byte
```

### Search Space Calculations

For puzzle #N with N-bit private key:
- **Range:** [2^(N-1), 2^N - 1]
- **Search Space:** 2^(N-1) possible keys
- **With M keys/sec:** Expected time = 2^(N-2) / M seconds

Example (Puzzle #70):
- Range: [2^69, 2^70 - 1]
- Search Space: 2^69 ≈ 5.9 × 10^20 keys
- At 1,000 MKey/s: 5.9 × 10^14 seconds ≈ 18.7 million years
- With 10,000 GPUs: ~1,870 years

**But with exposed public key + Kangaroo:**
- Complexity: √(2^69) = 2^34.5 ≈ 23 billion operations
- At 1,000 Mop/s: ~23,000 seconds ≈ 6.4 hours
- Realistic (with overheads): Days to weeks

### Pollard's Kangaroo Complexity

For ECDLP with public key Q, finding k where Q = k·G and k ∈ [a, b]:

**Expected operations:** ~ 2 × √(b - a)

**Memory:** O(√(b - a)) for distinguished points

**Parallelization:** Near-linear speedup (divide range)

## Economics & Incentive Analysis

### Cost-Benefit Analysis

**Example: Puzzle #70 (7.0 BTC, ~$180k)**

**Brute Force (infeasible):**
- 10,000 GPUs × $0.50/hour × 1,870 years = Impossible

**Kangaroo with Public Key (feasible):**
- 100 GPUs × $0.50/hour × 168 hours (1 week) = $8,400
- Net profit: $180,000 - $8,400 = $171,600 (ROI: 2,038%)

**Why unsolved?** Requires:
1. Advanced implementation of Kangaroo for secp256k1
2. Significant upfront GPU investment/rental
3. Risk of mempool sniping (solution stolen)
4. Competition from other solvers

### Mempool Protection Value

Recent solves used private mining pool partnerships to bypass mempool:
- Cost: 1-5% of reward to mining pool
- Benefit: 100% security against interception
- Example: 6.7 BTC reward × 3% fee = 0.2 BTC (~$5k) for guaranteed claim

## Security & Ethical Considerations

### Responsible Disclosure

- **Puzzle Challenges:** Fair game, creator intended them to be solved
- **Bug Bounties:** Follow responsible disclosure guidelines
- **Live Wallets:** NEVER attack wallets without explicit authorization
- **Sharing Techniques:** Educational sharing is encouraged

### Legal Considerations

- Solving intentional puzzles: ✅ Legal
- Cracking brain wallets with funds: ⚠️ Gray area (depends on jurisdiction)
- Attacking exchange wallets or personal wallets: ❌ Illegal (theft)
- Research and education: ✅ Legal with proper ethical boundaries

### Ethical Guidelines

1. Only target intentional puzzles and challenges
2. Don't attack wallets with identifiable owners
3. Share knowledge and techniques openly
4. Contribute tools and improvements to community
5. Respect creator intentions (e.g., Satoshi's Treasure ended)

## Resources & Community

### Documentation
- Bitcoin Developer Reference: https://developer.bitcoin.org/
- secp256k1 Specification: Standards for Efficient Cryptography (SEC 2)
- BIP32/39/44: HD wallets and seed phrases

### Tools & Code
- BitCrack: https://github.com/brichard19/BitCrack
- Kangaroo: https://github.com/JeanLucPons/Kangaroo
- Brainflayer: https://github.com/ryancdotorg/brainflayer
- KeyHunt: Various forks on GitHub

### Communities
- Bitcointalk.org: Bitcoin Puzzle thread
- Reddit: r/bitcoinpuzzles
- Discord: Various puzzle-solving groups
- GitHub: Open-source tool development

### Tracking Sites
- https://privatekeys.pw/puzzles/bitcoin-puzzle-tx
- https://btcpuzzle.info/
- https://secretscan.org/Bitcoin_puzzle
- https://mizogg.com/

## Conclusion

Cryptocurrency private key hunting represents a unique intersection of cryptography, computer science, economics, and puzzle-solving. From mathematical brain-teasers to massive GPU-powered brute force operations, these challenges push the boundaries of computational feasibility while teaching valuable lessons about cryptographic security.

The Bitcoin Puzzle Transaction remains one of the most compelling ongoing challenges, with ~969 BTC waiting for those who can crack increasingly difficult private keys. The exposed public keys on every 5th puzzle create an especially interesting dynamic where mathematical elegance (Pollard's Kangaroo) can overcome brute computational power.

Whether approaching these puzzles as educational exercises, competitive challenges, or potential financial rewards, they provide invaluable hands-on experience with elliptic curve cryptography, parallel computing, and cryptanalysis techniques that are fundamental to blockchain security.

**Remember:** These puzzles exist to be solved. The real treasure is the knowledge gained along the way.

---

*Collection maintained for AI training and educational purposes.*
*Last Updated: November 2025*
