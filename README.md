# EPR-YOLO: Lightweight RGB Vision-Based Express Parcel Detection

Official repository for the research project **“A Lightweight RGB Vision-Based Express Parcel Detection Framework with Active Learning and Quantization-Aware Training.”**

EPR-YOLO is an RGB vision-based express-parcel detection framework designed for complex logistics environments. The framework combines an **Express Parcel Recognition (EPR) dataset**, **Active Learning-based pseudo-labeling**, a lightweight **YOLOv11s-based EPR-YOLO detector**, **SFAConv**, **NGAM**, **Quantization-Aware Training (QAT)**, and a **FastAPI-based Web application**.

> **Repository status:** The dataset has been released. Source code, pretrained weights, and implementation details are being organized and will be released progressively.

<!-- TODO: Add the paper overview / representative figure here. -->
<!-- Example: ![Overview](assets/figure_overview.png) -->

## Highlights

- **EPR Dataset:** 5,603 annotated RGB images with 8,274 object instances across eight express-parcel categories and damaged variants.
- **Active Learning:** Iterative pseudo-label generation and manual correction are used to improve annotation efficiency while maintaining label consistency.
- **EPR-YOLO:** A lightweight detector built on YOLOv11s with SFAConv and NGAM for multi-scale feature extraction and global semantic modeling.
- **Lightweight Design:** EPR-YOLO reaches **71.654% mAP50** with **8.53 M parameters** and **20.9 GFLOPs**.
- **Model Compression:** Compared with YOLOv11s, EPR-YOLO reduces the parameter count by approximately **9.5%** and GFLOPs by approximately **3.2%**.
- **INT8 QAT:** Quantization-Aware Training reduces model size from **19.2 MB to 11.9 MB (~38.0%)** with limited detection-performance degradation.
- **Web Application:** A FastAPI-based prototype supports single-image detection, batch detection, visualization, and online inference.

## Framework

<!-- TODO: Add figures from the paper to `assets/` and enable the corresponding Markdown image links. -->

### Active Learning-based EPR dataset construction

<!-- ![Active Learning workflow](assets/figure1_active_learning.png) -->

The raw image collection is standardized through quality control and unified re-annotation. An iterative Active Learning workflow then uses YOLOv11s to generate pseudo-labels for unlabeled subsets, followed by manual inspection and correction before the labeled training set is progressively expanded.

### EPR-YOLO architecture

<!-- ![EPR-YOLO architecture](assets/figure6_epr_yolo.png) -->

EPR-YOLO is developed from YOLOv11s. Selected convolutional layers in the backbone are replaced by **Selective Multi-Scale Feature Aggregation Convolution (SFAConv)**, while the **NeLU-enhanced Global Attention Mechanism (NGAM)** is introduced into deeper backbone stages.

### Quantization-Aware Training

<!-- TODO: Add the relevant QAT figure/table visualization from the paper if desired. -->

QAT simulates low-precision quantization during training and produces an INT8-quantized model. The current study evaluates quantization performance and storage reduction; hardware-level benchmarking on resource-constrained edge devices remains future work.

### Web-based application

<!-- ![Web architecture](assets/figure7_web_architecture.png) -->
<!-- ![Web interface](assets/figure8_web_interface.png) -->

The application uses a native HTML/CSS/JavaScript front end and a FastAPI back end. The system supports model-status queries, single-image detection, batch detection, annotated-result visualization, confidence scores, bounding boxes, processing time, and class statistics.

## EPR Dataset

The **Express Parcel Recognition (EPR) Dataset** is publicly available on Kaggle:

**Kaggle:** https://www.kaggle.com/datasets/ongkingu1/express-parcel-recognition-epr-dataset

The final dataset contains:

| Item | Description |
|---|---|
| Images | 5,603 |
| Object instances | 8,274 |
| Number of classes | 8 |
| Image modality | RGB |
| Model input size | 640 × 640 pixels |
| Annotation task | Object detection |

The eight classes are:

1. Box
2. Damaged box
3. Envelope
4. Damaged envelope
5. Poly mailer
6. Damaged poly mailer
7. Irregular parcel
8. Tube

<!-- ![Representative EPR samples](assets/figure3_epr_samples.png) -->

## Results

### Comparative performance

| Model | Precision (%) | Recall (%) | mAP50 (%) | mAP (%) | F1 (%) | GFLOPs | Params (M) |
|---|---:|---:|---:|---:|---:|---:|---:|
| YOLOv11s | 88.101 | 71.134 | 70.800 | 66.818 | 78.706 | 21.6 | 9.43 |
| **EPR-YOLO** | **88.958** | **71.511** | **71.654** | **66.840** | **79.280** | **20.9** | **8.53** |

Results are reported as means across three independent random splits in the paper; see the manuscript for standard deviations and comparisons with the other YOLO variants.

### Independent test-set evaluation

| Model | Precision (%) | Recall (%) | mAP50 (%) | mAP (%) | F1 (%) |
|---|---:|---:|---:|---:|---:|
| EPR-YOLO | 88.343 | 70.730 | 70.962 | 66.160 | 78.247 |
| QAT-EPR-YOLO | 88.420 | 69.531 | 70.699 | 65.928 | 77.860 |

After INT8 quantization, the model size decreases from **19.2 MB to 11.9 MB**, corresponding to an approximately **38.0% reduction**.

## Repository Structure

```text
EPR-YOLO/
├── README.md
├── LICENSE
├── assets/                  # Figures from the paper (to be added)
├── active_learning/         # Active Learning and pseudo-label iteration
├── models/
│   ├── sfaconv/             # SFAConv implementation
│   └── ngam/                # NGAM implementation
├── qat/                     # Quantization-Aware Training
├── train/                   # Training pipeline
├── evaluate/                # Validation and test-set evaluation
├── web_app/                 # FastAPI Web application
├── configs/                 # Model/training configurations
└── weights/                 # Pretrained model weights
```

Each implementation directory currently contains a placeholder file. Code and pretrained weights will be released after repository cleanup and documentation.

## Installation

Code dependencies and installation instructions will be provided together with the source-code release.

```bash
# Coming soon
```

## Training

```bash
# Coming soon
```

## Evaluation

```bash
# Coming soon
```

## Quantization-Aware Training

```bash
# Coming soon
```

## Web Application

```bash
# Coming soon
```

## Paper Figures

All figures used in the README will be taken from the manuscript. Place the exported figures in the `assets/` directory and then uncomment/update the corresponding Markdown image links above.

Suggested filenames:

```text
assets/
├── figure1_active_learning.png
├── figure2_active_learning_metrics.png
├── figure3_epr_samples.png
├── figure4_sfaconv.png
├── figure5_ngam.png
├── figure6_epr_yolo.png
├── figure7_web_architecture.png
└── figure8_web_interface.png
```

## Citation

If you use the EPR dataset or this repository in your research, please cite the associated paper. The final bibliographic information and BibTeX entry will be updated after publication.

```bibtex
@article{wu2026epryolo,
  title   = {A Lightweight RGB Vision-Based Express Parcel Detection Framework with Active Learning and Quantization-Aware Training},
  author  = {Wu, An-Qi and Guo, Fan and Yang, Weijun and Wang, Rui-Feng and Hu, Pingfan},
  year    = {2026},
  note    = {Manuscript under review}
}
```

## Authors

- An-Qi Wu
- Fan Guo
- Weijun Yang
- Rui-Feng Wang
- Pingfan Hu

## License

A license file is included as a placeholder. Please select the final open-source license before publicly releasing the source code and model weights.

## Acknowledgements

We thank the contributors and maintainers of the open-source tools and datasets that supported this research.

## Updates

- **2026-09:** Initial repository structure and README prepared.
- Dataset released on Kaggle.
- Source code and pretrained weights: **Coming soon.**
