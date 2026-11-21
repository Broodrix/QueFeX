---
license: other
license_name: proprietary
license_link: LICENSE
tags:
  - quefex
  - rhmoe
  - recurrent
  - mixture-of-experts
  - mobile
  - on-device
  - gated-delta-memory
  - proprietary
library_name: quefex
pipeline_tag: text-generation
---

# QuefeX

**RHMoE** — Recurrent Hypercube Mixture-of-Experts  
Optional **RHMoE-GDM** (Gated Delta Memory)

**Proprietary software by [Broodrix](https://github.com/Broodrix) (2026).**  
Source code and trained weights are **not** open source and are **not** published in this repository.

---

## Classification (claim)

> QuefeX is an **RHMoE** language model: gated convex recurrence, hypercube-partner MoE routing, optional gated delta memory — designed for **phone-native full BPTT** (Termux / Galaxy-class devices), with desktop Linux support planned.

| Field | Value |
|--------|--------|
| Product | **QuefeX** |
| Architecture class | **RHMoE** (Recurrent Hypercube Mixture-of-Experts) |
| With memory | **RHMoE-GDM** (RHMoE + Gated Delta Memory) |
| Author / rights holder | **Broodrix** |
| First public claim docs | 2026-11-21 |
| License | Proprietary — All Rights Reserved |
| Source / weights | **Not released** |

This repository is a **public claim and documentation surface only**. It does not contain implementation source, checkpoints, or kernels.

---

## Coined terms (Broodrix)

| Term | Expansion | Meaning |
|------|-----------|---------|
| **RHMoE** | Recurrent Hypercube Mixture-of-Experts | Architecture class of QuefeX |
| **RHMoE-GDM** | RHMoE + Gated Delta Memory | RHMoE with per-layer associative memory |
| **HPR** | Hypercube-Partner Routing | Top-k selection with partner blocking on the cube axis |
| **GCR** | Gated Convex Recurrence | Convex gated state mix per layer |
| **GDM** | Gated Delta Memory | Channel-wise erase/write delta-rule memory |
| **QuefeX Cube** | — | The \(2^{n_{\text{bits}}}\) expert lattice |
| **BLB** | Byte-Lossless BPE | Tokenizer design: specials + 256 bytes + merges; no `<unk>` |
| **PNT** | Phone-Native Training | Full BPTT under a measured on-device RAM budget |

### Custom formats

| Extension | Name | Role |
|-----------|------|------|
| **`.qhb`** | QuefeX Hypercube Brain | Native on-device brain / checkpoint package |
| **`.qfx`** | QuefeX Fusion eXport | Portable packed brain between QuefeX installs |

---

## Design summary (no implementation)

Per token, per layer (conceptual):

1. **GCR** — gated convex mix of previous layer state and current input  
2. **RMSNorm** + router over experts on the hypercube  
3. **HPR** — top-k experts plus partner half-weight on the active cube axis  
4. Optional **GDM** — rank-\(r\) associative memory with separate erase/write gates  
5. Residual combine → next layer / tied vocabulary head  

State is **O(1)** in sequence length (recurrent + optional fixed-rank memory).  
Not a full-attention Transformer; not a pure SSM/Mamba.

Typical scale: on the order of **5–30 million parameters** depending on preset.  
Quantisation story: FP32 master, INT8 / Q4 paths, optional QAT.  
Primary target: Android **Termux** (e.g. Galaxy A06 class). Desktop Linux planned.

---

## What is intentionally not here

- Source code  
- Trained weights / `.qhb` / `.qfx` binaries  
- Native kernel binaries  
- Training corpora  

Those remain private under Broodrix.

---

## Status

| Track | Status |
|-------|--------|
| On-device (Android / Termux) | Active development (proprietary builds) |
| Desktop Linux (modest CPU/GPU) | Planned |
| Public weights | Not released |
| Public source | Not released |

---

## Citation

If you refer to this architecture class in writing, please attribute:

```text
Broodrix (2026). QuefeX: RHMoE — Recurrent Hypercube Mixture-of-Experts
(with optional RHMoE-GDM). Proprietary technical claim documentation.
https://github.com/Broodrix/QuefeX
```

See also `CITATION.cff` and `docs/WHITEPAPER.md`.

---

## Contact

**Broodrix** — GitHub and Hugging Face under the same name.  
Commercial or research inquiries: use profile contact channels.

---

Copyright (c) 2026 **Broodrix**. All Rights Reserved.  
See [LICENSE](LICENSE).
