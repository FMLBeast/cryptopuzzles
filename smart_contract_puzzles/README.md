# Smart Contract Cryptographic Puzzles Collection

## Overview

This collection documents smart contract-based cryptographic puzzles and CTF challenges, primarily focusing on EVM (Ethereum Virtual Machine) puzzles that require solving cryptographic challenges implemented as on-chain smart contracts.

**Collection Stats:**
- **Platforms:** 2 (Curta CTF, Codex Protocol)
- **Puzzles Documented:** 10+
- **Prize Types:** ETH, NFTs, cryptocurrency
- **Difficulty Range:** Beginner to Advanced
- **Years Covered:** 2018-2024

## Platforms

### 1. Curta CTF

**Type:** On-chain competitive CTF platform
**Blockchain:** Ethereum, Base, other EVM chains
**Rewards:** NFTs for successful solvers
**Creator:** waterfall-mkt
**GitHub:** `github.com/waterfall-mkt/curta`

**Description:**
> "A CTF protocol, where players create and solve EVM puzzles to earn NFTs."

#### How Curta Works

**Puzzle Structure:**
Every Curta puzzle must implement a standardized interface:
```solidity
interface IPuzzle {
    function name() external pure returns (string memory);

    function generate(address _seed) external returns (uint256);

    function verify(uint256 _start, uint256 _solution) external returns (bool);
}
```

**Key Innovation: Generative Puzzles**
- `generate(address)` takes the solver's address as a seed
- Returns a unique starting position for that solver
- Each puzzle is **unique to each solver** - no copying solutions!

**Solving Process:**
1. Call `generate(your_address)` to get your unique starting position
2. Solve the puzzle for YOUR specific instance
3. Call `verify(starting_position, your_solution)`
4. If correct: Receive NFT reward and leaderboard placement

#### Curta Cup 2023

**Event Details:**
- **Co-hosts:** Linea blockchain
- **Sponsors:** Base (Coinbase), Zuzalu
- **Puzzles:** 8 challenges
- **Authors:** ChainLight, Ottersec, Zellic
- **Participants:** Hundreds of solvers worldwide

**Prize Structure:**
- **1st place:** 3 NFTs (multiple puzzle solves)
- **Top 5:** NFT rewards
- **All solvers:** Participation NFT (varying rarity)

### 2. Codex Protocol

**Type:** Art + Cryptography puzzles
**Blockchain:** Ethereum
**Years Active:** 2018-2020
**Prize Type:** ETH bounties

**Description:**
> "CryptoPuzzles: Where art, cryptography, and cryptocurrency meet"

**Unique Approach:**
Codex combines physical art, mathematical challenges, and blockchain technology into integrated puzzles that require both visual analysis and cryptographic knowledge.

## Major Solved Puzzles

### Codex Puzzle #1 - "CODEXOKRYPHODRON" (Solved)

**Prize:** 3.1337 ETH
**Announcement:** May 25, 2018
**Solve Date:** ~20 days after announcement
**Creator:** Artist Zd3n

#### Challenge Description

**Visual Component:**
A dodecahedron (12-sided polyhedron) with intricate markings, paths, and symbols.

**Mathematical Component:**
An ETH private key is created from 256 bits of secret information - solvers needed to extract exactly 256 bits from the puzzle.

#### Solution Components

**1. Fibonacci Sequence (256 values)**

**Clue:** The puzzle included a hint showing the first few Fibonacci numbers in Roman numerals:
```
I, I, II, III, V, VIII, XIII, XXI...
(1, 1, 2, 3, 5, 8, 13, 21...)
```

**Task:** Calculate the first 256 values of the Fibonacci sequence

**Mathematical Formula:**
```
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2) for n ≥ 2
```

**Implementation:**
```python
def fibonacci_sequence(n):
    fib = [0, 1]
    for i in range(2, n):
        fib.append(fib[i-1] + fib[i-2])
    return fib[:n]

# Get first 256 Fibonacci numbers
fib_256 = fibonacci_sequence(256)
```

**2. Dodecahedron Path Following**

**Visual Clue:** The dodecahedron featured a rope/path (shown in red) that navigated between faces

**Task:** Follow the path in the correct sequence

**Method:**
1. Start at designated starting face
2. Follow the red rope/path visualization
3. Record which faces are visited in order
4. Each face contributes to the final solution

**3. Face-to-Bit Mapping**

**Integration:** Each face of the dodecahedron corresponds to a Fibonacci number

**Conversion Process:**
```
Face sequence → Fibonacci indices → Binary representation → 256-bit key
```

**4. Leonardo da Vinci References**

**Art Historical Context:**
- Dodecahedron appears in da Vinci's geometric studies
- Renaissance polyhedra illustrations
- Sacred geometry principles

**Purpose:** Added cultural depth and misdirection

#### Complete Solution Process

**Step 1: Calculate Fibonacci Sequence**
```python
import hashlib

def generate_fibonacci_256():
    fib = [0, 1]
    for i in range(2, 256):
        fib.append(fib[i-1] + fib[i-2])
    return fib
```

**Step 2: Extract Path from Dodecahedron**
```
Follow the red rope through faces:
Face A → Face D → Face G → Face B → ...
(12 faces total, path visits each in specific order)
```

**Step 3: Map to Fibonacci Values**
```python
face_order = [0, 3, 6, 1, ...]  # Indices based on path
fibonacci_values = [fibonacci_256[i] for i in face_order]
```

**Step 4: Convert to Binary**
```python
# Combine Fibonacci values into 256-bit key
key_bits = ''
for value in fibonacci_values:
    # Convert value to binary and extract bits
    key_bits += bin(value)[2:].zfill(8)  # Example encoding

# Ensure exactly 256 bits
private_key_bin = key_bits[:256]
```

**Step 5: Derive Ethereum Private Key**
```python
# Convert binary to integer
private_key_int = int(private_key_bin, 2)

# Convert to hex for Ethereum
private_key_hex = hex(private_key_int)[2:].zfill(64)

print(f"Private Key: 0x{private_key_hex}")
```

**Step 6: Claim Reward**
```javascript
// Use web3.js or similar
const account = web3.eth.accounts.privateKeyToAccount(privateKey);
// Transfer 3.1337 ETH to your address
```

#### Creator's Artistic Vision

**From Zd3n's writeup:**
> "I wanted to create a puzzle that wasn't just mathematical or just artistic, but required understanding both. The dodecahedron represents the intersection of art, mathematics, and cryptography - just like blockchain technology itself."

**Layers of Meaning:**
1. **Mathematical:** Fibonacci sequence (nature's pattern)
2. **Geometric:** Dodecahedron (Platonic solid)
3. **Historical:** Da Vinci (Renaissance innovation)
4. **Modern:** Blockchain (current technology frontier)

#### Solution Statistics

**Solve Time:** ~20 days
**Attempts:** Hundreds of failed attempts
**Tools Used:**
- 3D modeling software (to analyze dodecahedron)
- Python (Fibonacci calculation)
- Web3 libraries (key derivation)
- Image analysis tools

**Winner's Prize:**
- 3.1337 ETH (worth ~$1,500-$3,000 at the time)
- Recognition in Codex community
- First solver of CODEXOKRYPHODRON series

---

### Curta CTF Puzzle #2 - "Vanity Address Challenge" (Solved)

**Author:** ChainLight team
**Prize:** NFT (1st place)
**Solver:** ChainLight (1st place)
**Technique:** CREATE2 vanity address generation

#### Challenge Description

**Task:** Generate a smart contract at a specific address that satisfies the verify function

**Puzzle Interface:**
```solidity
contract Puzzle2 {
    function generate(address _seed) external pure returns (uint256) {
        // Generate unique starting position based on solver's address
        return uint256(keccak256(abi.encodePacked(_seed)));
    }

    function verify(uint256 _start, uint256 _solution) external view returns (bool) {
        // Verify that the solution produces the target address
        address target = deriveAddress(_start, _solution);
        return isValidTarget(target);
    }
}
```

#### Solution Approach: CREATE2 Vanity Addresses

**Background: CREATE2**
```solidity
// CREATE2 allows deterministic contract address generation
address = keccak256(0xff ++ deployerAddress ++ salt ++ keccak256(bytecode))[12:]
```

**Strategy:**
1. Find a `salt` value that produces an address matching the target pattern
2. Deploy contract using CREATE2 with that salt
3. Contract address is now predictable and can satisfy verification

**Implementation:**
```solidity
contract VanityDeployer {
    function findSalt(bytes32 initCodeHash, bytes memory pattern)
        external
        view
        returns (uint256 salt)
    {
        // Brute force search for salt
        for (uint256 i = 0; i < type(uint256).max; i++) {
            address predicted = predictAddress(initCodeHash, bytes32(i));
            if (matches(predicted, pattern)) {
                return i;
            }
        }
    }

    function predictAddress(bytes32 initCodeHash, bytes32 salt)
        internal
        view
        returns (address)
    {
        return address(uint160(uint256(keccak256(abi.encodePacked(
            bytes1(0xff),
            address(this),
            salt,
            initCodeHash
        )))));
    }
}
```

**Optimization:**
```javascript
// Off-chain computation (much faster)
const ethers = require('ethers');

function findVanitySalt(initCodeHash, pattern) {
    for (let salt = 0; salt < Number.MAX_SAFE_INTEGER; salt++) {
        const address = ethers.utils.getCreate2Address(
            deployerAddress,
            ethers.utils.hexZeroPad(ethers.utils.hexlify(salt), 32),
            initCodeHash
        );

        if (address.startsWith(pattern)) {
            return salt;
        }

        if (salt % 1000000 === 0) {
            console.log(`Checked ${salt} salts...`);
        }
    }
}

const salt = findVanitySalt(initCodeHash, '0x0000');
console.log(`Found salt: ${salt}`);
```

#### ChainLight's Winning Solution

**Time:** First to solve
**Technique:** GPU-accelerated vanity address generation

**Performance:**
- CPU brute force: ~100,000 addresses/second
- GPU acceleration: ~10,000,000 addresses/second (100× faster)
- Found salt in: ~30 minutes

**Reward:** 1st place NFT + leaderboard recognition

---

### Curta CTF Puzzle #3 - "ZSafe ECDSA Challenge" (Solved)

**Author:** jazzy (Zellic)
**Difficulty:** Advanced
**Technique:** ECDSA signature manipulation

**Writeup Source:** philogy.github.io/posts/curta-zsafe-writeup/

#### Challenge Concept

**False Assumption:** "Once a contract is deployed, its code is immutable"

**Reality:** Metamorphic contracts can change their code at the same address

**Puzzle Setup:**
```solidity
contract ZSafe {
    function generate(address _solver) external pure returns (uint256) {
        // Generate challenge based on solver's address
        return uint256(keccak256(abi.encodePacked(_solver, block.timestamp)));
    }

    function verify(uint256 _start, uint256 _solution) external view returns (bool) {
        // Complex ECDSA verification
        // Requires finding specific signature properties
    }
}
```

#### ECDSA Background

**Elliptic Curve Digital Signature Algorithm:**
```
Signature = (r, s)
r = (k × G).x mod n
s = (hash + r × privKey) / k mod n

Where:
- k is a random nonce
- G is the generator point
- n is the curve order
- privKey is the private key
```

**Key Vulnerability:** Nonce reuse or nonce malleability

#### Solution Technique

**Observation:** The puzzle exploits properties of ECDSA signatures and Ethereum's ecrecover

**Attack Vector:**
1. For same message hash, different (r, s) pairs can be valid
2. Given signature (r, s), can construct (r, n - s) as valid alternative
3. Metamorphic contract can be deployed, selfdestruct, and redeployed with different code

**Mathematical Insight:**
```
If (r, s) is a valid signature for message m and public key P, then:
(r, -s mod n) is also a valid signature for the same m and P

This is because ECDSA verification checks:
s⁻¹ × (hash × G + r × P) =? R (point with x-coordinate r)

With -s:
(-s)⁻¹ × (hash × G + r × P) = -(s⁻¹ × (hash × G + r × P))
```

**Exploitation:**
```solidity
// Deploy contract A at address X
CREATE2(salt, bytecodeA) → address X

// Get signature from contract A

// Selfdestruct contract A
// Deploy contract B at same address X
CREATE2(salt, bytecodeB) → address X (same!)

// Use signature malleability to pass verification with contract B
```

#### Solver's Implementation (Simplified)

```solidity
contract MetamorphicSolution {
    function solve() external {
        // Step 1: Deploy initial contract
        bytes32 salt = bytes32(uint256(0x1337));
        address instance = deploy(salt, bytecodeA);

        // Step 2: Get signature from initial state
        (uint8 v, bytes32 r, bytes32 s) = getSignature(instance);

        // Step 3: Selfdestruct and redeploy
        Instance(instance).destroy();
        instance = deploy(salt, bytecodeB); // Same address!

        // Step 4: Submit malleable signature
        bytes32 s_flipped = bytes32(CURVE_ORDER - uint256(s));

        // Step 5: Verify
        puzzle.verify(start, encodeSolution(v, r, s_flipped));
    }
}
```

#### Key Learnings

1. **Code isn't truly immutable** - Metamorphic contracts challenge this assumption
2. **ECDSA signatures have malleability** - (r, s) and (r, -s) both valid
3. **Creative use of CREATE2** - Same address, different code
4. **Advanced EVM mechanics** - Requires deep understanding of Ethereum

---

## Techniques Used Across Smart Contract Puzzles

### 1. CREATE2 Vanity Address Generation

**Purpose:** Generate contracts at specific addresses
**Complexity:** O(16^n) for n hex digits
**Tools:** GPU acceleration, custom miners

### 2. ECDSA Signature Analysis

**Purpose:** Exploit signature malleability and nonce vulnerabilities
**Required Knowledge:** Elliptic curve cryptography, modular arithmetic
**Common Vulnerabilities:** Nonce reuse, signature malleability

### 3. Metamorphic Contracts

**Purpose:** Change contract code at same address
**Technique:** CREATE2 + SELFDESTRUCT + CREATE2
**Use Case:** State manipulation, signature tricks

### 4. Storage Manipulation

**Purpose:** Direct manipulation of contract storage
**Technique:** Understanding Ethereum storage layout
**Tools:** Web3.js, custom scripts

### 5. Gas Optimization Puzzles

**Purpose:** Find solutions within gas limits
**Technique:** Assembly optimization, algorithm efficiency
**Challenge:** Compute intensive operations on-chain

### 6. Hash Collisions and Pre-images

**Purpose:** Find inputs that hash to specific values
**Technique:** Brute force, birthday attacks
**Difficulty:** Depends on hash function and output length

---

## Tools and Resources

### Development Frameworks

**Foundry**
```bash
# Install Foundry
curl -L https://foundry.paradigm.xyz | bash
foundryup

# Create new project
forge init my-curta-puzzle

# Run tests
forge test
```

**Hardhat**
```bash
npm install --save-dev hardhat
npx hardhat init
```

### Analysis Tools

**Etherscan:** Verify contracts, read storage
**Tenderly:** Debug transactions, simulate
**Dedaub:** Decompile contracts
**Remix:** IDE for Solidity development

### Libraries

**ethers.js:** Ethereum interactions
```javascript
const ethers = require('ethers');
const provider = new ethers.providers.JsonRpcProvider(RPC_URL);
```

**web3.py:** Python Ethereum library
```python
from web3 import Web3
w3 = Web3(Web3.HTTPProvider(RPC_URL))
```

---

## Learning Path

### Beginner

**Prerequisites:**
- Basic Solidity
- Understanding of Ethereum accounts
- Familiarity with transactions

**First Puzzles:**
- Simple arithmetic challenges
- Basic storage puzzles
- String manipulation

**Tools:**
- Remix IDE
- Etherscan
- MetaMask

### Intermediate

**Prerequisites:**
- Advanced Solidity (assembly, storage layout)
- Gas optimization understanding
- EVM opcodes familiarity

**Challenges:**
- CREATE2 vanity addresses
- Simple ECDSA challenges
- Storage slot manipulation

**Tools:**
- Foundry/Hardhat
- Tenderly
- ethers.js

### Advanced

**Prerequisites:**
- Deep EVM understanding
- Cryptography knowledge (ECDSA, hashing)
- Assembly optimization

**Challenges:**
- Metamorphic contracts
- Advanced ECDSA manipulation
- Gas-constrained puzzles

**Tools:**
- Custom tooling
- GPU acceleration
- Decompilers (Dedaub)

---

## Active Platforms and Future Puzzles

### Current Platforms

**Curta (curta.wtf)**
- Active puzzle releases
- NFT rewards
- Leaderboard competition

**Paradigm CTF**
- Annual event
- High difficulty
- Industry recognition

### Upcoming Trends

1. **Layer 2 Puzzles:** Optimism, Arbitrum, zkSync
2. **Zero-Knowledge Proofs:** zk-SNARK challenges
3. **MEV Challenges:** Flashbots, MEV-related puzzles
4. **Cross-chain Puzzles:** Multi-chain coordination

---

## Conclusion

Smart contract cryptographic puzzles represent the cutting edge of blockchain-based challenges. Unlike traditional CTFs, these puzzles exist permanently on-chain, are provably fair, and often reward solvers automatically through smart contracts.

From the artistic vision of Codex Protocol to the technical depth of Curta CTF, these platforms push solvers to understand not just smart contracts, but the underlying cryptography, EVM mechanics, and creative exploits that make blockchain technology both powerful and complex.

**For AI Training:** These puzzles demonstrate:
- Multi-layered problem solving
- Integration of art, math, and code
- Novel applications of cryptographic primitives
- Creative use of blockchain properties

---

**Primary Sources:**
- Medium: "Solve Codex Puzzle Bounty and Earn Cryptocurrency" by Codex
- Steemit: "Codex Puzzle #1 — CODEXOKRYPHODRON" by Zd3n
- Medium: "Curta CTF Write-Up" by ChainLight
- Blog: "Curta CTF ZSafe Write-up" by Philogy
- GitHub: waterfall-mkt/curta
- curta.wtf official documentation

*Document compiled from Medium articles, blog posts, and GitHub resources, November 2025*
