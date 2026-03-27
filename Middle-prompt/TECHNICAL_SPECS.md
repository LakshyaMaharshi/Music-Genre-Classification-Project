# Technical Specifications & Requirements

## 📋 ASSIGNMENT CONSTRAINTS

### **Hard Requirements** (Must Follow)
- [x] Framework: **PyTorch** (mandatory)
- [x] Dataset: **GTZAN Genre Collection**
- [x] Image Size: **180x180 pixels** (must resize MEL spectrograms)
- [x] Data Split: **70% train / 20% validation / 10% test**
- [x] Number of Models: **6 models** (all required)
- [x] Code Format: **Single Jupyter notebook**
- [x] Report Format: **CVPR LaTeX template** (4 pages max)
- [x] Code Submission: **code.zip** via ECS Handin
- [x] Report Submission: **report.pdf** via ECS Handin

---

## 🏗️ MODEL ARCHITECTURES

### **Model 1: Fully Connected Network**
```
Type: Multi-layer Perceptron
Input: Flattened image (180×180×3 = 97,200 neurons)
Architecture:
  - Input layer: 97,200 neurons
  - Hidden layer 1: [YOUR CHOICE] neurons
  - Hidden layer 2: [YOUR CHOICE] neurons
  - Output layer: 10 neurons (genres)
  - Activation: ReLU (hidden), Softmax (output)
Optimizer: Adam
Epochs: 50, then 100
```

### **Model 2: Convolutional Neural Network (Base)**
```
Type: CNN
Input: Image (180×180×3)
Architecture (based on Figure 1):
  conv1 → ReLU
  conv2 → ReLU
  MaxPool1 (2×2)
  conv3 → ReLU
  conv4 → ReLU
  MaxPool2 (2×2)
  Flatten
  fc1 → ReLU
  fc2 → ReLU
  output (10 classes)

Hyperparameters to Define:
  - Kernel sizes: [YOUR CHOICE, e.g., 3×3 or 5×5]
  - Channels: [YOUR CHOICE, e.g., 32, 64, 128, 256]
  - FC layer sizes: [YOUR CHOICE]

Optimizer: Adam
Epochs: 50, then 100
```

### **Model 3: CNN + Batch Normalization**
```
Type: CNN with BatchNorm
Input: Image (180×180×3)
Architecture:
  conv1 → BatchNorm2d → ReLU
  conv2 → BatchNorm2d → ReLU
  MaxPool1 (2×2)
  conv3 → BatchNorm2d → ReLU
  conv4 → BatchNorm2d → ReLU
  MaxPool2 (2×2)
  Flatten
  fc1 → ReLU
  fc2 → ReLU
  output (10 classes)

Same hyperparameters as Model 2
Optimizer: Adam
Epochs: 50, then 100
```

### **Model 4: CNN + BatchNorm + RMSProp**
```
Type: CNN with BatchNorm
Input: Image (180×180×3)
Architecture: Exactly same as Model 3
Change: Optimizer only
Optimizer: RMSProp (instead of Adam)
Epochs: 50, then 100
```

### **Model 5: LSTM for Audio**
```
Type: Recurrent Neural Network (LSTM)
Input: Audio sequence (sequence_length × features)
Architecture:
  - LSTM layers: [YOUR CHOICE, e.g., 2-3 layers]
  - Hidden size: [YOUR CHOICE, e.g., 128-256]
  - Bidirectional: [YOUR CHOICE, recommended]
  - Dropout: [YOUR CHOICE, e.g., 0.3-0.5]
  - Fully connected layers for classification
  - Output: 10 classes

Input Format Options:
  Option A: MFCC features
  Option B: Log-mel spectrograms
  Option C: Raw spectrograms

Optimizer: Adam
Epochs: Train until convergence
Convergence: Define criterion (e.g., val loss no improvement for 10 epochs)
```

### **Model 6: LSTM + GAN Augmented Data**
```
Type: RNN + GAN Augmentation

Part A - GAN:
  Generator:
    Input: Noise vector (e.g., 100-dim)
    Output: Synthetic audio features (same shape as real data)
    Architecture: [YOUR CHOICE - transposed conv or LSTM-based]

  Discriminator:
    Input: Audio features (real or fake)
    Output: Probability (real/fake)
    Architecture: [YOUR CHOICE - conv or LSTM-based]

  Training:
    Loss: BCE (Binary Cross Entropy)
    Optimizers: Adam for both G and D
    Generate: Same number of samples as training data

Part B - LSTM:
  Architecture: Same as Model 5
  Data: Original + GAN-generated samples (2× training data)
  Optimizer: Adam
  Epochs: Train until convergence
```

---

## 📊 DATASET SPECIFICATIONS

### **GTZAN Dataset**
```
Total Files: ~1000 audio files (30 seconds each)
Genres: 10 classes
  1. blues
  2. classical
  3. country
  4. disco
  5. hiphop
  6. jazz
  7. metal
  8. pop
  9. reggae
  10. rock

Audio Format:
  - Format: WAV
  - Sample Rate: 22050 Hz
  - Channels: Mono
  - Duration: 30 seconds
  - Bit Depth: 16-bit

MEL Spectrograms:
  - Location: images_original folder
  - Original Size: Variable
  - Required Size: 180×180 (must resize!)
  - Format: PNG
  - Channels: 3 (RGB)
```

### **Data Split**
```
Training:   70% (~700 files) - Use for model training
Validation: 20% (~200 files) - Use for hyperparameter tuning
Test:       10% (~100 files) - Use ONLY for final evaluation

Rules:
- Stratified split (equal genre distribution in each set)
- Create split ONCE, use same split for ALL models
- Never use test set during training/validation!
- Save split indices to ensure consistency
```

---

## ⚙️ TRAINING SPECIFICATIONS

### **Common Training Settings**

```python
# Reproducibility
RANDOM_SEED = 42  # Set this everywhere!
torch.manual_seed(RANDOM_SEED)
np.random.seed(RANDOM_SEED)

# Training
BATCH_SIZE = 32  # or 64, tune based on GPU memory
LEARNING_RATE = 0.001  # Standard starting point
DEVICE = 'cuda' if torch.cuda.is_available() else 'cpu'

# Loss Function
CRITERION = nn.CrossEntropyLoss()

# Optimizers
Adam: torch.optim.Adam(model.parameters(), lr=LEARNING_RATE)
RMSProp: torch.optim.RMSProp(model.parameters(), lr=LEARNING_RATE)

# Epochs
Models 1-4: 50 epochs first, then 100 epochs total
Models 5-6: Until convergence (e.g., early stopping after 10 epochs no improvement)
```

### **Training Loop Template**

```python
def train_epoch(model, dataloader, criterion, optimizer, device):
    model.train()
    running_loss = 0.0
    correct = 0
    total = 0

    for inputs, labels in dataloader:
        inputs, labels = inputs.to(device), labels.to(device)

        optimizer.zero_grad()
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()

        running_loss += loss.item()
        _, predicted = outputs.max(1)
        total += labels.size(0)
        correct += predicted.eq(labels).sum().item()

    epoch_loss = running_loss / len(dataloader)
    epoch_acc = 100. * correct / total
    return epoch_loss, epoch_acc

def validate_epoch(model, dataloader, criterion, device):
    model.eval()
    running_loss = 0.0
    correct = 0
    total = 0

    with torch.no_grad():
        for inputs, labels in dataloader:
            inputs, labels = inputs.to(device), labels.to(device)
            outputs = model(inputs)
            loss = criterion(outputs, labels)

            running_loss += loss.item()
            _, predicted = outputs.max(1)
            total += labels.size(0)
            correct += predicted.eq(labels).sum().item()

    epoch_loss = running_loss / len(dataloader)
    epoch_acc = 100. * correct / total
    return epoch_loss, epoch_acc
```

---

## 📈 EVALUATION METRICS

### **Required Metrics**

```python
# Overall Metrics
- Accuracy: (TP + TN) / Total
- Loss: CrossEntropyLoss value

# Per-Class Metrics (for each genre)
- Precision: TP / (TP + FP)
- Recall: TP / (TP + FN)
- F1-Score: 2 × (Precision × Recall) / (Precision + Recall)

# Confusion Matrix
- 10×10 matrix (rows: true labels, cols: predicted labels)
- Use sklearn.metrics.confusion_matrix

# Training Metrics (track per epoch)
- Training loss
- Training accuracy
- Validation loss
- Validation accuracy
```

### **Evaluation Code Template**

```python
from sklearn.metrics import classification_report, confusion_matrix
import seaborn as sns
import matplotlib.pyplot as plt

def evaluate_model(model, test_loader, device, genre_names):
    model.eval()
    all_preds = []
    all_labels = []

    with torch.no_grad():
        for inputs, labels in test_loader:
            inputs = inputs.to(device)
            outputs = model(inputs)
            _, predicted = outputs.max(1)

            all_preds.extend(predicted.cpu().numpy())
            all_labels.extend(labels.numpy())

    # Accuracy
    accuracy = 100. * np.sum(np.array(all_preds) == np.array(all_labels)) / len(all_labels)

    # Classification Report
    report = classification_report(all_labels, all_preds,
                                   target_names=genre_names,
                                   output_dict=True)

    # Confusion Matrix
    cm = confusion_matrix(all_labels, all_preds)

    return accuracy, report, cm
```

---

## 🎨 VISUALIZATION REQUIREMENTS

### **Required Plots**

1. **Training Curves** (for each model):
   - X-axis: Epochs
   - Y-axis: Loss / Accuracy
   - Two subplots: Loss and Accuracy
   - Both train and validation curves

2. **Model Comparison**:
   - Bar chart: Test accuracy for all 6 models
   - Side-by-side comparison

3. **Confusion Matrices**:
   - One per model (6 total)
   - Heatmap format
   - Genre labels on axes

4. **Additional Analysis Plots**:
   - Per-genre F1-scores comparison
   - Training time comparison
   - Sample predictions visualization

### **Plot Styling**

```python
# Use these settings for consistent, professional plots
plt.rcParams['figure.figsize'] = (10, 6)
plt.rcParams['font.size'] = 12
plt.rcParams['axes.labelsize'] = 12
plt.rcParams['axes.titlesize'] = 14
plt.rcParams['legend.fontsize'] = 10
plt.style.use('seaborn-v0_8-darkgrid')  # or 'ggplot'
```

---

## 🔍 KEY COMPARISONS TO ANALYZE

### **Required Analysis** (for Report Discussion)

1. **FC vs CNN** (Model 1 vs Models 2-4):
   - Which performs better?
   - Why does CNN work better for images?
   - Discuss spatial feature extraction

2. **Impact of Batch Normalization** (Model 2 vs Model 3):
   - Does BatchNorm improve accuracy?
   - Does it speed up convergence?
   - Training stability comparison

3. **Optimizer Comparison** (Model 3 vs Model 4):
   - Adam vs RMSProp performance
   - Convergence characteristics
   - When to use each optimizer

4. **Image vs Audio** (Models 1-4 vs Models 5-6):
   - Which input modality works better?
   - Explain why
   - Discuss temporal vs spatial features

5. **Data Augmentation** (Model 5 vs Model 6):
   - Does GAN augmentation help?
   - Quality of synthetic data
   - When is augmentation beneficial?

6. **Best Overall Model**:
   - Identify best performing model
   - Justify why it performs best
   - Discuss trade-offs (accuracy vs complexity vs training time)

---

## 🧪 TESTING & VALIDATION

### **Unit Tests to Implement**

```python
# Test 1: Data Loading
def test_data_loading():
    assert len(train_dataset) == expected_train_size
    assert len(val_dataset) == expected_val_size
    assert len(test_dataset) == expected_test_size
    print("✓ Data split correct")

# Test 2: Data Shapes
def test_data_shapes():
    image, label = train_dataset[0]
    assert image.shape == (3, 180, 180)
    assert 0 <= label < 10
    print("✓ Data shapes correct")

# Test 3: Model Forward Pass
def test_model_forward(model):
    dummy_input = torch.randn(1, 3, 180, 180)
    output = model(dummy_input)
    assert output.shape == (1, 10)
    print("✓ Model forward pass works")

# Test 4: Batch Processing
def test_batch_processing():
    batch = next(iter(train_loader))
    images, labels = batch
    assert images.shape == (BATCH_SIZE, 3, 180, 180)
    assert labels.shape == (BATCH_SIZE,)
    print("✓ Batch processing works")

# Test 5: Model Training Step
def test_training_step(model):
    model.train()
    batch = next(iter(train_loader))
    images, labels = batch
    images, labels = images.to(device), labels.to(device)

    optimizer.zero_grad()
    outputs = model(images)
    loss = criterion(outputs, labels)
    loss.backward()
    optimizer.step()

    assert loss.item() > 0
    print("✓ Training step works")
```

---

## 📐 RECOMMENDED HYPERPARAMETERS

### **Model 1 (FC Network)**
```python
INPUT_SIZE = 180 * 180 * 3  # 97,200
HIDDEN1_SIZE = 1024  # First hidden layer
HIDDEN2_SIZE = 512   # Second hidden layer
OUTPUT_SIZE = 10     # 10 genres

LEARNING_RATE = 0.001
BATCH_SIZE = 64
EPOCHS = 50  # then continue to 100
```

### **Models 2-4 (CNNs)**
```python
# Convolutional Layers
CONV1_CHANNELS = 32
CONV2_CHANNELS = 64
CONV3_CHANNELS = 128
CONV4_CHANNELS = 256
KERNEL_SIZE = 3  # or 5
POOL_SIZE = 2

# Fully Connected
FC1_SIZE = 512
FC2_SIZE = 256
OUTPUT_SIZE = 10

LEARNING_RATE = 0.001
BATCH_SIZE = 32  # CNNs use more memory
EPOCHS = 50  # then continue to 100
```

### **Models 5-6 (LSTMs)**
```python
# Audio Features
SAMPLE_RATE = 22050
N_MFCC = 40  # if using MFCC
N_MEL = 128  # if using mel spectrograms
SEQUENCE_LENGTH = 1024  # adjust based on audio length

# LSTM Architecture
NUM_LAYERS = 2  # or 3
HIDDEN_SIZE = 256  # or 512
BIDIRECTIONAL = True
DROPOUT = 0.3

# Fully Connected
FC_SIZE = 128
OUTPUT_SIZE = 10

LEARNING_RATE = 0.001
BATCH_SIZE = 32
EARLY_STOPPING_PATIENCE = 10  # epochs
```

### **GAN (Model 6)**
```python
# Generator
NOISE_DIM = 100
G_HIDDEN = 256

# Discriminator
D_HIDDEN = 256

# Training
G_LEARNING_RATE = 0.0002
D_LEARNING_RATE = 0.0002
LABEL_SMOOTHING = 0.9  # Use 0.9 instead of 1.0 for real labels
GAN_EPOCHS = 200  # or until convergence

# Data Generation
NUM_SYNTHETIC_SAMPLES = len(train_dataset)  # Same as original training data
```

---

## 🧮 EXPECTED PERFORMANCE RANGES

### **Baseline Expectations**
```
Random Guessing: 10% accuracy (10 classes)
Minimum Acceptable: >50% accuracy
Good Performance: 60-70% accuracy
Excellent Performance: >75% accuracy
State-of-the-art: 80-90% accuracy
```

### **Typical Performance Hierarchy**
```
Expected: Net1 < Net2 < Net3 ≈ Net4 < Net5 ≈ Net6

Rationale:
- CNNs better than FC for images
- BatchNorm helps training
- Optimizer choice has moderate impact
- Audio-based models capture temporal info
- GAN augmentation may or may not help
```

---

## 🛠️ REQUIRED LIBRARIES

### **Core Requirements**
```
torch>=2.0.0
torchvision>=0.15.0
torchaudio>=2.0.0
numpy>=1.24.0
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.12.0
scikit-learn>=1.3.0
librosa>=0.10.0
jupyter>=1.0.0
```

### **Optional but Recommended**
```
tensorboard  # For visualizing training
tqdm         # For progress bars
pillow       # For image handling
kaggle       # For dataset download
```

### **Installation Command**
```bash
pip install torch torchvision torchaudio numpy pandas matplotlib seaborn scikit-learn librosa jupyter
```

---

## 📁 PROJECT DIRECTORY STRUCTURE

```
Music Project/
├── PROJECT_REFERENCE.md         # Detailed task planner (this guide)
├── QUICK_START.md               # Quick reference guide
├── TASK_TRACKER.md              # Progress tracking
├── TECHNICAL_SPECS.md           # This file
├── requirements.txt             # Python dependencies
├── README.md                    # Setup instructions
│
├── notebooks/
│   └── music_genre_classification.ipynb  # Main notebook (submit this)
│
├── data/
│   └── GTZAN/
│       ├── genres/              # Audio files by genre
│       │   ├── blues/
│       │   ├── classical/
│       │   └── ... (10 genres)
│       └── images_original/     # MEL spectrograms
│
├── models/                      # Model checkpoints
│   ├── net1_epoch50.pth
│   ├── net1_epoch100.pth
│   ├── net2_epoch100.pth
│   └── ... (all models)
│
├── results/
│   ├── metrics/                 # CSV/JSON metrics
│   │   ├── model1_history.csv
│   │   └── ...
│   ├── plots/                   # Visualization outputs
│   │   ├── training_curves.png
│   │   ├── confusion_matrices.png
│   │   └── ...
│   └── analysis/
│       └── performance_comparison.txt
│
└── report/
    ├── report.tex               # LaTeX source
    ├── report.pdf               # Final PDF (submit this)
    └── figures/                 # Figures for report
        ├── figure1.png
        └── ...
```

---

## 🎓 REPORT REQUIREMENTS

### **Part 1: Implementation & Results (3 pages)**

**Structure:**
```
1. Introduction (0.3-0.5 pages)
   - Problem overview
   - Dataset description
   - Objectives

2. Methodology (1-1.5 pages)
   - Data preprocessing
   - Model architectures (all 6 models)
   - Training procedures
   - Evaluation metrics

3. Results (0.7-1 pages)
   - Performance tables
   - Key visualizations (2-3 figures max)
   - Numerical results

4. Discussion (0.5-0.7 pages)
   - Comparative analysis
   - Insights and findings
   - Limitations
```

**Figures to Include (select 2-4):**
- Training curves comparison
- Test accuracy bar chart
- Best model's confusion matrix
- Per-genre performance heatmap

**Tables to Include:**
- Model performance comparison (accuracy, precision, recall, F1)
- Training time and complexity comparison

### **Part 2: Deep Learning Topic Reflection (1 page)**

**Topic Options:**
1. Convolutional Neural Networks
2. Recurrent Neural Networks and LSTMs
3. Generative Adversarial Networks
4. Batch Normalization and Optimization
5. Transfer Learning (if explored)

**Structure:**
```
1. Topic Importance (2-3 paragraphs)
2. Current Technologies (2-3 paragraphs)
3. Implementation Analysis (2 paragraphs)
4. Impact Assessment (2 paragraphs)
5. Future Vision (1-2 paragraphs)
```

---

## ⚡ OPTIMIZATION TIPS

### **Speed Up Training**
1. Use GPU (10-50× faster)
2. Use DataLoader num_workers > 0
3. Use mixed precision training (torch.cuda.amp)
4. Use larger batch sizes if memory allows
5. Profile code to find bottlenecks

### **Improve Accuracy**
1. Data augmentation (rotation, shift, noise)
2. Ensemble models (average predictions)
3. Hyperparameter tuning (grid search)
4. Increase model capacity carefully
5. Use learning rate scheduling

### **Reduce Memory Usage**
1. Reduce batch size
2. Use gradient accumulation
3. Clear GPU cache periodically
4. Use torch.no_grad() for inference
5. Delete large variables after use

---

## 🚨 CRITICAL REMINDERS

### **DON'T:**
- ❌ Don't train on test set
- ❌ Don't look at test set until final evaluation
- ❌ Don't change test set between models
- ❌ Don't forget to resize images to 180×180
- ❌ Don't skip saving model checkpoints
- ❌ Don't hardcode paths in notebook
- ❌ Don't commit large files to git
- ❌ Don't exceed 4 pages in report

### **DO:**
- ✅ Set random seeds everywhere
- ✅ Save checkpoints after training
- ✅ Track all metrics systematically
- ✅ Use same train/val/test split for all models
- ✅ Comment your code thoroughly
- ✅ Validate data shapes frequently
- ✅ Test code on small subset first
- ✅ Start early (GAN is time-consuming!)

---

## 📚 USEFUL CODE SNIPPETS

### **Image Transforms**
```python
from torchvision import transforms

train_transform = transforms.Compose([
    transforms.Resize((180, 180)),  # Required!
    transforms.RandomHorizontalFlip(),  # Optional augmentation
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406],
                        std=[0.229, 0.224, 0.225])
])

test_transform = transforms.Compose([
    transforms.Resize((180, 180)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406],
                        std=[0.229, 0.224, 0.225])
])
```

### **Save/Load Models**
```python
# Save
torch.save({
    'epoch': epoch,
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'loss': loss,
    'accuracy': accuracy,
    'history': history
}, f'models/net{model_num}_epoch{epoch}.pth')

# Load
checkpoint = torch.load('models/net1_epoch100.pth')
model.load_state_dict(checkpoint['model_state_dict'])
```

### **Set Random Seeds**
```python
import random
import numpy as np
import torch

def set_seed(seed=42):
    random.seed(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    torch.backends.cudnn.deterministic = True
    torch.backends.cudnn.benchmark = False

set_seed(42)
```

---

## 🎯 SUCCESS CRITERIA

### **Code Quality Rubric**
- [ ] All 6 models implemented correctly
- [ ] Code is well-organized and documented
- [ ] Runs without errors from start to finish
- [ ] Reproducible results (random seeds)
- [ ] Professional coding practices

### **Report Quality Rubric**
- [ ] Clear and concise writing
- [ ] Proper CVPR formatting
- [ ] Insightful analysis and discussion
- [ ] Professional figures and tables
- [ ] Within 4-page limit

### **Model Performance Rubric**
- [ ] All models trained to completion
- [ ] Reasonable accuracy (>50%)
- [ ] Proper evaluation on test set
- [ ] Comprehensive metrics collected

### **Submission Rubric**
- [ ] All deliverables submitted
- [ ] Correct file formats
- [ ] Before deadline
- [ ] Complete and functional

---

## 🔗 USEFUL RESOURCES

### **PyTorch Documentation**
- Tutorial: https://pytorch.org/tutorials/
- nn.Module: https://pytorch.org/docs/stable/generated/torch.nn.Module.html
- DataLoader: https://pytorch.org/docs/stable/data.html

### **GTZAN Dataset**
- Original Paper: Tzanetakis & Cook (2002)
- Kaggle: Search "GTZAN Genre Collection"

### **GAN Resources**
- Original GAN Paper: Goodfellow et al. (2014)
- PyTorch GAN Tutorial: https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html

### **LaTeX/CVPR Template**
- CVPR Template: https://github.com/cvpr-org/author-kit

### **Audio Processing**
- librosa documentation: https://librosa.org/doc/latest/
- torchaudio: https://pytorch.org/audio/stable/

---

**This file contains all technical specifications. Use it as a quick reference while implementing!**
