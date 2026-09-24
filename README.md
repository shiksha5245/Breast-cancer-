IDC Detection from Breast Histopathology Images

A deep learning-based computer vision project for classifying breast histopathology image patches as Invasive Ductal Carcinoma (IDC) or non-IDC using a ResNet-18 convolutional neural network.

«Note: This project is intended for educational and research purposes. It is not a clinical diagnostic system and should not be used for medical diagnosis.»

---

📌 Project Overview

Breast histopathology images contain complex tissue structures that can be difficult to analyze manually at scale. This project explores how deep learning can be used to automatically classify small image patches extracted from breast tissue.

The primary objective is to build an end-to-end image classification pipeline that can:

- Load and preprocess histopathology image patches
- Analyze class and patient-level distributions
- Prevent patient-level data leakage
- Handle class imbalance
- Train a CNN-based classifier
- Evaluate model performance using multiple metrics
- Visualize predicted IDC regions across tissue samples

---

🎯 Problem Statement

Given a histopathology image patch, predict whether the patch contains Invasive Ductal Carcinoma (IDC).

This is formulated as a binary image classification problem:

Label| Class
"0"| Non-IDC
"1"| IDC

---

📊 Dataset

The project uses the Breast Histopathology Images dataset.

Dataset Statistics

- Image patches: ~277,524
- Patients: 279
- Image patch size: 50 × 50 pixels
- Task: Binary classification
- Classes: IDC / Non-IDC

Each patient can contribute many image patches. Therefore, the number of image patches is much larger than the number of patients.

---

🔍 Exploratory Data Analysis

Before model training, exploratory analysis was performed to understand:

- Number of patients
- Number of image patches
- Class distribution
- Patient-level variation
- IDC vs non-IDC examples
- Spatial distribution of IDC regions
- Tissue-level patch arrangement

Visual inspection was also performed to understand the visual characteristics of the two classes.

---

⚠️ Patient-Level Data Splitting

A major consideration in this project was preventing data leakage.

Instead of randomly splitting individual image patches, the dataset was divided using patient IDs.

Approximate split:

- Training: 70%
- Development/Validation: 15%
- Testing: 15%

This ensures that patches from the same patient do not appear across different splits.

This provides a more realistic evaluation of how the model performs on previously unseen patients.

---

🖼️ Image Preprocessing

The images were processed using the following pipeline:

1. Load image
2. Convert to RGB
3. Resize to 50 × 50 pixels
4. Apply training augmentation
5. Normalize image channels

Training Augmentation

The following augmentations were used:

- Random horizontal flip
- Random vertical flip

Augmentation helps increase the diversity of training examples and can improve model generalization.

---

🧠 Model Architecture

The primary model used in this project is ResNet-18.

Custom Classification Head

The original classification layer was replaced with a custom head:

ResNet-18
     ↓
512 features
     ↓
Fully Connected Layer
     ↓
256 features
     ↓
ReLU
     ↓
Batch Normalization
     ↓
Dropout
     ↓
2 output classes
     ↓
IDC / Non-IDC

Why ResNet-18?

ResNet-18 provides a good balance between:

- Model complexity
- Computational requirements
- Training efficiency
- Image feature extraction capability

The residual connections also help improve gradient flow during training.

---

⚖️ Handling Class Imbalance

The dataset contains an unequal number of IDC and non-IDC patches.

To reduce the effect of class imbalance, class-weighted Cross-Entropy Loss was used.

This gives greater importance to the minority class during training instead of allowing the model to be dominated by the majority class.

---

⚙️ Training

The model was trained using PyTorch.

Main Configuration

Parameter| Value
Framework| PyTorch
Architecture| ResNet-18
Task| Binary Classification
Batch Size| 32
Image Size| 50 × 50
Loss| Weighted Cross-Entropy
Augmentation| Horizontal + Vertical Flip
Optimizer| Configured in notebook
Device| CPU/GPU depending on environment

A learning-rate search was also performed to identify a suitable learning-rate range, followed by a cyclical learning-rate strategy.

---

📈 Evaluation Metrics

Model performance was evaluated using multiple metrics:

Accuracy

Measures the overall proportion of correctly classified samples.

Precision

Measures how many samples predicted as IDC were actually IDC.

[
Precision = \frac{TP}{TP + FP}
]

Recall

Measures how many actual IDC samples were correctly identified.

[
Recall = \frac{TP}{TP + FN}
]

F1-Score

Combines precision and recall.

[
F1 = 2 \times \frac{Precision \times Recall}
{Precision + Recall}
]

Because the dataset is imbalanced, F1-score, precision, and recall were considered alongside accuracy.

---

🗺️ Tissue-Level Visualization

An additional component of the project reconstructs image patches based on their spatial coordinates.

This allows predictions to be visualized across the tissue region rather than viewing each patch independently.

The visualization can show areas where the model assigns a higher probability to the IDC class.

«These visualizations represent model predictions and should not be interpreted as clinical confirmation of cancer.»

---

🔄 Project Workflow

Breast Histopathology Dataset
            ↓
      Data Exploration
            ↓
   Patient-Level Splitting
            ↓
 Image Preprocessing & Augmentation
            ↓
       Class Balancing
            ↓
        ResNet-18 CNN
            ↓
      Model Training
            ↓
       Validation
            ↓
 Performance Evaluation
            ↓
 Patch-Level Predictions
            ↓
 Tissue-Level Visualization

---

🛠️ Technologies Used

- Python
- PyTorch
- Torchvision
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- PIL / Pillow
- Jupyter Notebook

---

📁 Project Structure

IDC-Detection/
│
├── IDC_Detection.ipynb
├── README.md
│
├── models/
│   └── model_checkpoint.pth
│
├── results/
│   ├── metrics/
│   └── visualizations/
│
└── requirements.txt

The exact structure may vary depending on how the notebook and trained model files are organized.

---

💡 Key Learning Outcomes

Through this project, I gained practical experience in:

- Deep learning for image classification
- CNN architecture and ResNet
- PyTorch model development
- Image preprocessing
- Data augmentation
- Handling class imbalance
- Patient-level dataset splitting
- Preventing data leakage
- Model evaluation
- Learning-rate optimization
- Tissue-level prediction visualization
- Interpreting limitations of medical AI models

---

🚧 Limitations

This project has several limitations:

- The number of patients is relatively limited compared with large-scale clinical datasets.
- The dataset contains class imbalance.
- Histopathology images can contain staining and imaging variations.
- Patient populations and imaging systems may differ between institutions.
- The model has not been clinically validated.
- External validation on an independent dataset is required to assess generalization.

---

🚀 Future Improvements

Future development could include:

1. Larger and more diverse datasets
2. Patient-level cross-validation
3. External validation
4. Stain normalization
5. Advanced data augmentation
6. Fine-tuning pretrained CNN models
7. Threshold optimization
8. Grad-CAM-based explainability
9. Comparison with architectures such as DenseNet and EfficientNet
10. Evaluation across different patient and imaging domains

---

📌 Conclusion

This project demonstrates an end-to-end application of deep learning and computer vision to histopathology image classification.

By combining patient-level data splitting, image augmentation, class-weighted loss, ResNet-18, multi-metric evaluation, and tissue-level visualization, the project provides a practical framework for investigating automated IDC classification.

The results should be interpreted as a research/educational demonstration, rather than evidence of clinical diagnostic performance.

---

👩‍💻 Author

Shiksha Kumari 

Data Science & Machine Learning Student

Areas of Interest

- Data Science
- Machine Learning
- Deep Learning
- Computer Vision
- Artificial Intelligence

---

⭐ Acknowledgment

This project uses the Breast Histopathology Images dataset for educational and research purposes.

If you use or extend this project, please refer to the original dataset source and its associated terms of use.
