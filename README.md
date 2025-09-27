# 📌 Affect Recognition with CNNs (ResNet50 & EfficientNetV2-S)

## 📝 Overview
This project explores **affect recognition** from facial expressions using deep learning.  
The task involves:
- **Classification** of discrete facial expressions.  
- **Regression** of **valence** (positivity/negativity) and **arousal** (calmness/excitement).  

The models are evaluated in the context of **"in-the-wild" affective systems**, where robustness and correlation-based metrics (e.g., CCC, SAGR) are crucial.

---

## ⚙️ Model Architectures
Two CNN architectures were implemented:

- **ResNet50**  
  - ~25.6M parameters  
  - Deep residual network with skip connections  
  - Strong baseline widely adopted in computer vision  

- **EfficientNetV2-S**  
  - ~22M parameters  
  - Lightweight, parameter-efficient CNN  
  - Faster inference with competitive accuracy  

### 🔄 Transfer Learning Strategy
- **Pretrained Weights**: Initialized with **ImageNet** weights.  
- **Frozen Layers**: Early convolutional layers frozen (low-level features generalize well).  
- **Fine-tuned Layers**: Later layers and task-specific heads trained on affective dataset.  
- **Benefits**:
  - Faster convergence  
  - Reduced overfitting  
  - Better generalization with limited data  

---

## 🧪 Training Configuration
- **Input Size**: 224 × 224 RGB  
- **Batch Size**: 32  
- **Optimizer**: AdamW  
- **Learning Rate**: `1e-4` with `ReduceLROnPlateau` scheduler  
- **Loss Functions**:
  - Classification → CrossEntropy (with label smoothing / focal loss optional)  
  - Regression → MSE Loss  
- **Regularization**: Dropout + Weight Decay (`1e-4`)  
- **Data Augmentation**: Random flips, rotations, color jitter, normalization  
- **Epochs**: Up to 30, with **early stopping (patience = 5)**  

---

## 📊 Results & Performance

### 📌 Metrics Used
- **Classification**: Accuracy, F1, Cohen’s Kappa  
- **Regression**: RMSE, Pearson Correlation (CORR), Sign Agreement (SAGR), Concordance Correlation Coefficient (CCC)  
- **Why CCC?** → Best suited for *in-the-wild* systems as it balances accuracy, correlation, and agreement  

### 🏆 Best Results

| Model              | Accuracy | F1   | Valence CCC | Arousal CCC |
|--------------------|----------|------|-------------|-------------|
| **ResNet50**       | **46.25%** | **0.46** | **0.53** | **0.36** |
| EfficientNetV2-S   | 42.1%    | 0.41 | 0.49        | 0.35        |

---

## 🚀 How to Run

1. **Clone Repository & Install Dependencies**
   ```bash
   git clone <repo_url>
   cd affect-recognition
   pip install -r requirements.txt
   ```

2. **Open the Notebook**
   ```bash
   jupyter notebook code.ipynb
   ```

3. **Run Training**
   - Set model backbone (`ResNet50` or `EfficientNetV2-S`) in the notebook.  
   - Configure hyperparameters if needed.  
   - Execute training cells to train and evaluate models.  

4. **Evaluate Performance**
   - Results (logs + plots) will be saved automatically.  
   - Best metrics can be found in `summary.json`.  

---

## 🙌 Acknowledgements
- **Pretrained Models**: [ImageNet](https://www.image-net.org/)  
- **Frameworks**: PyTorch, Torchvision, NumPy, Matplotlib  
- **Metrics**: RMSE, CORR, SAGR, CCC (commonly used in AVEC/affective computing challenges)  
- **References**:
  - He et al., *Deep Residual Learning for Image Recognition (ResNet)*  
  - Tan & Le, *EfficientNetV2: Smaller Models and Faster Training*  

---

🔍 **Note**: This README summarizes the methodology, training details, and results from:
- `code.ipynb` → Implementation  
- `i211777_Areeba_A1-CS4025.pdf` → Project report  
- `summary.json` → Training logs & results
