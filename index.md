---
layout: default
title: Image-Deraining 研究主页
description: 记录图像去雨领域的科研进展、复现笔记与性能评测。
---

# 🌧️ Image-Deraining 研究库

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Stars](https://img.shields.io/github/stars/你的用户名/Image-Deraining?style=social)

## 🖼️ 实验结果展示 (Results Preview)

<p align="center">
  <img src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/images.jpeg" width="45%" title="Input Rainy Image">
  <img src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/images.jpeg" width="45%" title="Derained Result">
</p>

## 🚀 交互式去雨效果对比 (Interactive Slider)

---
layout: default
title: Image De-raining Demo
---

# Image De-raining Results

Drag the slider to compare the rainy image and the de-rained result.

<style>
/* ===============================
   Before / After Slider (Display)
   =============================== */

.ba-wrap{
  max-width: 900px;
  margin: 32px auto;
}

.ba-title{
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 10px;
}

.ba{
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 9;        /* 固定展示比例 */
  overflow: hidden;
  border-radius: 12px;
  border: 1px solid #ddd;
  background: #000;
}

/* 强制前端压缩，不依赖原图尺寸 */
.ba img{
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;           /* 仅展示用 */
  user-select: none;
  pointer-events: none;
}

.ba .after{
  clip-path: inset(0 0 0 50%);
}

/* Slider */
.ba input[type="range"]{
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: ew-resize;
  margin: 0;
}

/* Divider line */
.ba .divider{
  position: absolute;
  top: 0;
  left: 50%;
  width: 3px;
  height: 100%;
  background: #fff;
  transform: translateX(-1.5px);
  pointer-events: none;
}

/* Slider knob */
.ba .knob{
  position: absolute;
  top: 50%;
  left: 50%;
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: #fff;
  color: #000;
  font-size: 18px;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translate(-50%, -50%);
  pointer-events: none;
  box-shadow: 0 6px 18px rgba(0,0,0,0.25);
}

/* Labels */
.ba .label{
  position: absolute;
  top: 10px;
  padding: 6px 10px;
  font-size: 12px;
  border-radius: 999px;
  background: rgba(0,0,0,0.55);
  color: #fff;
  pointer-events: none;
}

.ba .label.before{ left: 10px; }
.ba .label.after{ right: 10px; }
</style>

<script>
document.addEventListener("DOMContentLoaded", () => {
  document.querySelectorAll(".ba").forEach(ba => {
    const slider = ba.querySelector("input");
    const after = ba.querySelector(".after");
    const divider = ba.querySelector(".divider");
    const knob = ba.querySelector(".knob");

    const update = v => {
      after.style.clipPath = `inset(0 0 0 ${v}%)`;
      divider.style.left = v + "%";
      knob.style.left = v + "%";
    };

    update(slider.value);
    slider.addEventListener("input", e => update(e.target.value));
  });
});
</script>

---

## Example 1

<div class="ba-wrap">
  <div class="ba-title">Rainy vs De-rained</div>
  <div class="ba">
    <!-- Before (Rainy) -->
    <img
      src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/images.jpeg"
      alt="Rainy image">

    <!-- After (De-rained) -->
    <img class="after"
      src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/treasure.png"
      alt="De-rained image">

    <div class="label before">Rainy</div>
    <div class="label after">Ours</div>

    <div class="divider"></div>
    <div class="knob">↔</div>
    <input type="range" min="0" max="100" value="50">
  </div>
</div>

---

## Example 2

<div class="ba-wrap">
  <div class="ba-title">Another Scene</div>
  <div class="ba">
    <img src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/images.jpeg">
    <img class="after" src="https://github.com/Heaviside80/Image-Deraining/raw/main/assets/images.jpeg">
    <div class="label before">Rainy</div>
    <div class="label after">Ours</div>
    <div class="divider"></div>
    <div class="knob">↔</div>
    <input type="range" min="0" max="100" value="50">
  </div>
</div>



## 📖 项目简介
本项目致力于构建一个系统化的图像去雨学习路径。我们不仅关注传统的物理模型，更紧跟深度学习前沿（CNN, Transformer, Mamba）。

## 📂 快速跳转
- [📚 文献精读笔记](./Papers/) - 包含 DDN, PReNet, Restormer 等。
- [📊 实验性能对比](./Papers/#benchmark) - 统一数据集下的 PSNR/SSIM 表现。
- [🛠️ 开发工具库](./Utils/) - 包含图像质量评价脚本。
- [📅 数据集获取](./Datasets/) - 常用去雨数据集汇总。

## 🛠️ 环境要求
```bash
pip install -r requirements.txt
