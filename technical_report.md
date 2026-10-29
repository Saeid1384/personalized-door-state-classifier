# Technical Report — Personalized Door State Classifier

## 1. Objective

Classify the state of a door seen by a fixed camera. The model has two output classes:

- **Closed:** the door is closed.
- **Open:** the door is open or partially open.

The project targets a specific home-camera setup rather than claiming to work on arbitrary doors.

## 2. Model and training setup

| Setting | Value |
|---|---|
| Architecture | EfficientNet-B0 |
| Framework | PyTorch / Torchvision |
| Input resolution | 224 × 224 RGB |
| Output classes | 2 |
| Parameters | Approximately 4.0 million |
| Batch size | 16 |
| Epoch limit | 15 |
| Optimizer | AdamW |
| Learning rate | 1e-5 |
| Weight decay | 1e-4 |
| Loss | Cross-Entropy Loss |
| Training augmentation | Horizontal flip, rotation up to 10°, brightness and contrast variation |

The notebook selects a checkpoint according to validation accuracy and reports test metrics separately when the private data and required checkpoint are available.

## 3. Data

The training workflow combines publicly available door imagery, including [DeepDoors2](https://github.com/gasparramoa/DeepDoors2), with approximately **5,000 personally collected images** from three doors in the target home environment.

The private images and model checkpoints are not included in this public repository. Dataset composition, exact per-split counts, and the evaluation split should be documented from the final run before making stronger performance claims. Review the license and terms of each public dataset before reuse or redistribution.

## 4. Reported results

- **Best recorded validation accuracy:** 97.01% at epoch 11.
- **Reported accuracy on personal data:** approximately 97% in the target setup.

The 97.01% value is a validation result from the recorded experiment. The approximately 97% personal-data result is reported by the project author; this report does not treat it as an independently verified benchmark on unseen doors. The exact evaluation protocol should be stated alongside any final benchmark figure.

## 5. Interpretation and limitations

The results suggest the model is useful for the target setup, but do not establish generalization to unseen doors, camera viewpoints, or environments. Near-duplicate frames from the same video can inflate performance if they appear across multiple splits. A stronger evaluation holds out entire recording sessions or days and, for a generalization claim, tests on a door not used for training.

## 6. Privacy and reproducibility

This repository is a lightweight project report and experiment record. It does not provide a standalone inference/prediction utility. Personal images and checkpoints are omitted for privacy and repository size. The notebook requires the original dataset folder structure and initial checkpoint to rerun the training workflow.
