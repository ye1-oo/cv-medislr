# Data Directory

This directory contains **lightweight demo samples** and **auxiliary files** used for
the inference-only demonstration of our medical sign language recognition models.

Due to dataset size and GitHub file size limitations, **full datasets and most pretrained model weights are not included in this repository**.
Instead, this directory is designed to support **demo execution and result reproduction**.

---

## Demo Samples (`samples/`)

The `samples/` directory contains **small preprocessed tensor samples** used exclusively in `demo.ipynb`.

- Each subdirectory corresponds to a modeling approach:
  - `1D/`
  - `2D Sequence/`
  - `2d_only/`

- For each model:
  - approximately **20 `.pt` tensor samples** are provided,
  - tensors are already preprocessed and ready for inference,
  - no additional preprocessing is required to run the demo.

These samples allow the demo notebook to:
- load pretrained checkpoints,
- run inference immediately,
- showcase qualitative model behavior.

---

## Pretrained Model Weights

Pretrained model checkpoints are **not fully tracked in this repository** due to file size constraints.

- Some lightweight checkpoints may appear under:
  ```
  preprocessed/model_weights/
  ```
- The complete set of pretrained weights for all models is provided via **Google Drive**.

The Drive link is included in the **main project README**.

---

## Preview Data (`preprocessed/preview`)

This folder contains **minimal preview-only data** (e.g., skeleton frames and keypoints) for
illustration and reference purposes.

- These files are **not used for training or evaluation**.
- They exist only to show data formats and intermediate representations.

---

## Notes

- This repository focuses on **code structure and inference demonstration**.
- Training requires access to the full dataset and pretrained checkpoints provided separately.

For detailed project description and usage instructions, refer to the **main README**.
