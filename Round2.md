Round 1 materials: [Tables 1–12, Figure 1 (README)](README.md)

**Reviewer qHqH**

- [Figure 2 – NFM Color Change Across Formats](#figure-2)
- [Table 13 – Blend Weight Strategy Ablation](#table-13)
- [Table 14 – Topology Stress Test](#table-14)
- [Figure 3 – Topology Reduction: 25J → 20J / 17J / 13J](#figure-3)
- [Figure 4 – DrAction Rendering Under Reduced Topologies](#figure-4)

**Reviewer 92aF**

- [Table 15 – All-Split Single/Two-Person Breakdown](#table-15)
- [Table 16 – Joint vs. Separate Rendering Ablation](#table-16)
- [Figure 5 – Joint Rendering vs. Separate Overlay](#figure-5)
- [Figure 6 – InternViT Attention: Separate vs. Joint](#figure-6)
- [Table 17 – End-to-End System Comparison](#table-17)
- [Table 18 – FPS Multi-Task Verification](#table-18)
- [Table 19 – MQA Protocol in Recent Open-Vocabulary Methods](#table-19)

---

<a id="figure-2"></a>

### Figure 2: NFM Color Change Across Formats

<img src="figs/nfm_change.png" alt="NFM Color Change Heatmap" style="zoom:40%;" />

<a id="table-13"></a>

### Table 13: Blend Weight Strategy Ablation (NTU-60 48/12 Xsub)

| Weight Strategy | NTU-60 48/12 | NTU-60→NW-UCLA | HumanML3D→NW-UCLA |
| :--- | :---: | :---: | :---: |
| (a) Uniform (w_k,j = 1/J) | 58.41 | 45.67 | 38.82 |
| (b) Distance (1/d^2) | 61.81 | 52.53 | 47.16 |
| (c) Learnable | 64.90 | 48.74 | 41.25 |
| **(d) Topology (Ours)** | 64.72 | 60.38 | 56.73 |

---

<a id="table-14"></a>

### Table 14: Topology Stress Test (train 25J, test reduced)

| Train → Test | Topology (Ours) | Uniform (1/J) | Distance (1/d^2) | Learnable |
| :--- | :---: | :---: | :---: | :---: |
| 25J (original) | 64.72 | 58.41 | 61.81 | 64.90 |
| 25J → 20J | 61.84 (−2.88) | 51.57 (−6.84) | 57.48 (−4.33) | 58.76 (−6.14) |
| 25J → 17J | 58.91 (−5.81) | 48.19 (−10.22) | 52.84 (−8.97) | 53.85 (−11.05) |
| 25J → 13J | 52.37 (−12.35) | 40.14 (−18.27) | 45.78 (−16.03) | 45.07 (−19.83) |

---

<a id="figure-3"></a>

### Figure 3: Topology Reduction (25J → 20J / 17J / 13J)

<img src="figs/tpose.png" alt="Topology Reduction" style="zoom:50%;" />

---

<a id="figure-4"></a>

### Figure 4: DrAction Rendering Under Reduced Topologies

<img src="figs/ntu_13j_vis.png" alt="Rendering under reduced topologies" style="zoom:30%;" />

---

<a id="table-15"></a>

### Table 15: Single-Person vs. Two-Person Accuracy (%) — All NTU-60 Splits

| Split | Action Type | SkeletonLLM | TDSM | PURLS |
| :--- | :--- | :---: | :---: | :---: |
| 55/5 | Single-person | 86.93 | 86.86 | 80.03 |
| 55/5 | Two-person | **89.14** (+2.21) | 85.01 (−1.85) | 75.99 (−4.04) |
| 48/12 | Single-person | 60.27 | 58.42 | 44.10 |
| 48/12 | Two-person | **75.37** (+15.10) | 50.85 (−7.57) | 34.23 (−9.87) |
| 40/20 | Single-person | 43.06 | 37.80 | 32.91 |
| 40/20 | Two-person | **55.42** (+12.36) | 30.97 (−6.83) | 25.49 (−7.42) |
| 30/30 | Single-person | 38.84 | 27.88 | 25.35 |
| 30/30 | Two-person | **35.84** (−3.00) | 21.87 (−6.01) | 19.85 (−5.50) |

---

<a id="table-16"></a>

### Table 16: Joint vs. Separate Rendering Ablation (NTU-60 48/12, two-person subset)

| Rendering Strategy | Two-Person Acc (%) | Δ vs. Joint |
| :--- | :---: | :---: |
| **Joint global compositing (Ours)** | **75.37** | — |
| Separate render                     |       67.14        |    −8.23    |

---

<a id="figure-5"></a>

### Figure 5: Joint Rendering vs. Separate Overlay on Two-Person Actions

<img src="figs/render_cmp.png" alt="Joint rendering vs separate overlay comparison" style="zoom:30%;" />

---

<a id="figure-6"></a>

### Figure 6: InternViT Attention — Separate vs. Joint Rendering

<img src="figs/atten_map.png" alt="ViT attention maps on multi-person scenes" style="zoom:30%;" />

---

<a id="table-17"></a>

### Table 17: End-to-End System Comparison

| Method | Bridge | Bridge Params / FLOPs | Vision Backbone Params/ FLOPs | LLM Backbone | Latency | Capability |
| :--- | :--- | :---: | :--- | :--- | :---: | :--- |
| CTR-GCN | Coord. encoder | 1.46M / 2.0G | — | — | **~10 ms** | Closed-set single-task |
| SUGAR | CTR-GCN + TQP | 189.46M / 225.1G | — | LLaMA2 -7B | N/A | Closed-set, single-format                    |
| **SkeletonLLM** | DrAction | **12.6K / 33.2G** | InternViT, 300M, 8.67T | Qwen2.5-7B | 191.6 ms | **Open-vocab + cross-format + caption + QA** |
| **+ FPS** | DrAction | 12.6K / 33.2G | InternViT, 300M, **1.41T** | Qwen2.5-7B | 97.3 ms | Same as above |

---

<a id="table-18"></a>

### Table 18: FPS Multi-Task Verification (same checkpoint, no retraining)

| Task | Test Set | Format (J) | Standard (448²) | + FPS | Δ |
| :--- | :--- | :--- | :---: | :---: | :---: |
| Open-vocab recog. | NTU-60 (55/5) | Kinect v2 (25) | 87.37% | 85.75% | −1.62 |
| Cross-format recog. | NW-UCLA | Kinect v1 (20) | 60.38% | 58.91% | −1.47 |
| Cross-format caption | HumanML3D | SMPL (22) | 37.28 BS | 36.52 BS | −0.76 |
| Motion QA (Temp.) | Skeleton-QA | Kinect v2 (25) | 68.4% | 67.1% | −1.3 |
| Motion QA (Causal) | Skeleton-QA | Kinect v2 (25) | 64.7% | 63.5% | −1.2 |

---

<a id="table-19"></a>

### Table 19: MQA / Candidate-Matching Protocol in Recent Open-Vocabulary Methods

| Method | Venue | Evaluation Protocol |
| :--- | :---: | :--- |
| PURLS | CVPR'24 | Label-text cosine matching |
| SCoPLe | CVPR'25 | Label-text cosine matching |
| Neuron | CVPR'25 | Label-text cosine matching |
| TDSM | ICCV'25 | Label-text cosine matching |

