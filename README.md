<div align="center">

# OmniVL-Guard Pro: A Tool-Augmented Agent for Omnibus Vision-Language Forensics

<a href="http://arxiv.org/abs/2605.16962"><img src="https://img.shields.io/badge/Paper-arXiv:2605.16962-b31b1b.svg" alt="arXiv"></a>
<a href="https://github.com/shen8424/OmniVL-Guard-Pro"><img src="https://img.shields.io/badge/GitHub-OmniVL--Guard--Pro-181717.svg?logo=github" alt="GitHub"></a>
<a href="#"><img src="https://img.shields.io/badge/Status-Under%20Review-orange.svg" alt="Under Review"></a>

</div>

---

## ⚠️ Availability

> This work is currently **under review**. The **FSTR (Full-Spectrum Tool Reasoning)** dataset, trained model weights, and the complete codebase will be publicly released upon acceptance. Stay tuned!

---

## 📖 Introduction

Existing vision-language forgery detection and grounding methods operate under a **closed-world** paradigm, assuming verification can be completed by the model alone. However, self-contained MLLMs are constrained by finite parametric knowledge, static training corpora, and limited perceptual resolution — creating a practical ceiling in dynamic open-world forensics.

**OmniVL-Guard Pro** breaks this ceiling by shifting from *scaling up* the self-contained model to *reaching beyond* it. It is a **tool-augmented agent** that extends unified forensics from closed-world prediction to open-world, evidence-driven reasoning across **text, image, and video** modalities.


---

## 🔗 Related Work: OmniVL-Guard

**OmniVL-Guard** (ICML 2026) is the first unified framework for vision-language forgery detection and grounding across image, text, and video modalities. OmniVL-Guard Pro builds upon this foundation, extending from closed-world prediction to open-world tool-augmented reasoning.

- **Paper:** [arXiv:2602.10687](https://arxiv.org/abs/2602.10687)
- **GitHub:** [OmniVL-Guard](https://github.com/shen8424/OmniVL-Guard)

---

## 🌟 Key Features

- **Open-World Forensic Agent:** Dynamically retrieves real-time event clues and invokes specialized perception tools, transcending the intrinsic limits of the base MLLM.
- **Rich Tool Environment:** Integrates real-time event search, local cropping & zooming, edge-anomaly screening, face detection, video frame extraction, and SAM3-based segmentation.
- **FSTR Dataset:** A large-scale *Full-Spectrum Tool Reasoning* dataset constructed via **Tree-Structured Self-Evolving Tool Trajectory Generation**, providing high-quality cold-start data for tool-augmented RL.
- **Checker-Guided Agentic RL (CGARL):** Introduces process-level supervision via a Multi-Agent Checker, penalizing the pseudo-success pattern where the *answer is correct but the reasoning is distorted*.
- **State-of-the-Art Performance:** Achieves strong in-domain results and robust zero-shot generalization across diverse forensic benchmarks.

---

## 🏗️ Method Overview

OmniVL-Guard Pro consists of three core components:

### 1. Tool-Enhanced Environment

To enable open-world evidence acquisition, we construct a tool environment spanning:
- **Real-time event search** — web retrieval for fact verification
- **Local cropping & zooming** — fine-grained inspection of candidate regions
- **Edge-anomaly screening** — automatic detection of boundary/texture anomalies
- **Face detection** — facial region inspection for portrait media
- **Video frame extraction** — temporal clip parsing for video forensics
- **SAM3 segmentation** — pixel-level mask generation for forgery localization

### 2. Tree-Structured Self-Evolving Tool Trajectory Generation

Constructing tool-reasoning trajectories faces an *efficiency-bias dilemma*: free exploration yields low-quality data, while answer-aware guidance introduces hindsight bias. Our solution proceeds in stages:

| Stage | Description |
| :--- | :--- |
| 🌱 **Seed Guidance** | Tree-structured search with MLLM expert pool (Explorer + Guider) for high-fidelity trajectories |
| 🌿 **Self-Evolution** | Guider-free expansion to scale up trajectory diversity |
| 🪨 **Hard Sample Synthesis** | Weakly-hinted generation for long-tail challenging cases |

The resulting **FSTR** dataset provides both cold-start SFT data ($\mathrm{FSTR}_{\mathrm{sft}}$) and RL training data ($\mathrm{FSTR}_{\mathrm{rl}}$).

### 3. Checker-Guided Agentic RL (CGARL)

Beyond teaching the model to invoke tools, CGARL ensures the model genuinely organizes reasoning around evidence. A **Checker** agent provides process-level supervision, explicitly verifying that intermediate tool calls, observations, and final judgments form a consistent and verifiable support relation.

---

## 📝 Citation

If you find this work helpful, please consider citing:

```bibtex
@article{shen2026omnivlguardpro,
  title={OmniVL-Guard Pro: A Tool-Augmented Agent for Omnibus Vision-Language Forensics},
  author={Shen, Jinjie and Huang, Zheng and Zhang, Yuchen and Wu, Yujiao and 
          Wang, Yaxiong and Cheng, Lechao and Tang, Shengeng and Hui, Tianrui and 
          Pu, Nan and Zhong, Zhun},
  journal={arXiv preprint arXiv:2605.16962},
  year={2026}
}
```
