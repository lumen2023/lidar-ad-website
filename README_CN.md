# LIDAR-AD：面向自动驾驶的无解码器潜在交互 Dreamer 与残差动作链

[![Project Page](https://img.shields.io/badge/项目主页-在线-blue?style=flat-square)](https://lumen2023.github.io/lidar-ad-website/)
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg?style=flat-square)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Paper](https://img.shields.io/badge/论文-审稿中-red?style=flat-square)]()

**刘永志，许锦昌，康增，张苏楠，庄伟超**

东南大学 机械工程学院 · 南京 211189

📧 yongzhiliu@seu.edu.cn · 📧 wezhuang@seu.edu.cn（通讯作者）

**审稿中** · IEEE Transactions on Knowledge and Data Engineering (TKDE)

---

## 📄 摘要

自动驾驶需要在高度动态的交通环境中进行长时序闭环决策。潜在世界模型通过在紧凑潜在空间中进行想象力推演，为此问题提供了有效框架。然而，多源驾驶观测中包含大量与控制任务无关的冗余信息，而可靠的决策依赖于风险相关的关系和未来动态。此外，车辆控制是连续且增量式演化的，这要求模型能够捕捉动作调整及其多步效应。

我们提出 **LIDAR-AD**——一种无需解码器、基于潜在交互感知与残差动作链的 Dreamer 模型。LIDAR-AD 不重建观测，而是通过**去冗余对齐**学习紧凑的潜在表征，使模型聚焦于多源驾驶输入中与风险相关的交互关系。为更好地捕捉车辆控制的连续性与增量性，LIDAR-AD 将策略输出形式化为**残差动作更新**，并引入**残差动作链对比学习**，从残差动作序列中提取时序依赖以支撑多步连续决策。

在多种模拟驾驶场景上的大量实验表明，LIDAR-AD 一致且显著地优于强世界模型基线，取得了最高奖励和最佳成功率。在 nuPlan 基准上的评估进一步验证了该方法在真实世界驾驶数据上的有效性。

---

## 🔑 核心贡献

1. **无解码器潜在交互表征（DLIR）** — 通过对多源观测（自车状态、LiDAR 点云、导航地图）进行门控融合与去冗余对齐，消除观测重建，建立交互感知的潜在表征。

2. **残差动作世界模型（RAWM）** — 将策略重新形式化为残差更新而非绝对动作，通过联合动作嵌入同时捕捉当前动作及其调整量。

3. **残差动作链对比学习（ARC-CL）** — 引入 K 步动作链对比学习，利用未来动作序列作为正样本约束先验 rollout 动态。

---

## 🧠 方法概览

<p align="center">
  <img src="static/images/LIDAR-AD/01_framework.png" alt="LIDAR-AD 框架图" width="85%">
</p>

LIDAR-AD 包含三个共享统一 RSSM 潜在状态 $s_t = (h_t, z_t)$ 的核心模块：

| 模块       | 功能                                                      |
|------------|-----------------------------------------------------------|
| **DLIR**   | 将异构观测编码为风险感知的潜在表征，无需重建 |
| **RAWM**   | 通过残差调整与联合动作嵌入建模连续控制 |
| **ARC-CL**  | 通过对动作链的对比学习，强制执行多步时序一致性 |

---

## 🎥 驾驶演示

我们在多种驾驶场景中评估了 LIDAR-AD：

- **MetaDrive 模拟器** — 混合交通、环岛、T 型路口
- **nuPlan 基准** — 真实驾驶数据的前视图与鸟瞰视图
- **风险场可视化** — 复杂交通场景中习得的风险感知表征

👉 **[访问项目主页](https://lumen2023.github.io/lidar-ad-website/)** 查看交互式视频对比与消融研究。

---

## 📊 主要结果

在 MetaDrive 和 nuPlan 基准上的广泛实验表明：

- **任务性能优越** — LIDAR-AD 在学习型世界模型方法中取得最高的回合奖励和成功率
- **潜在表征质量更佳** — 无解码器表征提升风险感知能力与分布外泛化性能
- **控制更平滑** — 残差动作建模显著降低动作 jerk，提升轨迹平滑度
- **泛化能力强** — 在未见过的交通密度、道路布局和交互模式上均有一致提升

---

## 🗂️ 项目结构

```
.
├── index.html              # 项目主页
├── static/
│   ├── css/                # 样式文件 (Bulma, Font Awesome, 自定义)
│   ├── js/                 # 交互脚本 (轮播图, BibTeX 复制等)
│   ├── images/LIDAR-AD/    # 图片与示意图
│   └── videos/             # 驾驶演示视频 (MP4)
│       ├── metadrive-scene/   # MetaDrive 场景
│       ├── nuplan/            # nuPlan 基准
│       └── risk_field/        # 风险场动态
└── README.md
```

---

## 🖥️ 本地开发

```bash
# 启动本地服务器
python3 -m http.server 8000

# 浏览器打开 http://localhost:8000
```

---

## 📝 引用

如果您觉得本工作有帮助，请引用：

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

## 📜 许可证

本项目主页采用 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) 许可。LIDAR-AD 代码和模型权重将另行发布。

---

## 🙏 致谢

本主页模板基于 [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template) 和 [Nerfies](https://nerfies.github.io/) 主页修改。
