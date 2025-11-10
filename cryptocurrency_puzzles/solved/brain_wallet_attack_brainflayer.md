# Brain Wallet Attacks with Brainflayer - Massive Success Story

## Overview

**Attack Tool:** Brainflayer
**Author:** Ryan Castellucci
**Release:** DEFCON 23 (August 2015)
**Wallets Cracked:** 18,000+
**Cost:** $55.86 for 1 trillion passphrase checks
**Success Rate:** 95%+ for common human-chosen phrases
**Total Value Recovered:** Significant (exact amounts private)

## What Are Brain Wallets?

Brain wallets allow users to generate Bitcoin private keys from memorable passphrases. The idea was to eliminate the need to store keys digitally—just remember your passphrase and regenerate the key anytime.

**The Process:**
```
1. User chooses passphrase: "correct horse battery staple"
2. Hash passphrase: SHA-256("correct horse battery staple")
3. Use hash as private key
4. Derive Bitcoin address from private key
```

**The Fatal Flaw:**
Human-chosen passphrases have **much lower entropy** than true random 256-bit keys, making them vulnerable to dictionary attacks.

### Entropy Comparison

**Random 256-bit key:**
```
Entropy: 256 bits
Possible keys: 2^256 ≈ 10^77
Infeasible to brute force
```

**Human passphrase ("correct horse battery staple"):**
```
Entropy: ~44 bits (generously)
  - 4 common English words
  - ~11 bits per word from ~2000 common words
  - 11 × 4 = 44 bits
Possible combinations: 2^44 ≈ 17.6 trillion
Feasible to exhaust with dictionary attack
```

**Weak passphrase ("password123"):**
```
Entropy: ~20 bits
  - Common password
  - In top 1000 passwords list
Cracked: < 1 second
```

## The DEFCON 23 Talk

### Ryan Castellucci's Revelation

On August 7, 2015, at DEFCON 23, security researcher Ryan Castellucci gave a presentation titled **"Why I'm Releasing a Brainwallet Cracker."**

**Key Findings:**
1. Checked 1 trillion passphrases for just $55.86 in compute costs
2. Recovered 18,000+ brain wallet addresses
3. Many wallets drained within seconds of receiving funds
4. Even "strong" passphrases from literature, songs, quotes were compromised

**The Demonstration:**
- Live demonstration showing instant compromise of newly-funded brain wallets
- Revealed that attackers had been monitoring the blockchain for years
- Wallets using famous quotes, book passages, song lyrics were all vulnerable

### Performance Metrics

**Original Brainflayer (DEFCON 23):**
- **Hash rate:** ~130,000 passphrases/second per CPU core
- **Optimization:** Used libsecp256k1 for fast secp256k1 operations
- **Bloom filter:** O(1) lookup for address existence

**Modern Brainflayer (optimized):**
- **Hash rate:** ~1,000,000+ passphrases/second per GPU
- **Speedup:** 4× faster than DEFCON release
- **Additional optimizations:** Nicolas Courtois & Guangyang Song (UCL)

## Technical Architecture

### Attack Pipeline

```
┌──────────────┐
│  Dictionary  │
│  (billions)  │
└──────┬───────┘
       │
       ▼
┌──────────────────┐
│  SHA-256 Hash    │  ← Passphrase to private key
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  secp256k1 ECDSA │  ← Private key to public key
│  (k × G)         │
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  SHA-256 +       │  ← Public key to address
│  RIPEMD-160      │
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│  Bloom Filter    │  ← O(1) check if funded
│  Check           │
└──────┬───────────┘
       │
       ▼
   ┌───┴────┐
   │  Hit!  │  ← Found funded wallet
   └────────┘
```

### Bloom Filter Optimization

**The Problem:**
Checking every generated address against the entire blockchain is slow.

**The Solution:**
Pre-build a **Bloom filter** containing all funded addresses.

**Bloom Filter Properties:**
- **Space-efficient:** ~1 bit per address (with false positive rate)
- **Fast lookup:** O(1) time
- **Trade-off:** Small false positive rate (acceptable)

**Implementation:**
```python
# Step 1: Build bloom filter from funded addresses
import pyblooming

bf = pyblooming.BloomFilter(capacity=100_000_000, error_rate=0.001)

# Add all funded addresses from blockchain
for address in funded_addresses:
    bf.add(address)

# Save bloom filter
bf.save('funded_addresses.bf')

# Step 2: Attack with bloom filter
for passphrase in dictionary:
    address = passphrase_to_address(passphrase)
    if address in bf:  # O(1) lookup
        # Verify (bloom filter may have false positive)
        if actually_funded(address):
            print(f"FOUND: {passphrase} → {address}")
```

### Dictionary Sources

Brainflayer attacks use massive dictionaries from various sources:

#### 1. Password Leaks
```
- RockYou: 14 million passwords
- LinkedIn breach: 117 million
- Collection #1: 773 million
- Have I Been Pwned: billions
```

#### 2. Literature
```
- Project Gutenberg: 60,000+ books
- Shakespeare complete works
- Bible (all translations)
- Famous poems, speeches
```

#### 3. Song Lyrics
```
- Top 10,000 songs lyrics
- Popular song databases
- Famous choruses
```

#### 4. Famous Quotes
```
- Movie quotes (IMDB)
- TV show quotes
- Politician speeches
- Internet memes
```

#### 5. Patterns
```
- Keyboard walks: qwerty, asdfgh, 1qaz2wsx
- Repeated characters: aaaaaa, 123123123
- Dates: birthdays, historical events
- Names + dates: john1990, alice1985
```

#### 6. Mutations
```
- Leetspeak: password → p4ssw0rd
- Capitalization: Password, PASSWORD
- Appended numbers: password1, password123
- Special characters: password!, p@ssword
```

**Total Dictionary Size:**
Modern attacks use 1 trillion to 100 trillion entries through combination and mutation.

## Famous Compromised Brain Wallets

### 1. "correct horse battery staple" (XKCD 936)

**Background:** XKCD comic #936 suggested using 4 random common words for strong passwords.

**The Trap:** Community created brain wallet with this exact phrase to demonstrate it would be instantly drained.

**Result:**
```
Passphrase: "correct horse battery staple"
Private Key: SHA-256(passphrase) =
  c4bbcb1fbec99d65bf59d85c8cb62ee2db963f0fe106f483d9afa73bd4e39a8a
Address: 1JwSSubhmg6iPtRjtyqhUYYH7bZg3Lfy1T
Status: Drained within hours of any funding
Attack Time: < 1 second after funding
```

**Lesson:** Even "random" word combinations from common word lists are in attacker dictionaries.

### 2. Bitcoin Whitepaper Opening

```
Passphrase: "Bitcoin: A Peer-to-Peer Electronic Cash System"
Status: Monitored and instantly drained
Attack Time: < 1 second
```

**Lesson:** Famous texts, especially crypto-related, are prime targets.

### 3. Shakespeare Quotes

```
Passphrase: "To be or not to be, that is the question"
Source: Hamlet, Act 3 Scene 1
Status: Compromised
Attack Time: < 1 second
```

**Lesson:** Classic literature is extensively cataloged in cracker dictionaries.

### 4. Song Lyrics - "Hey Jude"

```
Passphrase: "Hey Jude don't make it bad"
Source: The Beatles
Status: Compromised
Attack Time: < 1 second
```

**Lesson:** Popular song lyrics are included in specialized databases.

### 5. Religious Texts

```
Passphrase: "In the beginning God created the heavens and the earth"
Source: Genesis 1:1
Status: Compromised
Attack Time: < 1 second
```

**Lesson:** Religious texts in all translations are fully indexed.

### 6. "Satoshi Nakamoto"

```
Passphrase: "satoshi nakamoto"
Address: 1Hy3B6Fd5tLQdbzKVBCFSCpoC9BhVoLqqR
Status: Heavily monitored, any funds drained instantly
```

**Lesson:** Names, especially famous crypto figures, are obvious targets.

## Attack Implementation

### Brainflayer Installation

```bash
# Clone repository
git clone https://github.com/ryancdotorg/brainflayer.git
cd brainflayer

# Install dependencies
sudo apt-get install libssl-dev libgmp-dev build-essential

# Compile
make
```

### Building Bloom Filter

```bash
# Download funded addresses from blockchain
# (Various blockchain data providers offer this)

# Convert addresses to binary format
./hex2blf funded_addresses.txt > addresses.blf

# Bloom filter is ready
```

### Running Dictionary Attack

```bash
# Basic dictionary attack
./brainflayer -v -b addresses.blf -i dictionary.txt

# With mutator (leetspeak, capitals, etc.)
./brainflayer -v -b addresses.blf -m -i dictionary.txt

# Brute force (exhaustive)
./brainflayer -v -b addresses.blf -x 8  # 8-character search

# Output
Found! Passphrase: "correct horse battery staple"
       Private Key: c4bbcb1fbec99d65bf59d85c8cb62ee2db963f0fe106f483d9afa73bd4e39a8a
       Address: 1JwSSubhmg6iPtRjtyqhUYYH7bZg3Lfy1T
       Balance: 0.1 BTC
```

### Performance Optimization

**Single-threaded (1 CPU core @ 3 GHz):**
```
~130,000 passphrases/second
1 trillion passphrases: ~89 days
```

**Multi-threaded (32 cores):**
```
~4,000,000 passphrases/second
1 trillion passphrases: ~3 days
Cost (AWS c5.18xlarge): ~$10/hour × 72 hours = $720
```

**GPU-accelerated (custom CUDA):**
```
~100,000,000 passphrases/second per GPU
1 trillion passphrases: ~3 hours
Cost (single RTX 4090): ~$1/hour × 3 hours = $3
```

## Real-World Impact

### Timeline of Brain Wallet Attacks

**2011-2013: Early Days**
- Brain wallets promoted as secure and convenient
- First attacks begin but remain quiet
- Attackers drain wallets silently to avoid awareness

**2013-2015: Growing Problem**
- Security researchers warn about brain wallet vulnerabilities
- Blockchain analysis reveals thousands of compromised wallets
- Attackers become more sophisticated with larger dictionaries

**August 2015: DEFCON 23**
- Ryan Castellucci releases Brainflayer and research
- Public becomes widely aware of the danger
- Many users lose funds shortly after talk

**2015-Present: Death of Brain Wallets**
- Community consensus: brain wallets are insecure
- Wallet software removes brain wallet features
- Continuous monitoring by attackers ensures any new brain wallet is drained

### Estimated Total Losses

**Conservative Estimates:**
- 18,000+ wallets cracked by single researcher
- Estimated total loss: 100-1,000 BTC across all victims
- At $26,000/BTC: $2.6M - $26M total losses

**Reality Likely Higher:**
- Multiple independent attackers
- Many victims never report losses
- Ongoing attacks since 2011

### Defensive Response

**Bitcoin Core and Major Wallets:**
1. **Removed brain wallet features** from official releases
2. **Added warnings** about weak passphrases
3. **Enforced BIP39** (mnemonic seeds with proper entropy)
4. **Required randomness** from cryptographically secure RNG

**BIP39 Improvement:**
```
Brain Wallet (bad):
  - User chooses passphrase
  - Low entropy
  - Vulnerable to dictionary attacks

BIP39 Mnemonic (good):
  - Software generates 128-256 bits of entropy
  - Encodes as 12-24 words
  - Words are randomly selected
  - Even if attacker knows wordlist, 2^128 combinations
```

## Why Brain Wallets Fail

### Entropy Illusion

Humans think their passphrases are random, but they follow predictable patterns:

**User thinks:** "My passphrase is unique and strong"
```
"my daughter emma was born on june 5 1995"
```

**Attacker has:**
```
Dictionary: all names (emma, john, sarah, ...)
Dictionary: dates (june 5 1995, 06/05/1995, ...)
Pattern: [name] + [relation] + [date]
Combinations: millions (still feasible)
```

### The Birthday Paradox of Brain Wallets

**Collision Probability:**
With only ~4 billion possible passphrases in "good" space:
- After checking 65,536 passphrases: 50% chance of collision
- Reality: Most humans choose from ~100 million "reasonable" passphrases
- Most attackers can check all 100 million in hours

### Psychological Predictability

**Common Patterns:**
1. **Names:** Family, pets, celebrities (~100K possibilities)
2. **Dates:** Birthdays, anniversaries (~100 years × 365 days)
3. **Favorites:** Colors, foods, places (~10K possibilities)
4. **Combinations:** [Name][Date] = 100K × 36K = 3.6 billion (checkable in hours)

## Secure Alternatives

### BIP39 Mnemonic Seeds

**How it works:**
```
1. Generate 128-256 bits of cryptographic randomness
2. Encode as 12-24 words from fixed 2048-word list
3. Optional passphrase for additional security

Entropy: 128-256 bits (vs 20-44 bits for brain wallets)
Security: Resistant to dictionary attacks
```

**Example:**
```
witch collapse practice feed shame open despair creek road again
ice least
```
This represents 128 bits of true randomness, not human-chosen words.

### Deterministic Wallets (BIP32)

**Hierarchical Deterministic (HD) Wallets:**
```
Master Seed (256 bits) →
  Master Private Key →
    Child Key 1, Child Key 2, ...
```

**Advantages:**
- Single backup for infinite keys
- Proper entropy from RNG
- Cannot be dictionary attacked

## Lessons for Cryptopuzzle Solvers

### Attack Methodology

Brainflayer's success provides a template for attacking other puzzles:

1. **Identify Low-Entropy Targets**
   - Brain wallets (proven vulnerable)
   - Weak RNG implementations
   - Human-chosen seeds

2. **Build Comprehensive Dictionaries**
   - Password leaks
   - Common phrases
   - Domain-specific terms
   - Mutations and combinations

3. **Optimize for Performance**
   - Bloom filters for fast checking
   - GPU acceleration
   - Efficient cryptographic libraries

4. **Use Probability**
   - Attack most likely passphrases first
   - Prioritize by frequency/popularity

### Brain Wallet as CTF Challenge

Some CTFs deliberately use weak brain wallets as challenges:

**Challenge Setup:**
```
"We've created a Bitcoin address using a passphrase from a famous book.
The address contains 0.01 BTC. Find the passphrase to claim it."

Hints:
- 19th-century American literature
- Opening line of a novel
- Author's last name starts with M
```

**Solution Approach:**
```bash
# Build dictionary from 19th-century American literature
wget -r gutenberg.org/browse/shelf/19th-century-american
cat *.txt | ./extract_sentences.py > literature.dict

# Filter by authors starting with M
grep "Melville\|Melville" literature.dict > filtered.dict

# Run Brainflayer
./brainflayer -v -b target.blf -i filtered.dict

# Found: "Call me Ishmael." (Moby-Dick opening line)
```

## Conclusion

The brain wallet attack with Brainflayer represents one of the most successful large-scale cryptographic attacks in Bitcoin history. By exploiting the fundamental weakness of human-generated entropy, Ryan Castellucci and others demonstrated that:

1. **Human intuition about randomness is poor**
2. **Dictionary attacks scale incredibly well** (1 trillion checks for $50)
3. **Even "clever" passphrases are predictable**
4. **Cryptographic security requires true randomness**

The attack forced the Bitcoin community to abandon brain wallets and adopt proper entropy sources (BIP39 mnemonic seeds). Today, brain wallets are universally recognized as insecure, and any newly funded brain wallet is drained within seconds by ever-vigilant monitoring bots.

**For cryptopuzzle solvers**, Brainflayer teaches:
- Always suspect low-entropy solutions
- Build comprehensive dictionaries
- Optimize with data structures (bloom filters)
- Use GPU acceleration when possible
- Consider psychological predictability

**For security practitioners**, brain wallets are a cautionary tale:
- Never rely on users to generate high-entropy secrets
- Always use cryptographically secure random number generators
- Test implementations against dictionary attacks
- Assume attackers have unlimited computational resources

The brain wallet attack stands as a perfect example of the principle: **In cryptography, there is no such thing as "secure enough for most people"—either it's cryptographically secure, or it's broken.**

---

**References:**
- DEFCON 23 Talk: "Brainflayer: Cracking Bitcoin Brain Wallets" by Ryan Castellucci
- Brainflayer GitHub: https://github.com/ryancdotorg/brainflayer
- XKCD #936: "Password Strength" - https://xkcd.com/936/
- "Speed Optimizations in Bitcoin Key Recovery Attacks" - Courtois & Song (2016)
- Bitcoin Improvement Proposal 39 (BIP39): Mnemonic code for generating deterministic keys
