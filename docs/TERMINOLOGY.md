# QuefeX Terminology

**Rights holder:** Broodrix  
**Product:** QuefeX  
**Public claim documentation:** 2026-11-21  

## Architecture classification

**RHMoE** — *Recurrent Hypercube Mixture-of-Experts*

Optional memory variant: **RHMoE-GDM** — *RHMoE + Gated Delta Memory*.

One-line claim:

> QuefeX is an RHMoE language model: gated convex recurrence, hypercube-partner
> MoE routing, optional gated delta memory, designed for phone-native full BPTT.

## Coined terms (Broodrix)

| Term | Expansion | Meaning |
|------|-----------|---------|
| **RHMoE** | Recurrent Hypercube Mixture-of-Experts | Architecture class |
| **RHMoE-GDM** | RHMoE + Gated Delta Memory | RHMoE with associative memory |
| **HPR** | Hypercube-Partner Routing | Top-k + partner block on cube axis |
| **GCR** | Gated Convex Recurrence | Learned convex mix of state and input |
| **GDM** | Gated Delta Memory | Channel-wise erase/write delta memory |
| **QuefeX Cube** | — | \(2^{n_{\text{bits}}}\)-vertex expert lattice |
| **BLB** | Byte-Lossless BPE | Zero-`<unk>` byte-fallback tokenizer design |
| **PNT** | Phone-Native Training | Full on-device BPTT under RAM budget |

## File formats (custom, Broodrix)

| Extension | Name | Role |
|-----------|------|------|
| `.qhb` | QuefeX Hypercube Brain | Native brain / checkpoint package |
| `.qfx` | QuefeX Fusion eXport | Portable package between QuefeX installs |

Third-party “MNN” / “GGUF” style exports, when offered at all, are **notes only** — not substitute model files for foreign runtimes.

## Notice

These names and definitions are published so the architecture class and product
identity can be attributed to **Broodrix**. Implementation source and weights
remain proprietary and unpublished in public claim repositories.
