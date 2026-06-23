# LIDAR-AD: A Decoder-Free Latent-Interaction Dreamer with Action-Residual Chains for Autonomous Driving

[![Project Page](https://img.shields.io/badge/Project-Page-blue?style=flat-square)](https://lumen2023.github.io/lidar-ad-website/)
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg?style=flat-square)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Paper](https://img.shields.io/badge/Paper-Under%20Review-red?style=flat-square)]()
[![Code](https://img.shields.io/badge/Code-Coming%20Soon-lightgrey?style=flat-square)]()

**Yongzhi Liu**, Jinchang Xu, Zeng Kang, Sunan Zhang, Weichao Zhuang

School of Mechanical Engineering, Southeast University, Nanjing 211189, China

📧 yongzhiliu@seu.edu.cn · 📧 wezhuang@seu.edu.cn (Corresponding Author)

**Under Review** · IEEE Transactions on Knowledge and Data Engineering (TKDE)

---

## 📄 Abstract

Autonomous driving requires long-horizon closed-loop decision making in highly dynamic traffic environments. Latent world models offer an effective framework by enabling imagination-based planning in compact latent spaces. However, multi-source driving observations contain substantial control-irrelevant redundancy, and reliable decisions depend on risk-relevant relations and future dynamics. Moreover, vehicle control evolves continuously and incrementally, requiring models to capture action adjustments and their multi-step consequences.

We propose **LIDAR-AD** — a decoder-free latent-interaction Dreamer with residual-action chains. Instead of reconstructing observations, LIDAR-AD learns compact latent representations through **de-redundancy alignment**, focusing on risk-relevant interactions across multi-source driving inputs. To better capture the continuity and incrementality of vehicle control, LIDAR-AD formulates policy outputs as **residual action updates** with a **residual-action chain contrastive learning** objective, extracting temporal dependencies from action sequences for multi-step continuous decision making. Deterministic analysis further demonstrates that the latent-tanh residual parameterization represents smooth, long-horizon driving control as compact local updates — consistent with the concentration of residual actions observed in real driving data.

Extensive experiments across diverse simulated driving scenarios demonstrate that LIDAR-AD consistently and significantly outperforms strong world-model baselines, achieving the highest reward and best success rates among learning-based methods. Evaluation on the nuPlan benchmark further validates the method's effectiveness on real-world driving data.

---

## 🔑 Key Contributions

1. **Decoder-Free Latent-Interaction Representation (DLIR)** — Eliminates observation reconstruction by structuring multi-source observations (ego-vehicle state, LiDAR point clouds, navigation maps) into interaction-aware latent representations via gated fusion and de-redundancy alignment.

2. **Residual Action World Model (RAWM)** — Reformulates the policy as residual updates rather than absolute actions, with joint action embeddings that capture both current actions and their adjustments.

3. **Action-Residual Chain Contrastive Learning (ARC-CL)** — Introduces K-step action chain contrastive learning that constrains the prior rollout dynamics using future action sequences as positive pairs.

---

## 🧠 Method Overview

<p align="center">
  <img src="static/images/LIDAR-AD/01_framework.png" alt="LIDAR-AD Framework" width="85%">
</p>

LIDAR-AD consists of three core modules sharing a unified RSSM latent state $s_t = (h_t, z_t)$:

| Module       | Role                                                      |
|--------------|-----------------------------------------------------------|
| **DLIR**     | Encodes heterogeneous observations into risk-aware latent representations without reconstruction |
| **RAWM**     | Models continuous control as residual adjustments with joint action embeddings |
| **ARC-CL**   | Enforces multi-step temporal consistency through contrastive learning over action chains |

---

## 🎥 Driving Demonstrations

We evaluate LIDAR-AD across multiple driving scenarios:

- **MetaDrive Simulator** — Mixed traffic, roundabouts, T-intersections
- **nuPlan Benchmark** — Real-world driving data with front-view and bird's-eye-view perspectives
- **Risk Field Visualization** — Learned risk-aware representations in complex traffic

👉 **[Visit the project page](https://lumen2023.github.io/lidar-ad-website/)** for interactive video comparisons and ablation studies.

---

## 📊 Key Results

Extensive experiments on MetaDrive and nuPlan benchmarks demonstrate:

- **Superior task performance** — LIDAR-AD achieves the highest episode reward and success rate among learning-based world model methods
- **Better latent quality** — Decoder-free representations improve risk-awareness and generalization to out-of-distribution scenarios
- **Smoother control** — Residual action modeling significantly reduces action jerk and improves trajectory smoothness
- **Strong generalization** — Consistent gains across unseen traffic densities, road layouts, and interaction patterns

---

## 🗂️ Project Structure

```
.
├── index.html              # Main project page
├── static/
│   ├── css/                # Stylesheets (Bulma, Font Awesome, custom)
│   ├── js/                 # JavaScript (carousel, BibTeX copy, interactions)
│   ├── images/LIDAR-AD/    # Figures and diagrams
│   └── videos/             # Driving demonstration videos (MP4)
│       ├── metadrive-scene/   # MetaDrive scenarios
│       ├── nuplan/            # nuPlan benchmark
│       └── risk_field/        # Risk field dynamics
└── README.md
```

---

## 📝 Citation

If you find this work useful, please cite:

```bibtex
@article{liu2026lidarad,
  title   = {{LIDAR-AD}: A Decoder-Free Latent-Interaction Dreamer
             with Action-Residual Chains for Autonomous Driving},
  author  = {Liu, Yongzhi and Xu, Jinchang and Kang, Zeng
             and Zhang, Sunan and Zhuang, Weichao},
  journal = {IEEE Transactions on Knowledge and Data Engineering},
  note    = {Under Review},
  year    = {2026}
}
```

---

## 🖥️ Local Development

```bash
# Start a local server
python3 -m http.server 8000

# Then open http://localhost:8000
```

---

## 📜 License

This project page is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). The LIDAR-AD code and model weights will be released under a separate license.

---

## 🙏 Acknowledgments

This project page template is adapted from the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template) and the [Nerfies](https://nerfies.github.io/) project page.
