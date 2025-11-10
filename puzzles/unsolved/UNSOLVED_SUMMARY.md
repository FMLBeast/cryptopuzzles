# Unsolved ARweave Puzzles Summary

This document provides an overview of all currently unsolved ARweave puzzles and their status.

---

## Overview

- **Total Unsolved**: 6 puzzles
- **Total Unclaimed Rewards**: 1000+ AR (Puzzle 3 alone) + unknown amounts
- **Longest Unsolved**: Puzzle 3 (6+ years)
- **Difficulty Range**: Hard to Very Hard

---

## Puzzle 3 - The Crown Jewel

**Prize**: 1000 AR (~$21,000 USD)
**Years Unsolved**: 6+ years
**Difficulty**: Very Hard

### What We Know:
- 8 images → 8 four-character answers
- Likely involves steganography
- SHA-256 related (one image became "obsolete" with ARweave 1.7.0.0 update to SHA-384)
- Community has proposed various interpretations

### Why It's Hard:
- Minimal clues
- Requires deep ARweave technical knowledge
- Steganography + symbolic interpretation
- Exact format matching required

**[Detailed Documentation](puzzle_03.md)**

---

## Puzzle 5

**Status**: Marked as "solved" in HomelessPhD repository, but limited public documentation
**Difficulty**: Hard
**ARweave URL**: [Link](https://d5zw4kksq5gasg7ezkjvdpey562svcviatdltuyga43lrkexvngq.arweave.net/H3NuKVKHTAkb5MqTUbyY77UqiqgExrnTBgc2uKiXq00)

### Status Ambiguity:
- Listed as solved in some sources
- No public solution writeup found
- Solution methodology unknown

---

## Puzzle 7

**Prize**: 3 ETH
**Status**: Marked as "solved" but minimal documentation
**Announced**: June 14, 2019
**Difficulty**: Very Hard
**ARweave URL**: [Link](https://eplpvctnryuimypdq6gbfk4rx3bbfepzoxz5pldkqdjczy5udpla.arweave.net/I9b6im2OKIZh44eMEquRvsISkfl189esaoDSLOO0G9Y)

### Notes:
- Larger prize (3 ETH) suggests higher difficulty
- Listed among harder puzzles in difficulty rankings
- Solution method not publicly documented

---

## Puzzle 9

**Status**: Unsolved (or unverified)
**Difficulty**: Very Hard
**ARweave URL**: [Link](https://27xy2rcwg6o2g4colrausghtbtzvjk7au7lsfrwzdgqbq5s6tplq.arweave.net/1--NRFY3naNwTlxBSRjzDPNUq-Cn1yLG2RmgGHZem9c)

### Information:
- Listed in difficulty ranking as very hard
- April 2020: Still marked unsolved
- Visual puzzle with embedded image
- No public solution attempts documented

---

## Puzzle 10

**Status**: Unsolved
**Announced**: April 14, 2020
**Difficulty**: Very Hard
**ARweave URL**: [Link](https://2xzm6mh75smp5ivf2img3biam3iu7qhodsw5mk7cimkx7g4trl4a.arweave.net/1fLPMP_smP6ipdIYbYUAZtFPwO4crdYr4kMVf5uTivg)

### Information:
- Active community attempts (Medium article by Winwon)
- One of the more recent puzzles
- Solution attempts in progress but unsuccessful
- HomelessPhD repository tracking

---

## Puzzle 11

**Status**: Unsolved
**Difficulty**: Unknown
**Information**: Minimal public information available

---

## Puzzle 12

**Status**: Unsolved
**Difficulty**: Unknown
**ARweave URL**: [Link](https://2giml2y2fhwh.arweave.net/gymumAAsxGlzqPL5HzoEB8Xryu61o174j7vHwx21Qoo)

### Information:
- Later puzzle in series
- Minimal documentation
- HomelessPhD repository tracking

---

## Difficulty Rankings

### From @ArweaveP (March 2020):
**Unsolved puzzles ordered by difficulty:**
```
Easiest → Hardest:
3, 9, 8, 5, 7
```

**Note**: Puzzle 8 was later solved, but was ranked among harder puzzles.

### Historical Context:
- As of April 2020: Puzzles 1, 2, 4, 8 solved; 3, 5, 7, 9 unsolved
- "Odds are harder" - odd-numbered puzzles noted as more difficult

---

## Common Characteristics of Unsolved Puzzles

### Similarities:
1. **Visual-heavy** - Most involve image interpretation
2. **Minimal clues** - Few or no explicit hints
3. **Technical knowledge** - Require deep ARweave/crypto expertise
4. **Steganography suspected** - Hidden information in images
5. **Long-standing** - Years without solutions suggest extreme difficulty

### Likely Techniques Required:
- Advanced steganography
- Deep ARweave protocol knowledge
- Blockchain technical concepts
- Creative interpretation
- Possibly novel or obscure encoding methods

---

## Solving Strategies for Unsolved Puzzles

### 1. Steganography Analysis
```bash
# Try multiple tools
steghide extract -sf puzzle_image.png
zsteg puzzle_image.png --all
binwalk puzzle_image.png
exiftool puzzle_image.png
```

### 2. ARweave Deep Dive
- Study ARweave yellow paper
- Understand version changes (especially 1.7.0.0)
- Research Wildfire, Blockshadow, Proof of Access
- Examine ARweave GitHub commits from 2019-2020

### 3. Image Analysis
```python
from PIL import Image
import numpy as np

img = Image.open('puzzle.png')
# Separate channels
r, g, b = img.split()
# Look for patterns in individual channels
# Check for embedded data in LSBs
```

### 4. Community Collaboration
- Join ARweave Discord/Telegram
- Check GitHub issues (HomelessPhD/AR_Puzzles)
- Review historical Twitter discussions (@ArweaveP)
- Share findings and theories

---

## Unsolved Puzzle Opportunities

### For Researchers:
- Test novel steganography techniques
- Apply machine learning to pattern recognition
- Develop automated analysis tools
- Contribute to puzzle-solving methodology

### For AI Training:
- Examples of long-term unsolved problems
- Open-ended challenges without clear solution paths
- Multi-technique integration requirements
- Real-world cryptographic complexity

### For Bounty Hunters:
- Significant unclaimed rewards (Puzzle 3: $21,000+)
- Race condition: first solver wins
- Public verification of solutions
- Community recognition

---

## Resources for Solving

### Primary:
- **HomelessPhD/AR_Puzzles** - GitHub repository with tools and analysis
- **@ArweaveP** - Twitter account with historical hints
- **ARweave Documentation** - Technical references

### Tools:
- Steganography suite (Steghide, Stegsolve, zsteg)
- Image editors (GIMP, ImageMagick)
- Python + PIL/Pillow for programmatic analysis
- ARweave blockchain explorer

### Community:
- ARweave Discord
- Crypto puzzle forums
- Reddit r/ARweave
- GitHub discussions

---

## Historical Significance

These unsolved puzzles represent:
- **Longest-running crypto bounties** in the ARweave ecosystem
- **Testament to difficulty** - years without solutions
- **Community engagement** - ongoing attempts and discussions
- **Technical depth** - requiring bleeding-edge crypto knowledge

The fact that Puzzle 3 has remained unsolved for 6+ years despite a $21,000 bounty demonstrates the exceptional difficulty and the sophisticated nature of these challenges.

---

## Call to Action

If you're interested in attempting these puzzles:

1. **Start with Puzzle 3** - highest reward, most documentation
2. **Study solved puzzles** - understand creator's style
3. **Use multiple approaches** - combine techniques
4. **Join community** - collaborate and share findings
5. **Document attempts** - contribute to collective knowledge

---

## Updates

This document will be updated as:
- Puzzles get solved
- New information emerges
- Community makes progress
- Tools and techniques evolve

**Last Updated**: November 10, 2025
**Next Review**: Check HomelessPhD/AR_Puzzles repository for latest status
