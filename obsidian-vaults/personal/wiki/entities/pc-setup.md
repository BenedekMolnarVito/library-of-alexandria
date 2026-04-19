---
title: "PC Setup"
type: entity
domain: personal
tags:
  - hardware
  - infrastructure
  - desktop
created: 2026-04-19
updated: 2026-04-19
sources:
  - "[[sources/personal-vault-init-prompt]]"
---

# PC Setup

The primary desktop computer of [[wiki/entities/molnar-benedek]], used for software development, gaming, and daily productivity.

## Specifications

| Component | Details |
|-----------|---------|
| **CPU** | AMD Ryzen 7 3700X 8-Core Processor |
| **GPU** | AMD Radeon RX 5700 XT 8GB GDDR6 |
| **RAM** | 16GB DDR4 |
| **OS** | Windows (evidenced by environment) |

## Software Environment

- **Code Editor**: Visual Studio Code
- **Code Assistant**: GitHub Copilot
- **Browser**: Firefox
- **OneDrive**: Synced at C:\Users\molna\OneDrive

## Notes

- This is a circa-2019 mid-range build (Zen 2 CPU + RDNA1 GPU). Capable for most development tasks and moderate gaming but may struggle with large local AI model inference.
- The RX 5700 XT has 8GB VRAM — sufficient for small local AI models via ROCm/DirectML but limited for anything beyond ~7B parameter models.
