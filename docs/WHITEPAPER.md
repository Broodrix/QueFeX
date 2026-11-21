# WHITEPAPER — QuefeX (Public Claim)

**Product:** QuefeX  
**Architecture:** RHMoE / RHMoE-GDM  
**Author:** Broodrix  
**Date of this public claim text:** 2026-11-21  
**Status:** Proprietary — implementation not published  

---

## 1. Classification

QuefeX is **not** marketed as a Transformer LLM and **not** as a pure SSM/Mamba
model. It is defined as:

**RHMoE** — Recurrent Hypercube Mixture-of-Experts  

with an optional memory configuration:

**RHMoE-GDM** — RHMoE + Gated Delta Memory  

Composition:

1. **Gated Convex Recurrence (GCR)** — per-layer recurrent state  
2. **Hypercube-Partner Routing (HPR)** — experts on a hypercube lattice with partner blocking  
3. **Optional Gated Delta Memory (GDM)** — fixed-rank associative memory, O(1) in sequence length  

Design intent: **phone-native training and inference** (full BPTT under a measured RAM budget), with later desktop Linux adaptation.

## 2. Conceptual equation (per token, per layer)

Informational description only (not an SDK):

- Gate mixes previous state and current input (GCR).  
- Normalized state feeds a router over \(2^{n_{\text{bits}}}\) experts (QuefeX Cube).  
- Top-k experts plus partner contributions on the active axis (HPR).  
- Optional memory read/write with separate erase and write gates (GDM).  
- Residual combination into the next state; tied vocabulary head at the stack output.  

Backward training is defined as exact BPTT through time and depth for the
published design, including memory carry when GDM is enabled.

## 3. Systems position

| Aspect | Claim |
|--------|--------|
| Sequence state | O(1) (recurrent ± fixed-rank memory) |
| Parameter scale | On the order of 5–30 M (preset-dependent) |
| Tokenizer design | Byte-lossless BPE (BLB) — no `<unk>` by construction |
| Primary platform | Android Termux (Galaxy-class devices) |
| Secondary platform | Modest Linux desktops (planned) |
| Distribution formats | `.qhb` (native), `.qfx` (portable) — Broodrix formats |

## 4. What this document is not

- Not a source release  
- Not a weight release  
- Not a license to reimplement under the QuefeX or RHMoE names for commercial use without permission  

## 5. Attribution

```text
Broodrix (2026). QuefeX: RHMoE — Recurrent Hypercube Mixture-of-Experts
(with optional RHMoE-GDM). Public claim documentation.
```

Copyright (c) 2026 Broodrix. All Rights Reserved.
