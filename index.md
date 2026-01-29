---
layout: default
title: Image Deraining for Scene Text
---

## Qualitative Results

This page provides qualitative visualization of an image deraining approach tailored for scene text recognition scenarios.

The goal of this visualization is to support qualitative evaluation under rainy conditions.  
No quantitative metrics or implementation details are included.

---

## 🖼️ 实验结果展示 (Results Preview)

<p align="center">
  <img src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/rain_t1.png" width="45%" alt="Input Rainy Image">
  <img src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/derain_t1.png" width="45%" alt="Derained Result">
</p>

---

## 🚀 交互式去雨效果对比 (Interactive Slider)

<style>
/* ===============================
   Before / After Slider (Auto-fit)
   - No cropping (contain)
   - Container height follows image
   =============================== */

.ba-wrap{
  max-width: 980px;
  margin: 24px auto 40px;
}

.ba-title{
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 10px;
}

.ba{
  position: relative;
  width: 100%;
  border-radius: 12px;
  border: 1px solid #ddd;
  overflow: hidden;
  background: #000; /* keep clean when aspect differs */
}

/* BEFORE image: in normal flow, determines container height */
.ba img.before{
  position: relative;
  width: 100%;
  height: auto;
  display: block;
  object-fit: contain;
  user-select: none;
}

/* AFTER image: overlay, does not affect layout */
.ba img.after{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;           /* no cropping */
  clip-path: inset(0 0 0 50%);   /* initial 50% */
  user-select: none;
  pointer-events: none;
}

/* Slider (invisible but draggable) */
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
    const slider  = ba.querySelector('input[type="range"]');
    const after   = ba.querySelector("img.after");
    const divider = ba.querySelector(".divider");
    const knob    = ba.querySelector(".knob");

    const update = (v) => {
      after.style.clipPath = `inset(0 0 0 ${v}%)`;
      divider.style.left = v + "%";
      knob.style.left = v + "%";
    };

    update(slider.value);
    slider.addEventListener("input", (e) => update(e.target.value));
  });
});
</script>

<div class="ba-wrap">
  <div class="ba-title">Example 1</div>

  <div class="ba">
    <!-- BEFORE (Rainy) - determines height -->
    <img class="before"
         src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/rain_t1.png"
         alt="Rainy image">

    <!-- AFTER (De-rained) - overlay -->
    <img class="after"
         src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/derain_t1.png"
         alt="De-rained image">

    <div class="label before">Rainy</div>
    <div class="label after">De-rained</div>

    <div class="divider"></div>
    <div class="knob">↔</div>
    <input type="range" min="0" max="100" value="50" aria-label="Before/After slider">
  </div>
</div>
