# Inference Demo — Medical Sign Language Recognition

Team 10 — Computer Vision Project

This demo notebook presents **inference-only results** for our medical sign language recognition project.
All models were **pretrained offline**, and this demo focuses solely on loading trained checkpoints
and running predictions on **sample data**.

Training code and full datasets are not executed in this notebook.

---

## Models Included in This Demo

The following models are demonstrated:

### 1D Models
- 1D GRU
- 1D TCN  
(Implemented within a unified notebook due to shared preprocessing and input format.)

### 2D Sequence Models
- GRU (2D temporal sequence)
- TCN (2D temporal sequence)

### 2D Only Models
- TSN (Temporal Segment Network) with hand-focused inputs
- Tiling-based model using ResNet-18 backbone

Each model loads a corresponding pretrained checkpoint and performs inference on demo samples.

---

## Sample Data

- Demo samples are located in `data/samples/`
- Each model uses **20 pre-extracted tensor samples** (`.pt` files)
- These samples are provided **only for demonstration purposes**
- Full datasets are excluded due to storage limitations

---

## Model Weights

- Pretrained model checkpoints (`.pt`) are **not fully included in this repository**
- Due to GitHub file size limitations, checkpoints are provided via **Google Drive**
- Please download the required model weights before running the demo

(Refer to the main project README for the Drive link.)

---

## Path Configuration (Important)

This demo notebook is intended to be run on **Google Colab**.

Before running the demo, you **must update file paths** to match your Google Drive environment.

### Example

```python
BASE_DIR = "/content/drive/MyDrive/cv-medislr"
