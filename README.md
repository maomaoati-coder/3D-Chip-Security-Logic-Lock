# 3D Chip Security Logic Lock (3D芯片安全逻辑锁)
### Multi-Step Physical Intercept & Audit Architecture

[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]() [![Simulator](https://img.shields.io/badge/Simulator-Icarus%20Verilog%2012.0-green.svg)](https://iverilog.icarus.com/) [![EPWave](https://img.shields.io/badge/Waveform-EPWave%20Verified-blue.svg)]() [![Tests](https://img.shields.io/badge/Tests-35%20cases%20%7C%20100%25%20pass-brightgreen.svg)]() [![Modules](https://img.shields.io/badge/Modules-5%2F5%20Passed-brightgreen.svg)]()

> **A novel 3D-stacked hardware security logic lock implementing nanosecond-level
> physical interception and audit — designed by an independent chip architect,
> working entirely on a mobile phone.**

---

## ⭐ If this project is useful to you, please Star it

Your star helps this work reach more hardware security researchers and engineers.
It takes 2 seconds and means a lot to an independent architect working alone.

**[⭐ Star this repository](https://github.com/maomaoati-coder/3D Chip Security Logic Lock)**

---
<p align="center">
  <img src="
https://github.com/maomaoati-coder/3D-Chip-Security-Logic-Lock/blob/main/Image_1773235848971_146.jpg
" width="600px">
</p>

## What is This?

A complete RTL implementation of a **three-layer stacked hardware security logic lock**:

```
Data Input
    ↓
┌──────────────────────────────┐
│  Layer 1: Forksheet Core     │  ARX computation → Vertical VIA leap
│  (Engine — 3nm behavior)     │
└──────────────┬───────────────┘
               │ TSV Channel (Through-Silicon VIA)
               ↓
┌──────────────────────────────┐
│  Layer 2: M2 Intercept       │  PGU Logic Array → Five Axioms Check
│  (Audit — Non-destructive)   │  → PASS / FAIL verdict
└──────────────┬───────────────┘
               │ TSV Channel
               ↓
┌──────────────────────────────┐
│  Layer 3: Sovereign Base     │  Back-gate bias → Logic gate off
│  (Brake — 12nm behavior)     │  → Hard-wired permanent shutdown
└──────────────────────────────┘
```

**Key innovation:** When audit fails, the brake layer executes
nanosecond-level back-gate bias adjustment followed by permanent
hard-wired logic gate deactivation — irreversible without hardware reset.
No software can bypass this.

---

## Five Axioms Check (M2 Audit Layer)

The audit layer validates five independent security axioms simultaneously:

| Axiom | Check | Meaning |
|-------|-------|---------|
| Axiom 1 | Bio-Hash = Stored | Data matches cryptographic reference |
| Axiom 2 | Phys-XOR = 0 | Physical audit chain integrity |
| Axiom 3 | Entropy ∈ [16,48] | No degenerate input attack |
| Axiom 4 | Sampling Integrity | Non-destructive tap confirmed |
| Axiom 5 | Truth Gate Parity | Logic consistency verified |

All five must pass. A single failure triggers the brake layer.

---

## Verification Results

> Verified on **EDA Playground** using **Icarus Verilog 12.0**
> All modules include EPWave waveform output ($dumpfile/$dumpvars)

| Module | File | Tests | Pass | EPWave | Status |
|--------|------|-------|------|--------|--------|
| forksheet_core | 引擎层_设计.sv | 7 | 100% | ✅ | ✅ PASSED |
| m2_intercept | 审计层_设计.sv | 6 | 100% | ✅ | ✅ PASSED |
| sovereign_base | 制动层_设计.sv | 8 | 100% | ✅ | ✅ PASSED |
| tsv_channel | 垂直通道_设计.sv | 6 | 100% | ✅ | ✅ PASSED |
| chip3d_security_top | 顶层集成_设计.sv | 8 | 100% | ✅ | ✅ PASSED |
| **Total** | | **35** | **100%** | **✅** | **5/5** |

Zero latch inferences. Zero timing violations.

---

## Repository Structure

```
3D-Chip-Security-Logic-Lock/
├── rtl/
│   ├── 引擎层_设计.sv          # forksheet_core
│   ├── 审计层_设计.sv          # m2_intercept
│   ├── 制动层_设计.sv          # sovereign_base
│   ├── 垂直通道_设计.sv        # tsv_channel
│   └── 顶层集成_设计.sv        # chip3d_security_top (all modules)
├── tb/
│   ├── 引擎层_测试台.sv
│   ├── 审计层_测试台.sv
│   ├── 制动层_测试台.sv
│   ├── 垂直通道_测试台.sv
│   └── 顶层集成_测试台.sv
├── docs/
│   ├── 技术论文_中文版.html
│   ├── Technical_Paper_EN.html
│   ├── 仿真验证报告_中文版.html
│   └── Verification_Report_EN.html
├── LICENSE
├── CITATION.cff
└── README.md
```

---

## Quick Start — Run on EDA Playground

1. Go to [edaplayground.com](https://www.edaplayground.com)
2. Select **Icarus Verilog 12.0** | Check **Open EPWave after run**
3. Paste design file into **Design** panel
4. Paste testbench into **Testbench** panel
5. Click **Run** → EPWave opens automatically

---

## Security Architecture — Three-Layer Defense

```
ATTACK SCENARIO                    DEFENSE RESPONSE
─────────────────                  ────────────────
Illegal data injection      →      Axiom 1/2/3 fail → FAIL verdict
Entropy manipulation        →      Axiom 3 (Hamming [16,48]) blocks it
Sampling channel attack     →      Axiom 4 (non-destructive tap)
Logic consistency bypass    →      Axiom 5 (truth gate parity)
Any audit failure           →      Brake layer activates in ns
Software unlock attempt     →      HARDLOCK: only hardware rst_n works
```

---

## Design Story

This architecture was designed entirely by a **single independent chip architect
working on a mobile phone** — no computer, no commercial EDA tools, no lab.

The 3D stacked security lock represents the next generation beyond the
[SiliconForge Security SoC V3.0](https://github.com/maomaoati-coder/3D Chip Security Logic Lock),
adding physical-layer enforcement that no software can circumvent.

---

## License & IP

**Copyright (c) 2026 maomaoati-coder. All Rights Reserved.**

This design is proprietary. Unauthorized copying, use, or distribution is prohibited.
For licensing and collaboration inquiries, open an Issue or Discussion.

See [LICENSE](LICENSE) for full terms.

---

## Citation

If you reference this work in research or publications:

```bibtex
@software{chip3d_security_lock_2026,
  author    = {maomaoati-coder},
  title     = {3D Chip Security Logic Lock: Multi-Step Physical Intercept and Audit},
  year      = {2026},
  month     = {March},
  url       = {https://github.com/maomaoati-coder/3D-Chip-Security-Logic-Lock},
  note      = {Verified: Icarus Verilog 12.0, EDA Playground, EPWave}
}
```

---

## Contact

- Open an **Issue** for technical questions
- Open a **Discussion** for collaboration or licensing
- GitHub: [@maomaoati-coder](https://github.com/maomaoati-coder)

---

**⭐ Star this project if it helped you or inspired your work.**

*Three layers. Five axioms. Nanosecond response. Designed on a phone.*
