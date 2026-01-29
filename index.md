---
layout: default
title: Image Deraining for Scene Text
---

## Qualitative Visualization

This page presents qualitative visualization results of an image deraining approach designed for scene text recognition under rainy conditions.  
All results are shown for qualitative comparison only.

---

## 🖼️ Results Preview

<p align="center">
  <img src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/rain_t1.png" width="45%" alt="Rainy Image">
  <img src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/derain_t1.png" width="45%" alt="De-rained Result">
</p>

---

## 🚀 Interactive Before / After Slider

<style>
/* ===============================
   Before / After Slider (Final)
   - frame size follows image
   - no cropping
   - minimal blank space
   =============================== */

.ba-wrap{
  max-width: 540px;
  margin: 24px auto 40px;
}

.ba-title{
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 10px;
}

/* outer container: no border here */
.ba{
  position: relative;
  width: 100%;
}

/* inner frame: border matches image size */
.ba .frame{
  position: relative;
  width: 100%;
  border: 1.5px dashed #bbb;   /* 灰色虚线框 */
  border-radius: 12px;
  overflow: hidden;
  background: #000;
}

/* BEFORE image: determines frame height */
.ba img.before{
  position: relative;
  width: 100%;
  height: auto;
  display: block;
  object-fit: contain;
  user-select: none;
}

/* AFTER image: overlay for slider */
.ba img.after{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
  clip-path: inset(0 0 0 50%);
  user-select: none;
  pointer-events: none;
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
    const slider  = ba.querySelector('input[type="range"]');
    const after   = ba.querySelector("img.after");
    const divider = ba.querySelector(".divider");
    const knob    = ba.querySelector(".knob");

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

<div class="ba-wrap">
  <div class="ba-title">Example 1</div>

  <div class="ba">
    <div class="frame">
      <!-- BEFORE -->
      <img class="before"
           src="https://github.com/Heaviside80/deraining-for-scene-text/raw/main/assets/rain_t1.png"
           alt="Rainy image">

      <!-- AFTER -->
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
</div>
