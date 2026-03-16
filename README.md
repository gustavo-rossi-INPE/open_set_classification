# Tree species mapping in a dense Brazilian Cerrado formation based on UAV imagery and open-set deep learning models

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch 2.x](https://img.shields.io/badge/PyTorch-2.x-red.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This repository contains an integrated classification framework that performs tree species classification from UAV-derived individual tree crown (ITC) images under an open-set recognition setting. It includes data preparation, closed-set model training, open-set calibration, evaluation, and large-scale inference.



## Key Features

- Closed-set training with deep learning models
- Open-set recognition using PCA-based and OpenMax-based approaches
- Evaluation with open-set metrics such as Macro-F1, OSCR-AUC, AUROC, and FPR@TPR
- Patch-based inference from UAV orthomosaics
- Crown-level output aggregation for large-scale mapping
- Reproducible experiments with fixed random seeds



## Project Structure

```text
├── notebooks/
│   ├── 01_patch_extraction.ipynb
│   ├── 02_train_calibrate_eval_infer.ipynb
├── requirements.txt
├── README.md
└── data/
    └── README_data.md
```

## Installation

### Prerequisites

- Python 3.10 or higher
- CUDA-compatible GPU (optional but recommended)

### Setup
#### Note
This entire project was elaborated and executed in Google Colab environment, using the T4 GPU provided by the Google Colab Premium signature.
If the desire is to run locally, follow the following steps:

1. **Clone the repository**

```bash
git clone https://github.com/gustavo-rossi-INPE/open_set_classification.git
cd open_set_classification
```

2. ** Create a virtual Environment
```bash
conda create -n open-set-trees python=3.10
conda activate open-set-trees
```

### Install the main dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

## Usage

### Patch Extraction

Patch extraction is performed from crown polygons and can be applied in two different contexts:

1. **Training dataset generation**

   Image patches are extracted from manually delineated individual tree crowns (ITCs).  
   These crowns represent the reference dataset used to train the closed-set classifiers.

2. **Inference dataset generation**

   Image patches are extracted from automatically detected crowns obtained through the segmentation workflow described in Baudchon et al. (2026). For full details regarding crown automatic segmentation, please refer to the original publication.
   These crowns are used to generate the patches classified during the large-scale inference stage.
   
```bibtex
Baudchon, H., Ouaknine, A., Weiss, M., Teng, M., Walla, T. R., Caron-Guay, A., Pal, C., & Laliberté, E. (2026).  
[SelvaBox: A high-resolution dataset for tropical tree crown detection](https://arxiv.org/abs/2507.00170)
```

Although the extraction scripts are included in this repository, running them is **not required** to reproduce the experiments, since the training dataset is already provided in its final structure.


---
### Main pipeline
The notebook 02_train_calibrate_eval_infer.ipynb covers the pipeline from model training to evaluation and large-scale inference.

Execute the notebook sections in the following order:

1. **Dataset inspection**  
   Verifies the organization of the pre-extracted patch dataset and counts the available samples per species and split.

2. **Closed-set training**  
   Trains the closed-set deep learning classifiers on the known species dataset across 5 different seeds.

3. **Closed-set evaluation**  
   Summarizes model performance and generates comparative plots across runs and architectures.

4. **Open-set calibration and evaluation**  
   Fits and evaluates the open-set recognition methods, including PCA-Qmin-based and OpenMax-based approaches.

5. **ROC / OSCR analysis**  
   Generates threshold-based and threshold-free open-set performance curves.

6. **Confusion matrix generation**  
   Produces the multiclass confusion matrix including the unknown class.

7. **Large-scale inference and shapefile export**  
   Applies the selected operational model to inference outputs and exports the final results as tabular and spatial files.




---

## Data Availability

The full dataset used in this study is not entirely included in this repository due to size and storage limitations.

The repository contains the code required to reproduce the experiments described in the paper. Input data may include:

- Orthomosaic for patch extraction-
- Manually delimited crown shapefile for train/val patch extraction
- Cropped individual tree crown (ITC) image patches, organized into labeled species folders.
- Train / validation / test splits
- Automatically delimited crown shapefile for large-scale inference.

Additional information about dataset access and metadata will be provided separately.


The dataset is available at Zenodo:
https://doi.org/xxxxx

---

## Reproducibility

The experiments were designed to ensure reproducible results through:

- Fixed random seeds across Python, NumPy, and PyTorch
- Consistent data partitioning strategies
- Explicit training and evaluation workflows
- Saved model outputs and evaluation metrics

All experiments can be reproduced by running the notebooks in the order described in the **Usage** section.

---

## Citation

If you use this code in your research, please cite the associated paper:

```bibtex
@article{rossi2026_openset_trees,
  title   = {Tree species mapping in a dense Brazilian Cerrado formation based on UAV imagery and open-set deep learning models},
  author  = {Rossi, Gustavo Fiedler and others},
  journal = {Journal Name},
  year    = {2026}
}
```

This citation will be updated once the paper is officially published.

---

## Acknowledgments

This work was developed as part of research conducted at:

- University of São Paulo (USP)

The authors acknowledge the use of open-source software from the scientific Python ecosystem, including **PyTorch**, **scikit-learn**, and **NumPy**.

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
