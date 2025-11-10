# Probability Theory and Combinatorics in Cryptographic Puzzles

## Abstract

Probability theory and combinatorics form the mathematical foundation for analyzing randomness, counting possibilities, and reasoning under uncertainty. This document provides comprehensive coverage of probability principles, combinatorial techniques, and their applications in cryptographic puzzle solving. We analyze the ARweave Puzzle 4 probability problem involving random droid voting and develop general frameworks for solving probability and counting problems in puzzle contexts.

---

## 1. Introduction

### 1.1 Definitions

**Probability Theory:**
The mathematical study of random phenomena, quantifying likelihood of events.

**Formal Definition:**
For sample space Ω and event A ⊆ Ω:
```
P(A) = |A| / |Ω|  (classical probability)

where:
    |A| = number of outcomes in A
    |Ω| = total number of possible outcomes
```

**Combinatorics:**
The mathematics of counting, arrangement, and selection.

### 1.2 Historical Development

**Early Probability (1654):**
- Pascal and Fermat: "Problem of Points" (dividing stakes)
- Foundation of modern probability theory

**Combinatorics Origins:**
- Ancient: Chinese counting rods, Indian mathematics
- Medieval: Combinatorial problems in poetry and music
- Modern: Formal development in 19th-20th centuries

**Key Contributors:**
- **Pierre de Fermat** (1607-1665): Combinatorial principles
- **Blaise Pascal** (1623-1662): Pascal's triangle
- **Jacob Bernoulli** (1654-1705): Law of large numbers
- **Abraham de Moivre** (1667-1754): Normal approximation
- **Leonhard Euler** (1707-1783): Graph theory, partitions
- **Andrey Kolmogorov** (1903-1987): Axiomatic probability

---

## 2. Probability Foundations

### 2.1 Sample Space and Events

**Sample Space (Ω):**
Set of all possible outcomes.

**Example: Coin Flip**
```
Ω = {H, T}
|Ω| = 2
```

**Example: Two Dice**
```
Ω = {(1,1), (1,2), ..., (6,6)}
|Ω| = 36
```

**Event:**
Subset of sample space.

**Example: Sum of dice = 7**
```
A = {(1,6), (2,5), (3,4), (4,3), (5,2), (6,1)}
|A| = 6
P(A) = 6/36 = 1/6
```

### 2.2 Kolmogorov Axioms

**Axiom 1 (Non-negativity):**
```
P(A) ≥ 0 for all events A
```

**Axiom 2 (Normalization):**
```
P(Ω) = 1
```

**Axiom 3 (Countable Additivity):**
```
For mutually exclusive events A₁, A₂, ...:
P(A₁ ∪ A₂ ∪ ...) = P(A₁) + P(A₂) + ...
```

### 2.3 Basic Probability Rules

**Complement Rule:**
```
P(A') = 1 - P(A)
where A' is complement of A
```

**Addition Rule:**
```
P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
```

**Multiplication Rule (Independent Events):**
```
P(A ∩ B) = P(A) × P(B)
```

**Conditional Probability:**
```
P(A|B) = P(A ∩ B) / P(B)
```

**Bayes' Theorem:**
```
P(A|B) = P(B|A) × P(A) / P(B)
```

---

## 3. Combinatorial Principles

### 3.1 Fundamental Counting Principle

**Rule:**
If task 1 can be done in n₁ ways, task 2 in n₂ ways, ..., task k in nₖ ways, then all tasks together can be done in:
```
n₁ × n₂ × ... × nₖ ways
```

**Example: Password**
```
Password = 3 letters (A-Z) + 2 digits (0-9)
Total combinations = 26 × 26 × 26 × 10 × 10
                   = 17,576,000
```

### 3.2 Permutations

**Permutations (Order Matters):**

**Without Repetition:**
```
P(n, r) = n! / (n-r)!

n = total items
r = items selected
```

**Example: Top 3 finishers in race of 10**
```
P(10, 3) = 10! / 7! = 10 × 9 × 8 = 720
```

**With Repetition:**
```
n^r

Example: 4-digit PIN (0-9)
10⁴ = 10,000
```

**Circular Permutations:**
```
(n-1)!

Example: Seating n people around circular table
(n-1)!
```

### 3.3 Combinations

**Combinations (Order Doesn't Matter):**

**Without Repetition:**
```
C(n, r) = n! / (r!(n-r)!)
Also written as (n choose r) or ⁿCᵣ
```

**Example: Choose 5 cards from 52**
```
C(52, 5) = 52! / (5! × 47!)
         = (52 × 51 × 50 × 49 × 48) / (5 × 4 × 3 × 2 × 1)
         = 2,598,960
```

**With Repetition:**
```
C(n+r-1, r) = (n+r-1)! / (r!(n-1)!)

Example: Choose 3 scoops from 5 flavors (can repeat)
C(5+3-1, 3) = C(7, 3) = 35
```

### 3.4 Pascal's Triangle

```
         1
       1   1
     1   2   1
   1   3   3   1
 1   4   6   4   1
1  5  10  10  5   1
```

**Property:**
```
C(n, r) = C(n-1, r-1) + C(n-1, r)

Each entry is sum of two entries above it
```

---

## 4. ARweave Puzzle 4: Droid Voting Problem

### 4.1 Problem Statement

**Verbal Description:**
"Three droids need to choose a leader. Only two of them are suitable for the function. However, droids have no idea about politics and they will vote randomly. What is the chance (%) that the same candidate gets all the votes?"

### 4.2 Problem Interpretation

**Clarification Questions:**
```
1. Are there exactly 2 candidates?
2. Can droids vote for themselves?
3. Is voting truly random (uniform distribution)?
```

**Assumption:**
Two candidates (A and B), each droid randomly votes for A or B with equal probability.

### 4.3 Solution Method 1: Enumeration

**Sample Space:**
Each droid has 2 choices, 3 droids total:
```
|Ω| = 2³ = 8 possible voting combinations
```

**All Outcomes:**
```
Droid 1, Droid 2, Droid 3:
1. A, A, A  ← Unanimous for A
2. A, A, B
3. A, B, A
4. A, B, B
5. B, A, A
6. B, A, B
7. B, B, A
8. B, B, B  ← Unanimous for B
```

**Unanimous Outcomes:**
```
Only outcomes 1 and 8 are unanimous
|Unanimous| = 2
```

**Probability:**
```
P(Unanimous) = 2 / 8 = 1/4 = 0.25 = 25%
```

**Answer: 25%**

### 4.4 Solution Method 2: Probability Rules

**Approach:**
Calculate probability directly using independence.

**P(All vote for A):**
```
Each droid votes A with probability 1/2
All independent: P(A,A,A) = (1/2)³ = 1/8
```

**P(All vote for B):**
```
Similarly: P(B,B,B) = (1/2)³ = 1/8
```

**P(Unanimous):**
```
P(All A or All B) = P(All A) + P(All B)
                  = 1/8 + 1/8
                  = 2/8 = 1/4 = 25%
```

### 4.5 Solution Method 3: Binomial Distribution

**Model:**
Let X = number of votes for candidate A
X ~ Binomial(n=3, p=0.5)

**PMF:**
```
P(X = k) = C(3, k) × (0.5)³

P(X = 0) = C(3,0) × (0.5)³ = 1 × 0.125 = 0.125  (All B)
P(X = 1) = C(3,1) × (0.5)³ = 3 × 0.125 = 0.375
P(X = 2) = C(3,2) × (0.5)³ = 3 × 0.125 = 0.375
P(X = 3) = C(3,3) × (0.5)³ = 1 × 0.125 = 0.125  (All A)
```

**Unanimous:**
```
P(X = 0 or X = 3) = 0.125 + 0.125 = 0.25 = 25%
```

### 4.6 Generalization

**n Droids, k Candidates:**

**All vote for same candidate:**
```
P(Unanimous) = k × (1/k)ⁿ = k¹⁻ⁿ = k / kⁿ
```

**Examples:**
```
n=3, k=2: P = 2/8 = 25%  ✓ (matches puzzle)
n=5, k=2: P = 2/32 = 6.25%
n=3, k=3: P = 3/27 ≈ 11.1%
n=4, k=2: P = 2/16 = 12.5%
```

---

## 5. Classical Probability Problems

### 5.1 Birthday Paradox

**Question:**
How many people needed for >50% chance two share a birthday?

**Analysis:**
```
P(No shared birthdays for n people):
    Person 1: 365/365
    Person 2: 364/365 (must differ from person 1)
    Person 3: 363/365 (must differ from 1 and 2)
    ...
    Person n: (365-n+1)/365

P(No match) = (365/365) × (364/365) × ... × ((365-n+1)/365)
            = 365! / ((365-n)! × 365ⁿ)

P(At least one match) = 1 - P(No match)
```

**Implementation:**
```python
def birthday_probability(n):
    """Calculate P(at least 2 people share birthday)."""
    if n > 365:
        return 1.0

    prob_no_match = 1.0
    for i in range(n):
        prob_no_match *= (365 - i) / 365

    return 1.0 - prob_no_match

# Find minimum n for P > 0.5
for n in range(1, 100):
    prob = birthday_probability(n)
    if prob > 0.5:
        print(f"n = {n}: P = {prob:.4f}")
        break

# Output: n = 23: P = 0.5073
```

**Answer:** 23 people

### 5.2 Monty Hall Problem

**Setup:**
- 3 doors: 1 has car, 2 have goats
- You choose door
- Host opens different door (always goat)
- Should you switch?

**Analysis:**

**If you don't switch:**
```
P(Win) = 1/3  (initial choice probability)
```

**If you switch:**
```
Initial choice correct: P = 1/3 → Switch loses
Initial choice wrong:   P = 2/3 → Switch wins

P(Win if switch) = 2/3
```

**Simulation:**
```python
import random

def monty_hall_simulation(n_trials=10000, switch=True):
    """Simulate Monty Hall problem."""
    wins = 0

    for _ in range(n_trials):
        # Setup
        car_door = random.randint(1, 3)
        choice = random.randint(1, 3)

        # Host opens door (not car, not choice)
        remaining = [d for d in [1,2,3] if d != choice and d != car_door]
        host_opens = random.choice(remaining)

        if switch:
            # Switch to other unopened door
            choice = [d for d in [1,2,3] if d != choice and d != host_opens][0]

        if choice == car_door:
            wins += 1

    return wins / n_trials

print(f"Don't switch: {monty_hall_simulation(switch=False):.4f}")
print(f"Switch:       {monty_hall_simulation(switch=True):.4f}")

# Output:
# Don't switch: 0.3341
# Switch:       0.6659
```

**Conclusion:** Always switch! (doubles your odds)

### 5.3 Gambler's Ruin

**Problem:**
Gambler with $a, opponent with $b. Fair coin flip, $1 bet each round. What's P(gambler wins all money)?

**Solution:**
```
Let P(a) = probability gambler wins starting with $a

Boundary conditions:
    P(0) = 0     (already broke)
    P(a+b) = 1   (already won)

Recurrence:
    P(a) = 0.5 × P(a-1) + 0.5 × P(a+1)

Solution (fair game):
    P(a) = a / (a+b)
```

**Example:**
```
Gambler has $10, opponent has $40
P(Win) = 10 / 50 = 0.2 = 20%
```

---

## 6. Combinatorial Problems

### 6.1 Derangements

**Problem:**
How many permutations of n items have NO item in its original position?

**Example: n=3**
```
Original: [1, 2, 3]

Permutations:
    [1,2,3] - Not derangement (all in place)
    [1,3,2] - Not derangement (1 in place)
    [2,1,3] - Not derangement (3 in place)
    [2,3,1] - Derangement ✓
    [3,1,2] - Derangement ✓
    [3,2,1] - Not derangement (2 in place)

D(3) = 2
```

**Formula:**
```
D(n) = n! × Σ((-1)^k / k!)  for k=0 to n

Approximation: D(n) ≈ n! / e

Examples:
    D(3) = 2
    D(4) = 9
    D(5) = 44
    D(10) = 1,334,961
```

**Implementation:**
```python
import math

def derangements(n):
    """Calculate number of derangements of n items."""
    total = 0
    for k in range(n+1):
        total += ((-1)**k) / math.factorial(k)

    return round(math.factorial(n) * total)

for n in range(1, 11):
    print(f"D({n}) = {derangements(n)}")
```

### 6.2 Stars and Bars

**Problem:**
Distribute r identical objects into n distinct bins.

**Formula:**
```
C(n+r-1, r) = (n+r-1)! / (r!(n-1)!)
```

**Example:**
```
Distribute 5 identical candies to 3 children

Solution: C(3+5-1, 5) = C(7, 5) = 21 ways
```

**Visual Representation:**
```
Use stars (*) for objects, bars (|) for dividers

*****||    → Child 1: 5, Child 2: 0, Child 3: 0
**|**|*    → Child 1: 2, Child 2: 2, Child 3: 1
|***|**    → Child 1: 0, Child 2: 3, Child 3: 2
```

### 6.3 Pigeonhole Principle

**Statement:**
If n+1 objects placed into n boxes, at least one box contains ≥2 objects.

**Applications:**

**Example 1:**
```
In any group of 367 people, at least 2 share a birthday.
(367 people, 366 possible birthdays including Feb 29)
```

**Example 2:**
```
In sequence of n²+1 distinct integers, either:
    - Increasing subsequence of length n+1, or
    - Decreasing subsequence of length n+1
```

**Generalized:**
```
If kn+1 objects in n boxes, some box has ≥k+1 objects
```

---

## 7. Advanced Topics

### 7.1 Conditional Probability and Independence

**Independent Events:**
```
P(A ∩ B) = P(A) × P(B)
P(A|B) = P(A)
```

**Dependent Events:**
```
P(A ∩ B) = P(A|B) × P(B)
```

**Example: Drawing Cards**
```
Without replacement (dependent):
    P(2 aces) = (4/52) × (3/51) = 1/221

With replacement (independent):
    P(2 aces) = (4/52) × (4/52) = 1/169
```

### 7.2 Expected Value

**Definition:**
```
E[X] = Σ xᵢ × P(X = xᵢ)
```

**Example: Dice Roll**
```
E[X] = 1×(1/6) + 2×(1/6) + 3×(1/6) + 4×(1/6) + 5×(1/6) + 6×(1/6)
     = 21/6 = 3.5
```

**Properties:**
```
E[aX + b] = aE[X] + b
E[X + Y] = E[X] + E[Y]  (linearity)
```

### 7.3 Variance and Standard Deviation

**Variance:**
```
Var(X) = E[(X - E[X])²]
       = E[X²] - (E[X])²
```

**Standard Deviation:**
```
σ = √Var(X)
```

**Example: Fair Coin (X = # heads in n flips)**
```
E[X] = n/2
Var(X) = n/4
σ = √(n/4) = √n / 2
```

### 7.4 Generating Functions

**Ordinary Generating Function:**
```
G(x) = Σ aₙ × xⁿ

Encodes sequence {aₙ} as coefficients of polynomial
```

**Example: Fibonacci**
```
F₀=0, F₁=1, Fₙ=Fₙ₋₁+Fₙ₋₂

G(x) = x / (1 - x - x²)
```

**Applications:**
- Counting combinations
- Solving recurrences
- Probability distributions

---

## 8. Probability Distributions

### 8.1 Discrete Distributions

**Uniform:**
```
P(X = k) = 1/n  for k ∈ {1, 2, ..., n}

Example: Die roll
```

**Binomial:**
```
P(X = k) = C(n,k) × p^k × (1-p)^(n-k)

n = trials, p = success probability

Example: Coin flips
```

**Geometric:**
```
P(X = k) = (1-p)^(k-1) × p

Number of trials until first success
```

**Poisson:**
```
P(X = k) = (λ^k × e^(-λ)) / k!

λ = average rate

Example: Arrivals per hour
```

### 8.2 Continuous Distributions

**Uniform:**
```
f(x) = 1/(b-a)  for x ∈ [a, b]
```

**Normal (Gaussian):**
```
f(x) = (1/(σ√(2π))) × exp(-(x-μ)²/(2σ²))

μ = mean, σ = standard deviation
```

**Exponential:**
```
f(x) = λe^(-λx)  for x ≥ 0

Models time between events
```

---

## 9. Applications in Cryptographic Puzzles

### 9.1 Analyzing Puzzle Difficulty

**Brute Force Probability:**
```
If solution is 1 of n equally likely possibilities:
    P(Success in k tries) = k/n
    P(Success by try k) = 1 - (1-1/n)^k
```

**Example: 4-character hex string**
```
n = 16⁴ = 65,536
P(Find in 1000 tries) = 1000/65536 ≈ 1.5%
```

### 9.2 Cryptographic Security

**Key Space Analysis:**
```
k-bit key:
    Total keys = 2^k
    Average guesses to break = 2^(k-1)

Examples:
    64-bit: 2^63 ≈ 9.2 × 10^18 operations
    128-bit: 2^127 ≈ 1.7 × 10^38 operations
    256-bit: 2^255 ≈ 5.8 × 10^76 operations
```

### 9.3 Birthday Attack

**Collision Probability:**
For hash function with n-bit output:
```
After √(2^n) ≈ 2^(n/2) attempts, expect collision

SHA-256 (256-bit):
    Collision resistance: 2^128 operations
```

---

## 10. Practice Problems

### Problem 1: Card Probability
From standard 52-card deck, draw 5 cards. What's P(exactly 2 aces)?

### Problem 2: Combinatorial
How many ways to arrange letters in "PROBABILITY"?

### Problem 3: Conditional
P(Rain) = 0.3, P(Traffic | Rain) = 0.8, P(Traffic | No Rain) = 0.2
What's P(Rain | Traffic)?

### Problem 4: Combinatorial Optimization
Choose 3 numbers from 1-20 such that sum is even. How many ways?

### Problem 5: Complex Probability
Roll two dice. Given sum ≥ 8, what's P(both dice show ≥ 4)?

---

## 11. Solutions

### Problem 1 Solution:
```
Total ways to draw 5 from 52: C(52,5)
Ways to get exactly 2 aces:
    - Choose 2 aces from 4: C(4,2)
    - Choose 3 non-aces from 48: C(48,3)

P = [C(4,2) × C(48,3)] / C(52,5)
  = [6 × 17,296] / 2,598,960
  = 103,776 / 2,598,960
  ≈ 0.0399 = 3.99%
```

### Problem 3 Solution (Bayes' Theorem):
```
P(Rain | Traffic) = P(Traffic | Rain) × P(Rain) / P(Traffic)

P(Traffic) = P(Traffic | Rain) × P(Rain) +
             P(Traffic | No Rain) × P(No Rain)
           = 0.8 × 0.3 + 0.2 × 0.7
           = 0.24 + 0.14 = 0.38

P(Rain | Traffic) = (0.8 × 0.3) / 0.38
                  = 0.24 / 0.38
                  ≈ 0.632 = 63.2%
```

---

## 12. References

### Textbooks
1. Ross, S. (2019). "A First Course in Probability", 10th Ed.
2. Feller, W. (1968). "An Introduction to Probability Theory and Its Applications"
3. Graham, R., Knuth, D., Patashnik, O. (1994). "Concrete Mathematics"

### Papers
1. Kolmogorov, A. (1933). "Foundations of the Theory of Probability"
2. Erdős, P. & Rényi, A. (1959). "On Random Graphs"

### Online Resources
- Brilliant.org: Interactive probability and combinatorics
- Khan Academy: Video tutorials
- AoPS (Art of Problem Solving): Problem sets

---

## 13. Conclusion

Probability theory and combinatorics provide essential tools for reasoning about uncertainty and counting possibilities. The ARweave Puzzle 4 droid voting problem exemplifies how these mathematical frameworks enable systematic solution of problems involving randomness.

Understanding probability and combinatorics is crucial not only for puzzle-solving but for cryptographic security analysis, algorithm design, and artificial intelligence. Whether calculating collision probabilities in hash functions, analyzing brute-force attack feasibility, or reasoning about random processes, these mathematical tools provide rigorous foundations for quantitative reasoning.

The intersection of probability, combinatorics, and cryptography demonstrates how classical mathematics remains indispensable in the digital age—from ancient counting problems to modern blockchain puzzles.

---

**Document Version:** 1.0
**Last Updated:** November 10, 2025
**Author:** ARweave Cryptopuzzle Research Project
