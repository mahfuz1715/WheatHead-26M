# WheatHead-26M

### Cross-Domain Wheat Head Detection and Counting on GWHD 2021

WheatHead-26M is a research project focused on robust wheat-head detection and image-level counting across unseen field domains. The study compares YOLOv8 and YOLO26 variants on the **Global Wheat Head Detection (GWHD) 2021** benchmark and evaluates detection quality, computational efficiency, counting reliability, and domain-wise behavior.

The strongest model in the study, **YOLO26m**, is referred to as **WheatHead-26M**.

> **Status:** Accepted for presentation at the **12th IEEE International Women in Engineering (WIE) Conference on Electrical and Computer Engineering 2026 (IEEE WIECON-ECE 2026)**.

---

## Research Focus

This work was designed around four practical questions:

- How well do YOLOv8 and YOLO26 generalize to unseen GWHD 2021 domains?
- Which model provides the best accuracy-efficiency trade-off?
- How reliable are the strongest detectors for image-level wheat-head counting?
- Which test domains remain the most difficult, and why?

Rather than relying only on aggregate detection scores, the study also examines counting error and domain-specific failure patterns.

---

## Evaluated Models

Five one-stage detectors were compared:

- YOLOv8n
- YOLOv8s
- YOLOv8m
- YOLO26s
- YOLO26m

Among the YOLOv8 variants, **YOLOv8m** performed best.  
Among all evaluated models, **YOLO26m / WheatHead-26M** achieved the strongest overall test performance.

---

## Main Detection Results

| Model | Precision | Recall | F1 | mAP@0.50 | mAP@0.50:0.95 | Params (M) | GFLOPs |
|---|---:|---:|---:|---:|---:|---:|---:|
| YOLOv8n | 0.798 | 0.599 | 0.684 | 0.670 | 0.302 | 3.01 | 8.1 |
| YOLOv8s | 0.779 | 0.621 | 0.691 | 0.677 | 0.285 | 11.13 | 28.4 |
| YOLOv8m | 0.835 | 0.670 | 0.743 | 0.734 | 0.333 | 25.84 | 78.7 |
| YOLO26s | 0.824 | 0.670 | 0.739 | 0.736 | 0.322 | 9.93 | 20.5 |
| **WheatHead-26M** | **0.851** | **0.691** | **0.763** | **0.762** | **0.363** | **21.75** | **67.8** |

Relative to YOLOv8m, WheatHead-26M achieved better detection metrics while using:

- **15.8% fewer parameters**
- **13.9% fewer GFLOPs**

---

## Wheat-Head Counting

The two strongest medium-sized detectors, YOLOv8m and WheatHead-26M, were evaluated for image-level counting.

Counting thresholds were selected using validation data only:

- **Confidence threshold:** 0.20
- **IoU threshold:** 0.50

| Model | MAE ↓ | RMSE ↓ | R² ↑ | MAPE ↓ |
|---|---:|---:|---:|---:|
| YOLOv8m | 8.918 | 11.759 | 0.826 | 24.84% |
| **WheatHead-26M** | **8.085** | **10.742** | **0.855** | **22.92%** |

WheatHead-26M therefore improved both localization and downstream counting performance.

---

## Dataset

The experiments use the **Global Wheat Head Detection 2021 (GWHD 2021)** dataset.

| Split | Records | Boxes | Domains |
|---|---:|---:|---:|
| Training | 3,657 | 163,690 | 18 |
| Validation | 1,476 | 44,347 | 11 |
| Test | 1,382 | 67,424 | 18 |

The supplied train, validation, and test partitions were preserved so that the evaluation reflects cross-domain generalization rather than a random image-level split.

During evaluation-library indexing, one repeated test image record was removed, resulting in **1,381 unique test images** and **67,365 valid test instances**.

The dataset itself is not redistributed in this repository.

**Dataset reference:**  
Global Wheat Head Detection 2021  
DOI: `10.34133/2021/9846158`

---

## Training Setup

All models were fine-tuned using:

- Input size: **640 × 640**
- Batch size: **16**
- Maximum epochs: **80**
- Early-stopping patience: **15**
- Cosine learning-rate scheduling

YOLOv8 runs used **AdamW** with an initial learning rate of **0.001**.

YOLO26 runs used automatic optimizer selection together with stronger augmentation, including HSV variation, rotation, translation, scaling, flips, mosaic, and a small MixUp probability.

---

## Domain-Wise Findings

The largest counting errors for WheatHead-26M appeared in:

- **UQ_8**
- **UQ_9**
- **KSU_4**
- **Ukyoto_1**

Lower errors were observed in:

- **NAU_2**
- **CIMMYT_2**
- **NAU_3**

Dense scenes, overlap, small heads, and visually complex backgrounds were among the main sources of remaining error.

This analysis highlights that a strong overall score does not guarantee equally strong performance across every agricultural domain.

---

## Repository Structure

```text
WheatHead-26M/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── 01_wheathead26m_detection_counting.ipynb
└── paper/
    └── README.md
```

The repository is organized to keep the implementation and paper information separate and easy to navigate.

---

## Paper

**Title:**  
*Cross-Domain Wheat Head Detection and Counting Using YOLOv8 and YOLO26: An Accuracy–Efficiency Study on GWHD 2021*

### Authors

- Shawna Akter
- **Mahfuz Uddin Ahmed**
- Moin Uddin Ahmed
- Rafid Bin Taher
- K. M. Safin Kamal

### Conference

**12th IEEE International Women in Engineering (WIE) Conference on Electrical and Computer Engineering 2026 (IEEE WIECON-ECE 2026)**

### Status

**Accepted for Presentation**

The publisher-formatted paper is not redistributed in this repository. The official publication link and DOI can be added once the final bibliographic record becomes available.

---

## Limitations

The study has several limitations:

- YOLOv8 and YOLO26 were trained with different optimization and augmentation settings.
- All models used a fixed 640 × 640 input resolution.
- Evaluation was limited to static RGB images from GWHD 2021.
- Dense and heavily occluded wheat heads remained difficult.
- Broader validation across additional datasets and field conditions is still needed.

---

## Future Directions

Potential extensions include:

- standardized training across detector generations,
- higher-resolution feature learning,
- domain adaptation,
- occlusion-aware detection,
- broader field validation,
- and combining detection with density- or tracking-based counting methods.

---

## Citation

Official citation details will be updated when the final conference bibliographic record becomes available.

```bibtex
@misc{wheathead26m2026,
  title = {Cross-Domain Wheat Head Detection and Counting Using YOLOv8 and YOLO26: An Accuracy--Efficiency Study on GWHD 2021},
  note  = {Accepted for presentation at IEEE WIECON-ECE 2026},
  year  = {2026}
}
```
