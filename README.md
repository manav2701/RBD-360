# RBD-360: A Realistic Benchmark for Quality Analysis of Distorted 360° Videos 
**Public dataset will be available soon**

## Authors
Manav Arun Mehta, Pramit Mazumdar,  Kalyan Chatterjee, Sweta Dey, Mudassir Khan, Raja Shekar Kadurka

## Abstract

User-generated 360° video content is becoming increasingly popular due to the availability of low-cost acquisition devices and its inherently immersive nature. To facilitate research and development in this area, we introduce **RBD-360**, a dataset designed explicitly for quality assessment of user-generated 360° videos that includes various distortions typical of non-professional settings.

RBD-360 features a collection of randomly captured source videos across multiple categories, recorded in three different environments: **indoor**, **outdoor-day**, and **outdoor-night**. The impaired video sequences are created using three standard codecs—**H.264**, **H.265**, and **VP9**—at varying bitrates and quantization parameters.

To evaluate subjective video quality, we employed an **HMD-based Modified Absolute Category Rating (ACR)** protocol, along with assessments from the **Simulator Sickness Questionnaire (SSQ)**. This setup captures time-dependent viewer discomfort in accordance with **ITU-T P.919 recommendations**.

We implement benchmark quality assessment metrics on the RBD-360 dataset and report the results. The dataset is publicly available for testing quality assessment models tailored for user-generated 360° videos.

## Usage
The RUG360 dataset is intended for research in **video quality assessment (VQA), quality of experience (QoE), and immersive media analysis**. Researchers can use this dataset to:
1. Benchmark their video quality models.
2. Train and evaluate new VQA algorithms.
3. Study the impact of real-world distortions in 360° videos.
# Reproducibility

All experiments can be reproduced using the software versions and commands listed below. The evaluation pipeline is fully scripted (`evaluate.sh`, provided in this repository).

---

## Software environment

| Tool | Version | Purpose |
|------|---------|---------|
| FFmpeg | 7.0.3 | Encoding (H.264, H.265, VP9) and decoding |
| libvmaf | 3.0.0 | VMAF, PSNR, SSIM computation |
| Python | 3.11+ | Result aggregation and plotting |

> **Note on FFmpeg build:** libvmaf support must be compiled in. Build with `--enable-libvmaf` and link against libvmaf ≥ 3.0.0. A pre-built static binary will not include this by default.

---

## Encoder presets

### H.264 (libx264)
```
-c:v libx264 -preset medium -crf <QP>
```

### H.265 (libx265)
```
-c:v libx265 -preset medium -crf <QP>
```

### VP9 (libvpx-vp9)
```
-c:v libvpx-vp9 -deadline good -cpu-used 2 -b:v 0 -crf <QP>
```

QP values used: **22, 32, 42**. Bitrate targets used: **500, 1500, 3000 kbps**.

---

## Evaluation pipeline

Run `evaluate.sh` from the repository root. It expects source sequences in `./sequences/` as raw YUV files and writes per-clip JSON results to `./results/`.

```bash
bash evaluate.sh
```

To verify your tool versions before running:

```bash
ffmpeg -version | head -1
ffmpeg -filters | grep vmaf
```

---

## Affiliations

1. **Department of Computer Science & Engineering**  
   Indian Institute of Information Technology Vadodara, India  

2. **Department of Computer Science & Engineering**  
   Indian Institute of Technology Kharagpur, India  

3. **Department of Computer Science & Engineering**  
   College of Computer Science, Applied College Tanumah  
   King Khalid University, Abha, Saudi Arabia  

4. **Senior Data Scientist**  
   Toyota Motor North America, Plano, Texas, USA  

## Contact
For any inquiries regarding the dataset, please contact the authors at **[202252344@iiitvadodara.ac.in]**.

