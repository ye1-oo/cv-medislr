# Medical Sign Language Recognition  
**Medical-domain Korean Sign Word Recognition with Controlled Representation Comparisons**

Team 10 — Computer Vision Project  
Ewha Womans University

## Overview

This project presents an end-to-end pipeline for **medical-domain Korean sign word recognition**, focusing on **isolated medical sign words** performed within short temporal windows (approximately 1–2 seconds).

We design a unified preprocessing pipeline and conduct **controlled comparisons across multiple input representations and sequence modeling strategies**, including:

- 1D keypoint sequences  
- 2D RGB frame sequences  
- Skeleton image sequences  
- Skeleton frame tiling (2D CNN baseline)

Our goal is to analyze **how representation choice and sequence encoders interact**, under identical data splits and controlled experimental settings, in a **low-data medical sign language scenario**.

This repository contains:
- preprocessing notebooks,
- model training notebooks,
- an inference-only demo notebook,
- lightweight demo samples and pretrained checkpoints.

## Motivation

In medical environments, accurate communication between Deaf or speech-impaired patients and clinicians is critical, yet professional medical sign interpreters are often unavailable.

Medical sign language presents unique challenges:
- short, word-level motions,
- subtle hand-shape differences,
- high sensitivity to background, viewpoint, and signer variation.

This project aims to establish a **robust and extensible baseline pipeline** for medical sign word recognition, serving as a foundation for future real-world deployment.

## Dataset

- **Source**: AI-Hub Korean Sign Language Dataset  
- **Subset**: 22 medical-related isolated sign words  
- **Signers**: 10  
- **Viewpoints**: 5 (D / F / L / R / U)

After preprocessing:
- Raw videos: 1,100  
- Corrupted samples removed: 3  
- Final usable sequences: **1,097**

All experiments use the same cleaned dataset and a fixed **train/validation/test split (70/15/15)**.

## Preprocessing Pipeline

```
Raw videos
 → Word-level temporal cropping
 → Skeleton & keypoint extraction (MediaPipe Holistic)
 → Fixed-length sequence normalization (T = 16)
 → Representation-specific tensor construction
```

Key preprocessing design choices:
- Word-level segmentation using provided temporal metadata
- MediaPipe Holistic for hand and body skeleton extraction
- Hands-only, body-only, and full-skeleton configurations
- Fixed sequence length (T = 16) via uniform sampling or padding
- Train-only normalization to prevent data leakage

Skeleton outputs are stored as:
- JSON keypoints for 1D models
- Skeleton-rendered images for 2D CNN-based models

## Modeling Approaches

### 1D Keypoint-based Models

- Input: hand keypoints (42 joints × (x, y, z, visibility))
- Explicit velocity features added
- Models:
  - BiGRU + Attention
  - TCN + Attention

### 2D RGB Frame-based Models

- Input: cropped RGB hand frames
- Frame encoder: MobileNetV3 Small
- Models:
  - BiGRU
  - TCN

### Skeleton Image Sequence (TSN)

- Input: hand-skeleton images (grayscale)
- Cached as `.pt` tensors with shape `(16, 1, 64, 64)`
- Model:
  - MobileNetV2 + Temporal Segment Network (TSN)

### Skeleton Frame Tiling (2D CNN Baseline)

- Input: 16 skeleton frames tiled into a 4×4 grid
- Single 224×224 image
- Model:
  - ResNet18

## Results

| Representation | Model | Best Validation Accuracy | Test Accuracy |
|----------------|-------|--------------------------|---------------|
| 1D Keypoints | BiGRU + Attention | 0.927 | 0.892 |
| 1D Keypoints | TCN + Attention | **0.951** | **0.952** |
| 2D RGB | BiGRU + Attention | 0.952 | 0.903 |
| 2D RGB | TCN + Attention | 0.612 | 0.539 |
| Skeleton Images | MobileNetV2 + TSN | 0.842 | 0.824 |
| Skeleton Tiling | ResNet18 | 0.859 | 0.873 |

The optimal sequence encoder strongly depends on the input representation.  
TCN excels with explicit temporal signals (1D keypoints with velocity), while GRU generalizes better for implicit temporal representations such as RGB frames.

## Repository Structure

```
cv-medislr/
├── demo.ipynb
├── modeling/
│   ├── 1d/
│   ├── 2d_sequence/
│   └── 2d_only/
├── preprocessing/
├── data/
│   ├── processed/metadata/
│   ├── preview/
│   ├── samples/
│   └── README.md
└── README.md
```

## Demo

The demo.ipynb notebook demonstrates inference-only execution using pretrained models.

- No training is performed
- Lightweight sample tensors are used
- Intended to be run on Google Colab

Before running the demo, users must modify file paths to match their own Google Drive mount
location. Detailed instructions are provided in demo_README.md.

## Full Data and Pretrained Models

Due to GitHub file size limitations, the following are not fully included in this repository:

- Full preprocessed datasets
- Most pretrained model weights

They are available via Google Drive at the following link:

https://drive.google.com/drive/u/2/folders/10uM25Xfm6KCamKFkzoV2dMvfjE5hPQAR

The Drive folder includes:
- Pretrained model checkpoints (data/preprocessed/model_weights)
- Demo-related files
- Additional data required for inference

## Notes

- This repository is intended for reproducibility and demonstration
- Training requires external data and pretrained checkpoints
- All reported results correspond to pretrained models

## Reference

This repository accompanies the project report:

*Medical-domain Korean Sign Word Recognition: A Unified Pipeline with Controlled Representation Comparisons*  
Ewha Womans University, Computer Vision Project
