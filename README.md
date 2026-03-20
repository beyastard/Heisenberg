# Heisenberg Architecture

> *"Greater certainty about the current belief state necessarily implies lesser sensitivity to new observations — and vice versa. The Kalman gain mediates this trade-off exactly, making it formally isomorphic to Heisenberg's uncertainty principle applied to neural computation."*

Heisenberg is a novel language model architecture combining entropy-based dynamic patching, a Parallax-inspired dual-track selective scan backbone, a Kalman-filtered probabilistic belief state, and interleaved sparse attention for cross-positional binding. It operates at the character level with no tokenizer, no subword vocabulary, and linear-time sequence processing.

## Design Philosophy

Heisenberg is built around four core principles:

**1. No tokenizer bias.** The model operates directly on characters. Every character in every language maps to exactly one slot in a fixed vocabulary. There are no subword merges, no coverage gaps, no fertility disparity between languages. Chinese characters are single morphemic units, as the writing system intends.

**2. Linear-time sequence processing.** The selective scan processes sequences in O(n) time and O(1) recurrent memory. There is no attention matrix across the full sequence. Doubling sequence length doubles compute — not quadruples it. This makes character-level modelling computationally viable at practical sequence lengths.

**3. Explicit epistemic state.** Every other neural architecture represents hidden state as a point estimate — a single vector encoding what the model believes. Heisenberg represents hidden state as a probability distribution — a mean vector and a diagonal covariance encoding both what the model believes and how confident it is. This uncertainty is a first-class computational citizen that governs routing, gating, and temporal dynamics.

**4. Semantically grounded patches.** Rather than fixed-stride convolution over raw characters, Heisenberg uses a learned seed Transformer to identify patch boundaries at high-entropy positions — word endings, punctuation, morpheme boundaries. The downstream scan processes semantically coherent units rather than arbitrary fixed-length windows.

---

*Heisenberg is an active research architecture. Training experiments are ongoing. Results will be updated as they become available. The codebase is structured for experimentation — the modular uncertainty estimator, configurable attention ratio, and adjustable patch parameters are all designed to support ablation studies.*
