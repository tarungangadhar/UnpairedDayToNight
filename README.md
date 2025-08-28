# Day-to-Night Translation using CycleGAN

**Author:** Tarun Gangadhar Vadaparthi  
**Report:** [UnpairedDayToNight.pdf](docs/UnpairedDayToNight.pdf)  
**Colab Notebook:** [Open in Colab](https://colab.research.google.com/drive/1ezn_tiMShosXUccKUCosbrBKKuUjvsQW?usp=sharing)  
**Project Website:** [View Website](https://tarungangadhar.github.io/day-to-night-cycleGAN/)

---

##  Abstract
This project explores **unpaired image-to-image translation** for converting **daytime driving scenes into nighttime equivalents** using **CycleGAN**. Unlike paired supervised methods, CycleGAN leverages cycle-consistency and adversarial training to learn mappings between **Day ↔ Night** domains without requiring aligned image pairs.  
The goal is to enhance datasets for autonomous driving research where night data is limited.

---

##  Method

- **Architecture:** CycleGAN (two generators + two discriminators)
- **Adversarial Objective:** Least-Squares GAN (LSGAN) loss
- **Cycle Consistency:** Enforces forward–backward consistency (`Day → Night → Day`)
- **Identity Loss:** Encourages generators to preserve color mapping when given images from the target domain
- **Dataset:** BDD100K (10k subset). Day/Night domain split was generated using **luminance-based heuristics**.
- **Implementation:** PyTorch, trained with Adam optimizer (`lr=0.0002`)


---

## Results

### Quantitative Performance
- **Day → Night (A→B):**  
  - SSIM: **0.80 – 0.86**  
  - PSNR: **~25 dB**  
  - LPIPS: **0.18 – 0.22**

- **Night → Day (B→A):**  
  - SSIM: **~0.82 avg**  
  - PSNR: **mid-20 dB range**  
  - LPIPS: **~0.18 – 0.22**

**Histograms of Metrics (A→B and B→A):**

<div align="center">
  <img src="assets/metricshist.png" alt="Histograms of SSIM, PSNR, LPIPS for A→B and B→A" width="850">
</div>

---

### Trends Across Epochs

Cycle consistency improves steadily over training:
- SSIM rises into the low–mid 0.8s  
- PSNR increases into the mid-20 dB range  
- LPIPS drops to ~0.20  

<div align="center">
  <img src="assets/metricsepochs.png" alt="SSIM, PSNR, LPIPS trends across epochs" width="850">
</div>

---

### Qualitative Results

| Input (Day) | Generated (Night) |
|-------------|-------------------|
| ![Day](assets/sampleday.png) | ![Night](assets/samplenight.png) |

| Input (Night) | Generated (Day) |
|-------------|-------------------|
| ![Day](assets/samplenight1.png) | ![Night](assets/sampleday1.png) |



