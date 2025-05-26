# Staircase Detection

<p align="center">
  <img src="images/staircase_banner.png" alt="Staircase Detection Banner" width="80%">
</p>

---

## 📖 Table of Contents

1. [Overview](#-overview)
2. [Motivation](#-motivation)
3. [Dataset & Scenarios](#-dataset--scenarios)
4. [Methodology](#-methodology)

   * [Preprocessing](#preprocessing)
   * [Detection Pipeline](#detection-pipeline)
5. [Architecture](#-architecture)
6. [Usage](#-usage)
7. [Results & Visualizations](#-results--visualizations)
8. [Folder Structure](#-folder-structure)
9. [Installation](#-installation)
10. [Contributing](#-contributing)
11. [License](#-license)

---

## 🔍 Overview

**Staircase Detection** automatically identifies staircases in images captured from diverse environments (indoor, outdoor, uneven lighting). Leveraging modern computer vision techniques, our pipeline segments potential stair regions and refines detections through geometric analysis.

<p align="center">
  <img src="images/pipeline_overview.png" alt="Pipeline Overview" width="70%">
</p>

---

## 🎯 Motivation

Detecting staircases reliably is crucial for:

* **Robotics & Navigation:** Enabling autonomous robots and wheelchairs to safely traverse stairs.
* **Accessibility:** Assisting visually impaired users via smartphone alerts.

<p align="center">
  <img src="images/motivation.png" alt="Motivation Diagram" width="60%">
</p>

---

## 📂 Dataset & Scenarios

We evaluate on three scenarios:

1. **Indoor Staircases** – controlled lighting, uniform steps.
2. **Outdoor Staircases** – variable textures (stone, wood).
3. **Challenging Conditions** – shadows, partial occlusion.

Each scenario contains 500 labeled images with bounding boxes around stairs.

<p align="center">
  <img src="images/dataset_samples.png" alt="Dataset Samples" width="80%">
</p>

---

## 🛠 Methodology

### Preprocessing

* Resize to 512×512
* Histogram equalization to normalize lighting

### Detection Pipeline

1. **Edge & Line Extraction:** Canny + Hough Transform
2. **Region Proposals:** Group parallel lines into step candidates
3. **Classifier:** CNN-based binary classifier to filter false positives
4. **Post-processing:** Non-Maximum Suppression on bounding boxes

<p align="center">
  <img src="images/architecture_diagram.png" alt="Architecture Diagram" width="70%">
</p>

---

## 🏗 Architecture

| Component              | Details                               |
| ---------------------- | ------------------------------------- |
| Backbone CNN           | ResNet-50 pretrained on ImageNet      |
| Feature Pyramid        | FPN for multiscale feature extraction |
| Proposal Network       | RPN generating 2000 anchors per image |
| Classifier & Regressor | Fully connected heads for detection   |

<p align="center">
  <img src="images/model_structure.png" alt="Model Structure" width="70%">
</p>

---

## 🚀 Usage

```bash
# Clone repo
git clone https://github.com/Vishnucreate/StaircaseDetection.git
cd StaircaseDetection

# Install dependencies
pip install -r requirements.txt

# Run detection on sample images
python detect.py --input path/to/images/ --output results/
```

---

## 📈 Results & Visualizations

| Scenario    | Precision | Recall | F1-score |
| ----------- | --------: | -----: | -------: |
| Indoor      |      0.92 |   0.88 |     0.90 |
| Outdoor     |      0.89 |   0.85 |     0.87 |
| Challenging |      0.85 |   0.80 |     0.82 |

<p align="center">
  <img src="images/results_plot.png" alt="Results Plot" width="70%">
</p>

<p align="center">
  <img src="images/sample_detections.png" alt="Sample Detections" width="80%">
</p>

---

## 🗂 Folder Structure

```bash
StaircaseDetection/
├── images/                # Illustrations & result images
├── data/                  # Labeled dataset (download separately)
├── models/                # Trained model checkpoints
├── detect.py              # Inference script
├── train.py               # Training script
├── requirements.txt       # Python deps
└── README.md              # This file
```

---

## ⚙️ Installation

```bash
pip install -r requirements.txt
```

Dependencies include OpenCV, PyTorch, scikit-learn.

---

## 🤝 Contributing

We welcome pull requests for:

* Additional scenario datasets
* Model improvements (e.g. transformer backbones)
* Real-time video integration

---

## 📄 License

This project is licensed under MIT. See [LICENSE](LICENSE) for details.
