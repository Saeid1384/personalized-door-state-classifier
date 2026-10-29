# Personalized Door State Classifier

A personalized computer-vision experiment for classifying a door as **Open** or **Closed** using **EfficientNet-B0** and **PyTorch**. A partially open door is counted as **Open**.

> **Scope:** This model was tuned for a specific home-camera setup. It is presented as a project report, not as a general-purpose door-recognition tool.

## Demo

<!-- Add your demo GIF here when ready. You can link the GIF to the full demo video. -->

## At a glance

| Item | Details |
|---|---|
| Task | Binary image classification |
| Classes | `Closed`, `Open` (includes partially open) |
| Architecture | EfficientNet-B0 |
| Framework | PyTorch / Torchvision |
| Input | 224 × 224 RGB images |
| Parameters | Approximately 4.0 million |
| Best recorded validation accuracy | 97.01% (epoch 11) |
| Reported accuracy on personal data | Approximately 97% in the target setup; evaluation details should be interpreted in context |

## Dataset

The project combines public door imagery, including [DeepDoors2](https://github.com/gasparramoa/DeepDoors2), with approximately **5,000 images collected personally** from three doors in the target home environment. The personal images and model checkpoints are not included in this repository for privacy and size reasons.

The public dataset's license and terms should be checked before reusing or redistributing its files. This repository does not redistribute the dataset.

## Approach

- Fine-tuning an EfficientNet-B0 classifier with two output classes.
- Image augmentation during training, including horizontal flips, small rotations, and brightness/contrast variation.
- AdamW optimizer and cross-entropy loss.
- The notebook documents the training and evaluation workflow; the private dataset and initial checkpoint required to rerun the experiment are not included.

## Limitations

The reported results are specific to the current experiment and target setup. Performance on unseen doors, camera positions, or environments has not been established. For a reliable generalization test, separate complete recording sessions or days rather than randomly splitting near-identical frames from the same video.

## Repository contents

- [`personalized_door_state_classifier.ipynb`](personalized_door_state_classifier.ipynb) — training and evaluation notebook.
- [`technical_report.md`](technical_report.md) — concise technical report.
- [`requirements.txt`](requirements.txt) — core Python packages used by the notebook.
