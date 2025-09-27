Project Overview
This project explores Convolutional Neural Networks (CNNs) for affect analysis (categorical emotion classification and continuous valence/arousal regression).  
We implemented multiple baselines, applied transfer learning, and evaluated performance using both categorical and continuous domain metrics.
Repository Structure
├── annotations/ # Annotation files (labels, metadata)
├── images/ # Dataset images
├── checkpoints/ # Trained model weights + logs
├── results/ # Output plots & metrics
├── code.ipynb # Main Jupyter Notebook (all code)
└── README.md # Project documentation
Network Details

- Models Used:ResNet50, EfficientNetV2-S
- Pretraining: ImageNet pretrained weights (transfer learning)
- Training Settings:
  - Optimizer: AdamW
  - Scheduler: ReduceLROnPlateau
  - Losses: CrossEntropy (classification), MSE (regression)
  - Batch size: 32
  - Epochs: ~20 (with early stopping)
- Augmentations: Random horizontal flip, color jitter, random crop, normalization

Rationale for Baselines:

- ResNet50 – classic deep CNN, strong baseline.
- EfficientNetV2-S – modern, parameter-efficient CNN, better performance with fewer FLOPs.
  Qualitative Results
  We visualize correct and incorrect predictions for each model.  
  (Plots are generated directly in `code.ipynb`)
  Evaluation Metrics
- Categorical domain: Accuracy, F1-score, Cohen’s Kappa, Krippendorff’s Alpha, AUC, AUC-PR
- Continuous domain: RMSE, CORR, SAGR, CCC
- Why multiple metrics?
  - Accuracy/F1 alone may not capture label imbalance → Kappa/Alpha improve reliability checks
  - RMSE for magnitude error, CORR for linear relation, SAGR for sign correctness, CCC combines correlation & bias.
  - For in-the-wild deployment, CCC is most suited.
    How to Run

1. Clone repo & open `code.ipynb`
2. Update dataset path inside notebook
3. Run all cells to train/evaluate models
4. Trained checkpoints are available in `/checkpoints`
