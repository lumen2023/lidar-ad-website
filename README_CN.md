# LIDAR-AD：面向自动驾驶的无解码器潜在交互 Dreamer 与残差动作链

[![Project Page](https://img.shields.io/badge/🌐-项目主页-blue?style=flat-square)](https://lumen2023.github.io/lidar-ad-website/)
[![Paper](https://img.shields.io/badge/📄-审稿中-red?style=flat-square)]()
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey?style=flat-square)](https://creativecommons.org/licenses/by-sa/4.0/)

**刘永志 · 许锦昌 · 康增 · 张苏楠 · 庄伟超**

东南大学 机械工程学院 · 南京 211189

📧 [yongzhiliu@seu.edu.cn](mailto:yongzhiliu@seu.edu.cn) · [wezhuang@seu.edu.cn](mailto:wezhuang@seu.edu.cn)（通讯作者）

> 🏷️ **审稿中** — IEEE Transactions on Knowledge and Data Engineering (TKDE)

---

## 📄 摘要

自动驾驶需要在高度动态的交通环境中进行长时序闭环决策。潜在世界模型通过在紧凑潜在空间中进行想象力推演，为此问题提供了有效框架。然而，多源驾驶观测中包含大量与控制任务无关的冗余信息，而可靠决策依赖于风险相关的关系和未来动态。此外，车辆控制是连续且增量式演化的，这要求模型捕捉动作调整及其多步效应。

我们提出 **LIDAR-AD**——一种无需解码器、基于潜在交互感知与**残差动作链**的 Dreamer 模型。LIDAR-AD 不重建观测，而是通过**去冗余对齐**学习紧凑潜在表征，聚焦多源驾驶输入中与风险相关的交互关系。为捕捉车辆控制的连续性与增量性，LIDAR-AD 将策略输出形式化为**残差动作更新**，并引入**残差动作链对比学习**，从动作序列中提取时序依赖以支撑多步连续决策。

在 MetaDrive 和 nuPlan 上的大量实验表明，LIDAR-AD 一致且显著地优于强基线，取得最高奖励与最佳成功率。

---

## 🔑 核心贡献

1. **无解码器潜在交互表征（DLIR）** — 对多源观测（自车状态、LiDAR、导航地图）进行门控融合与去冗余对齐，无需观测重建

2. **残差动作世界模型（RAWM）** — 策略输出重新形式化为残差更新，联合动作嵌入同时捕捉当前动作及其调整量

3. **残差动作链对比学习（ARC-CL）** — K 步动作链对比学习，利用未来动作序列约束先验 rollout 动态

---

## 🧠 方法

### 整体框架

<p align="center">
  <img src="static/images/LIDAR-AD/01_framework.png" alt="LIDAR-AD 框架" width="92%">
</p>

LIDAR-AD 围绕共享 RSSM 状态 $s_t = (h_t, z_t)$ 统一三个模块：

| 模块 | 功能 |
|------|------|
| **DLIR** | 将异构观测编码为风险感知的潜在表征，**无需重建** |
| **RAWM** | 通过**残差调整**与联合动作嵌入建模连续控制 |
| **ARC-CL** | 通过**动作链对比学习**强制执行多步时序一致性 |

### DLIR — 去冗余对齐

<p align="center">
  <img src="static/images/LIDAR-AD/02_DLIR-framework.png" alt="DLIR 架构" width="92%">
</p>

DLIR 显式建模三类异构观测间的交互：

1. **分组编码** — 自车状态、LiDAR 点云、导航地图分别编码
2. **跨模态交互** — 双线性注意力捕捉模态间关系
3. **标量门控** — 可学习门 $\alpha_t^k$ 自适应加权各模态贡献
4. **去冗余对齐** — Barlow Twins 目标消除跨模态冗余，保留风险相关特征

### RAWM — 残差动作建模

<p align="center">
  <img src="static/images/LIDAR-AD/04_COA_framework.png" alt="RAWM 架构" width="72%">
</p>

RAWM 将策略形式化为残差更新而非绝对动作：

$$u_t = u_{t-1} + \alpha \cdot \Delta u_t, \quad \Delta u_t \sim \pi_\theta(\cdot \mid s_t, u_{t-1})$$

$$a_t = \tanh(u_t), \quad d_t = E_\text{act}([a_t; \Delta u_t])$$

**latent-tanh** 参数化将平滑长时域控制表示为紧凑局部更新，与真实驾驶数据中残差动作的集中性一致。

---

## 📊 实验结果

### 训练曲线

<p align="center">
  <img src="static/images/LIDAR-AD/05_traing_curve.png" alt="训练曲线" width="92%">
</p>

LIDAR-AD 收敛更快且最终性能高于所有对比基线。

### 分布外泛化

<p align="center">
  <img src="static/images/LIDAR-AD/06_OOD-Mixed.png" alt="OOD 混合交通" width="30%">
  <img src="static/images/LIDAR-AD/06_OOD-roundout.png" alt="OOD 环岛" width="30%">
  <img src="static/images/LIDAR-AD/06_OOD-T-intersection.png" alt="OOD T型路口" width="30%">
</p>

在未见过的交通密度和道路布局上展现出强零样本泛化能力。

### 潜在表征分析 & 消融

<table>
<tr>
  <td width="33%"><img src="static/images/LIDAR-AD/07_barlow_representation.png" width="100%"><br><em>Barlow 表征分析</em></td>
  <td width="33%"><img src="static/images/LIDAR-AD/08_ablation_performance_spectrum.png" width="100%"><br><em>消融性能谱</em></td>
  <td width="33%"><img src="static/images/LIDAR-AD/09_action_comparison.png" width="100%"><br><em>控制平滑度对比</em></td>
</tr>
</table>

### 风险场可视化

<p align="center">
  <img src="static/images/LIDAR-AD/03_driving_risk_field.png" alt="风险场" width="80%">
</p>

无解码器表征实现风险感知场景理解——习得的风险场自适应地高亮碰撞相关区域。

---

## 🎥 驾驶演示

> 💡 点击视频播放。访问[项目主页](https://lumen2023.github.io/lidar-ad-website/)查看交互式对比。

### 🚗 MetaDrive — 混合交通

<table>
<tr>
  <td width="33%"><b>LIDAR-AD（本方法）</b></td>
  <td width="33%"><b>基线 — Case 1</b></td>
  <td width="33%"><b>基线 — Case 2</b></td>
</tr>
<tr>
  <td><video src="static/videos/metadrive-scene/mixed/LIDAR-AD_seed100_mix_density0.4.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/mixed/lattice_front_frames_3eds_ep002_seed147.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/mixed/lattice_front_frames_3eds_ep006_seed139.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

### 🔄 MetaDrive — 环岛

<table>
<tr>
  <td width="33%"><b>Case 1</b></td>
  <td width="33%"><b>Case 2</b></td>
  <td width="33%"><b>Case 3</b></td>
</tr>
<tr>
  <td><video src="static/videos/metadrive-scene/roundout/0.5/ep000_seed1000.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/roundout/0.5/ep002_seed1002.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/roundout/0.5/ep003_seed1003.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

### ⛔ MetaDrive — T 型路口

<table>
<tr>
  <td width="33%"><b>Case 1</b></td>
  <td width="33%"><b>Case 2</b></td>
  <td width="33%"><b>Case 3</b></td>
</tr>
<tr>
  <td><video src="static/videos/metadrive-scene/T-intersection/ep000_seed1000.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/T-intersection/ep002_seed1002.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/metadrive-scene/T-intersection/ep005_seed1000.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

### 🗺️ nuPlan — 前视图

<table>
<tr>
  <td width="33%"><b>Case 1</b></td>
  <td width="33%"><b>Case 2</b></td>
  <td width="33%"><b>Case 3</b></td>
</tr>
<tr>
  <td><video src="static/videos/nuplan/render1/front.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/nuplan/render2/front.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/nuplan/render3/front.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

### 🗺️ nuPlan — 鸟瞰图 (BEV)

<table>
<tr>
  <td width="33%"><b>Case 1</b></td>
  <td width="33%"><b>Case 2</b></td>
  <td width="33%"><b>Case 3</b></td>
</tr>
<tr>
  <td><video src="static/videos/nuplan/render1/bev.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/nuplan/render2/bev.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/nuplan/render3/bev.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

### ⚡ 风险场动态

<table>
<tr>
  <td width="33%"><b>Case 1</b></td>
  <td width="33%"><b>Case 2</b></td>
  <td width="33%"><b>Case 3</b></td>
</tr>
<tr>
  <td><video src="static/videos/risk_field/215BDA927CCDA3160BC32E46FB5FC41E.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/risk_field/7CB3BFDE3334D633DF36E6764335B96E.mp4" controls muted loop width="100%" preload="metadata"></video></td>
  <td><video src="static/videos/risk_field/B2DD5AD354955C4EBBF863EB99DF52BF.mp4" controls muted loop width="100%" preload="metadata"></video></td>
</tr>
</table>

---

## 🗂️ 项目结构

```
.
├── index.html                         # 项目主页
├── static/
│   ├── css/                           # 样式文件
│   ├── js/                            # 交互脚本
│   ├── images/LIDAR-AD/               # 13 张图片与示意图
│   └── videos/                        # 18 个驾驶演示 (MP4)
│       ├── metadrive-scene/           #   mixed / roundabout / T-intersection
│       ├── nuplan/                    #   front-view + BEV
│       └── risk_field/                #   风险场动态
└── README.md
```

## 🖥️ 本地开发

```bash
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

---

## 📝 引用

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

项目主页：[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)。代码与模型：另行发布。

## 🙏 致谢

主页模板基于 [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template) 和 [Nerfies](https://nerfies.github.io/) 修改。
