# Music Genre Classification Project - Task Reference Guide

## 📌 Project Overview

**Course**: Deep Learning Technologies (COMP6252)
**Assignment**: Coursework 1 - Music Genre Classification
**Dataset**: GTZAN (10 genres, ~1000 audio files)
**Deadline**: Tuesday 28th April 2026, 16:00 (ECS Handin)
**Handin URL**: https://handin.ecs.soton.ac.uk/handin/2526/COMP6252/1
**Deliverables**:
- Code submission (Jupyter notebook as code.zip)
- Report (4 pages max: 3 pages implementation + 1 page reflection)

**Marking Breakdown** (total 20 marks):
- Part 1 — Implementation, Results & Discussion: **16 marks**
- Part 2 — Topic Reflection: **4 marks**
- Marks awarded for: successful task completion, evidence of understanding, well-structured/commented code, professionalism, report quality

---

## 🎯 Project Objectives

Implement and compare **6 different neural network models** for music genre classification:

### Image-based Models (MEL Spectrograms)
1. **Model 1**: Fully Connected Network (2 hidden layers)
2. **Model 2**: Convolutional Neural Network (Base architecture)
3. **Model 3**: CNN + Batch Normalization
4. **Model 4**: CNN + Batch Normalization + RMSProp optimizer

### Audio-based Models (Raw Audio/Spectrograms)
5. **Model 5**: RNN with LSTMs
6. **Model 6**: RNN with LSTMs + GAN-augmented data

---

## 📊 SEQUENTIAL TASK PLANNER

### **PHASE 1: PROJECT SETUP & DATA PREPARATION**

#### **Task 1.1: Environment Setup & Dataset Download**
**Estimated Tokens**: ~5K context needed
**Complexity**: Low
**Dependencies**: None

**What to Provide to Claude:**
```
Project: Music Genre Classification using GTZAN dataset

Task: Set up the project environment and download the dataset

Requirements:
1. Create project directory structure:
   - /data (for GTZAN dataset)
   - /models (for saved model checkpoints)
   - /results (for plots and metrics)
   - /notebooks (for Jupyter notebook)

2. Install required libraries:
   - PyTorch (torch, torchvision, torchaudio)
   - numpy, pandas, matplotlib, seaborn
   - librosa (for audio processing)
   - scikit-learn

3. Download GTZAN dataset:
   - Source: Kaggle GTZAN Genre Collection
   - Structure: 10 genres folder with audio files and images_original (MEL spectrograms)
   - Verify: 10 genres × ~100 files each

4. Create a requirements.txt file with all dependencies

Please implement this setup step by step.
```

---

#### **Task 1.2: Data Exploration & Preprocessing Pipeline**
**Estimated Tokens**: ~10K context needed
**Complexity**: Medium
**Dependencies**: Task 1.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - GTZAN dataset

Task: Explore dataset and create preprocessing pipeline

Context:
- Dataset downloaded in /data/GTZAN
- 10 genres: blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock
- Two data types: MEL spectrogram images + raw audio files

Requirements:
1. Explore dataset structure:
   - Count files per genre
   - Check image dimensions and formats
   - Check audio file properties (sample rate, duration, format)

2. Create preprocessing functions:
   - For images: Resize MEL spectrograms to 180x180 using torchvision.transforms.Resize
   - For audio: Load and preprocess audio files using librosa or torchaudio
   - Normalize data appropriately

3. Create train/validation/test split:
   - Training: 70%
   - Validation: 20%
   - Test: 10%
   - Ensure stratified split (equal genre distribution)

4. Visualize:
   - Sample MEL spectrograms from each genre
   - Distribution of data across splits

Please create a comprehensive data exploration notebook section.
```

---

#### **Task 1.3: Base DataLoader Implementation**
**Estimated Tokens**: ~8K context needed
**Complexity**: Medium
**Dependencies**: Task 1.2 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification

Task: Implement PyTorch Dataset and DataLoader classes

Context:
- Data splits created: train/val/test (70/20/10)
- Two data types needed: images (180x180) and audio

Requirements:
1. Create GTZANImageDataset class:
   - Load MEL spectrogram images
   - Apply transforms (resize to 180x180, normalize)
   - Return (image_tensor, label)

2. Create GTZANAudioDataset class:
   - Load raw audio files
   - Convert to appropriate format (spectrograms or features)
   - Return (audio_tensor, label)

3. Create DataLoaders:
   - Implement for train/val/test sets
   - Use appropriate batch sizes (e.g., 32 or 64)
   - Enable shuffling for training set
   - Set random seed for reproducibility

4. Test DataLoaders:
   - Print batch shapes
   - Verify label distributions
   - Visualize sample batches

Please implement robust DataLoader classes with error handling.
```

---

### **PHASE 2: IMAGE-BASED MODELS (Models 1-4)**

#### **Task 2.1: Model 1 - Fully Connected Network**
**Estimated Tokens**: ~12K context needed
**Complexity**: Medium
**Dependencies**: Phase 1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 1

Task: Implement and train Fully Connected Neural Network

Context:
- Input: 180x180x3 MEL spectrogram images (flattened to vector)
- Output: 10 classes (genres)
- DataLoaders ready from previous task

Requirements:
1. Define Net1 architecture:
   - Input layer: 180*180*3 = 97,200 neurons
   - Hidden layer 1: Choose appropriate size (e.g., 512-1024)
   - Hidden layer 2: Choose appropriate size (e.g., 256-512)
   - Output layer: 10 neurons (genres)
   - Activation: ReLU for hidden layers, Softmax for output

2. Training setup:
   - Loss function: CrossEntropyLoss
   - Optimizer: Adam
   - Learning rate: Start with 0.001 (tune if needed)
   - Batch size: 32 or 64

3. Training process:
   - Train for 50 epochs first
   - Save metrics (loss, accuracy) per epoch
   - Train for 100 epochs total
   - Save final model checkpoint

4. Validation:
   - Evaluate on validation set after each epoch
   - Track validation accuracy and loss
   - Implement early stopping if needed

5. Output:
   - Plot training/validation curves
   - Print final test accuracy
   - Save model weights

Please implement Net1 with comprehensive logging and visualization.
```

---

#### **Task 2.2: Model 2 - Convolutional Neural Network (Base)**
**Estimated Tokens**: ~15K context needed
**Complexity**: Medium-High
**Dependencies**: Task 2.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 2

Task: Implement CNN architecture based on assignment Figure 1

Context:
- Input: 180x180x3 MEL spectrogram images
- Architecture reference: Figure 1 in assignment PDF
- Previous model (Net1) baseline established

Requirements:
1. Define Net2 architecture following Figure 1 structure:
   - conv1 → ReLU → conv2 → ReLU → MaxPool1
   - conv3 → ReLU → conv4 → ReLU → MaxPool2
   - Flatten → fc1 → ReLU → fc2 → ReLU → output

2. Select hyperparameters:
   - Kernel sizes (e.g., 3x3 or 5x5)
   - Number of channels per conv layer
   - MaxPool kernel sizes (e.g., 2x2)
   - Fully connected layer sizes
   - Justify your selections

3. Training setup (same as Model 1):
   - Optimizer: Adam
   - Loss: CrossEntropyLoss
   - Train 50 epochs, then 100 epochs
   - Save metrics and model

4. Comparison with Model 1:
   - Compare test accuracy
   - Compare training time
   - Analyze performance differences

5. Output:
   - Training/validation curves
   - Confusion matrix on test set
   - Comparison table with Model 1

Please implement Net2 with architectural justification and comparison analysis.
```

---

#### **Task 2.3: Model 3 - CNN with Batch Normalization**
**Estimated Tokens**: ~12K context needed
**Complexity**: Medium
**Dependencies**: Task 2.2 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 3

Task: Add Batch Normalization to CNN architecture

Context:
- Base architecture: Net2 from previous task
- Goal: Improve training stability and performance
- Batch normalization should be added after each convolutional layer

Requirements:
1. Modify Net2 architecture to create Net3:
   - conv1 → BatchNorm2d → ReLU
   - conv2 → BatchNorm2d → ReLU → MaxPool1
   - conv3 → BatchNorm2d → ReLU
   - conv4 → BatchNorm2d → ReLU → MaxPool2
   - Fully connected layers (same as Net2)

2. Training setup (same as previous models):
   - Optimizer: Adam
   - Train 50 epochs, then 100 epochs
   - Save metrics and model

3. Analysis:
   - Compare with Net2 (with and without batch norm)
   - Analyze convergence speed
   - Compare final test accuracy
   - Check if overfitting is reduced

4. Output:
   - Training/validation curves (overlay Net2 for comparison)
   - Performance comparison table
   - Analysis of batch normalization impact

Please implement Net3 and provide detailed comparison with Net2.
```

---

#### **Task 2.4: Model 4 - CNN with Batch Norm + RMSProp**
**Estimated Tokens**: ~10K context needed
**Complexity**: Low-Medium
**Dependencies**: Task 2.3 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 4

Task: Test RMSProp optimizer with batch-normalized CNN

Context:
- Architecture: Same as Net3 (CNN + Batch Normalization)
- Change: Replace Adam optimizer with RMSProp
- Goal: Compare optimizer performance

Requirements:
1. Use Net3 architecture (exact same as Task 2.3)

2. Training setup:
   - Optimizer: RMSProp (instead of Adam)
   - Learning rate: Start with 0.001 (may need tuning)
   - All other parameters same as Net3
   - Train 50 epochs, then 100 epochs

3. Analysis:
   - Compare Net4 (RMSProp) vs Net3 (Adam)
   - Analyze convergence behavior
   - Compare final test accuracy
   - Discuss optimizer characteristics

4. Output:
   - Training/validation curves (overlay Net3)
   - Performance comparison table (Models 1-4)
   - Analysis of optimizer impact

Please implement Net4 and provide comparative analysis of Adam vs RMSProp.
```

---

### **PHASE 3: AUDIO-BASED MODELS (Models 5-6)**

#### **Task 3.1: Audio Preprocessing for RNN**
**Estimated Tokens**: ~15K context needed
**Complexity**: Medium-High
**Dependencies**: Phase 1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Audio Preprocessing

Task: Prepare raw audio data for RNN/LSTM processing

Context:
- Raw audio files in GTZAN dataset (30-second clips)
- Need sequence data for LSTM processing
- Should extract temporal features

Requirements:
1. Audio loading:
   - Use librosa or torchaudio
   - Load audio files at consistent sample rate (e.g., 22050 Hz)
   - Handle mono/stereo conversion

2. Feature extraction (choose ONE approach):
   - Option A: MFCC features (Mel-Frequency Cepstral Coefficients)
   - Option B: Log-mel spectrograms
   - Option C: Raw spectrograms
   - Justify your choice

3. Sequence preparation:
   - Convert audio to sequence of feature vectors
   - Choose appropriate sequence length/time steps
   - Handle variable-length sequences (padding or truncation)

4. Create GTZANAudioSequenceDataset:
   - Return (sequence_tensor, label) tuples
   - Shape: (batch, sequence_length, features)
   - Test with DataLoader

5. Visualization:
   - Plot extracted features for sample audios
   - Show feature distributions

Please implement audio preprocessing pipeline suitable for LSTM input.
```

---

#### **Task 3.2: Model 5 - RNN with LSTMs**
**Estimated Tokens**: ~15K context needed
**Complexity**: High
**Dependencies**: Task 3.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 5

Task: Implement LSTM-based RNN for audio classification

Context:
- Input: Audio sequences prepared in Task 3.1
- Output: 10 genre classes
- This is the first audio-based model

Requirements:
1. Define Net5 architecture:
   - Input: (batch, sequence_length, features)
   - LSTM layers: Choose number of layers (e.g., 2-3)
   - Hidden units: Choose size (e.g., 128-256)
   - Bidirectional LSTM (optional but recommended)
   - Fully connected layers for classification
   - Dropout for regularization

2. Training setup:
   - Optimizer: Adam
   - Loss: CrossEntropyLoss
   - Convergence criterion: Define (e.g., no improvement for 10 epochs)
   - Train until convergence

3. Hyperparameter tuning:
   - Experiment with LSTM layers, hidden size
   - Adjust learning rate if needed
   - Report final configuration

4. Analysis:
   - Compare with best image-based model (Models 1-4)
   - Analyze temporal patterns learned
   - Identify challenging genres for audio approach

5. Output:
   - Training/validation curves
   - Test set performance
   - Confusion matrix
   - Model checkpoint

Please implement Net5 with justification for design choices.
```

---

#### **Task 3.3: Model 6 Part A - GAN Implementation for Data Augmentation**
**Estimated Tokens**: ~20K context needed
**Complexity**: Very High
**Dependencies**: Task 3.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - GAN Implementation

Task: Build GAN to generate synthetic audio samples for data augmentation

Context:
- Training data: GTZAN audio files (~700-800 samples after 70% split)
- Goal: Generate same number of synthetic samples as training data
- Use GAN to augment dataset for Model 6

Requirements:
1. Define Generator architecture:
   - Input: Noise vector (e.g., 100-dim)
   - Output: Audio features matching training data format
   - Use transposed convolutions or LSTM-based generator
   - Output shape should match real audio feature shape

2. Define Discriminator architecture:
   - Input: Audio features (real or fake)
   - Output: Probability of being real (single value)
   - Use convolutional or LSTM-based discriminator

3. GAN training:
   - Loss: Binary Cross Entropy
   - Optimizers: Adam for both G and D
   - Train discriminator and generator alternately
   - Training epochs: Until GAN converges (monitor losses)

4. Synthetic data generation:
   - Generate ~700-800 synthetic audio samples
   - Generate samples for each genre (balanced)
   - Save generated samples

5. Quality validation:
   - Visualize real vs fake audio features
   - Check if discriminator is confused (good sign)
   - Manual inspection of generated samples

6. Output:
   - GAN training loss curves (G and D losses)
   - Sample generated audio visualizations
   - Saved synthetic dataset

Notes:
- GAN training can be unstable - implement techniques like:
  - Label smoothing
  - Learning rate scheduling
  - Gradient clipping
- This is the most complex task - take time to implement properly

Please implement GAN for audio data augmentation with quality checks.
```

---

#### **Task 3.4: Model 6 Part B - LSTM with GAN-Augmented Data**
**Estimated Tokens**: ~12K context needed
**Complexity**: Medium
**Dependencies**: Task 3.2 and 3.3 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Model 6

Task: Train LSTM with GAN-augmented dataset

Context:
- Base model: Net5 (LSTM from Task 3.2)
- Augmented data: Original training data + GAN-generated samples
- Goal: Test if data augmentation improves performance

Requirements:
1. Prepare augmented dataset:
   - Combine original training data with GAN-generated samples
   - Verify balanced genre distribution
   - Create new DataLoader with augmented data

2. Use Net5 architecture (same as Model 5):
   - Same LSTM configuration
   - Same hyperparameters
   - Only difference: augmented training data

3. Training:
   - Train until convergence
   - Use same convergence criterion as Model 5
   - Save metrics per epoch

4. Comparison analysis:
   - Net5 (original data) vs Net6 (augmented data)
   - Test on same test set (original, not augmented!)
   - Compare accuracy, precision, recall, F1-score
   - Analyze if GAN augmentation helped

5. Output:
   - Training curves (overlay Net5 for comparison)
   - Performance comparison table
   - Discussion: Did augmentation help? Why/why not?

Please implement Net6 and provide thorough comparison with Net5.
```

---

### **PHASE 4: EVALUATION & ANALYSIS**

#### **Task 4.1: Comprehensive Performance Metrics**
**Estimated Tokens**: ~10K context needed
**Complexity**: Medium
**Dependencies**: All models (1-6) trained

**What to Provide to Claude:**
```
Project: Music Genre Classification - Final Evaluation

Task: Evaluate all 6 models on test set with comprehensive metrics

Context:
- All 6 models trained and checkpoints saved
- Test set: 10% of data (same for all models)
- Need comprehensive comparison

Requirements:
1. Load all 6 trained models

2. Evaluate each model on test set:
   - Overall accuracy
   - Per-class precision, recall, F1-score
   - Confusion matrix (10x10 for each model)

3. Create comparison tables:
   - Table 1: Overall performance (accuracy for each model)
   - Table 2: Training time comparison
   - Table 3: Model complexity (# parameters)
   - Table 4: Per-genre performance (best/worst genres)

4. Statistical analysis:
   - Identify which genres are easiest to classify
   - Identify which genres are most confused
   - Analyze misclassification patterns

5. Output:
   - CSV files with all metrics
   - Performance summary tables
   - Save for report section

Please evaluate all models and create comprehensive comparison tables.
```

---

#### **Task 4.2: Visualization & Results Analysis**
**Estimated Tokens**: ~12K context needed
**Complexity**: Medium
**Dependencies**: Task 4.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Results Visualization

Task: Create publication-quality visualizations for all results

Context:
- All metrics collected from Task 4.1
- Need figures for report and analysis

Requirements:
1. Training curves:
   - Plot training/validation loss for each model
   - Plot training/validation accuracy for each model
   - Create subplot grid showing all 6 models

2. Model comparison:
   - Bar chart: Test accuracy for all 6 models
   - Bar chart: Training time comparison
   - Line plot: Convergence speed comparison

3. Confusion matrices:
   - Generate 6 confusion matrices (one per model)
   - Create 2x3 subplot grid with all matrices
   - Highlight frequent misclassifications

4. Per-genre analysis:
   - Heatmap: F1-scores per genre per model
   - Identify strongest/weakest performing genres
   - Visualize which models excel at which genres

5. Architecture comparison:
   - FC vs CNN performance
   - Impact of batch normalization (Net2 vs Net3)
   - Impact of optimizer (Net3 vs Net4)
   - Image-based vs Audio-based (Net1-4 vs Net5-6)
   - Impact of GAN augmentation (Net5 vs Net6)

Please create all visualizations with clear labels and legends, suitable for academic report.
```

---

#### **Task 4.3: Results Interpretation & Insights**
**Estimated Tokens**: ~8K context needed
**Complexity**: Low-Medium
**Dependencies**: Task 4.2 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Results Interpretation

Task: Analyze results and extract insights for report

Context:
- All models evaluated
- All visualizations created
- Need to write discussion section

Requirements:
1. Comparative analysis:
   - Why did CNNs outperform/underperform FC networks?
   - How did batch normalization affect performance?
   - What's the impact of optimizer choice (Adam vs RMSProp)?
   - Do audio-based models outperform image-based models?
   - Did GAN augmentation improve LSTM performance?

2. Genre-specific insights:
   - Which genres are easiest to classify? Why?
   - Which genres are most confused? Why?
   - Are there patterns (e.g., rock/metal confusion)?

3. Model strengths/weaknesses:
   - When would you use each model?
   - What are computational trade-offs?
   - Which model is best overall?

4. Lessons learned:
   - What worked well?
   - What didn't work as expected?
   - What would you do differently?

5. Output:
   - Written analysis (bullet points or paragraphs)
   - Key insights for report discussion section
   - Recommendations for future work

Please provide comprehensive analysis and insights based on results.
```

---

### **PHASE 5: REPORT WRITING**

#### **Task 5.1: Report Part 1 - Implementation & Results (3 pages)**
**Estimated Tokens**: ~15K context needed
**Complexity**: Medium
**Dependencies**: Phase 4 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Report Writing

Task: Write main report section (3 pages max)

Context:
- All models implemented and evaluated
- All metrics and visualizations ready
- Using CVPR LaTeX template

Requirements:
1. Introduction (0.5 pages):
   - Problem statement: Music genre classification
   - Dataset: GTZAN (10 genres)
   - Objective: Compare 6 different DL approaches
   - Overview of models

2. Methodology (1 page):
   - Dataset description and preprocessing
   - Data split: 70/20/10
   - Model architectures (brief description of each Net1-6)
   - Training details: optimizers, loss, epochs, hyperparameters
   - Evaluation metrics: accuracy, precision, recall, F1

3. Results (1 page):
   - Performance table: All 6 models with test accuracy
   - Training curves figure (select most informative)
   - Confusion matrices (select 2-3 most interesting)
   - Per-genre performance highlights

4. Discussion (0.5 pages):
   - FC vs CNN comparison
   - Impact of batch normalization
   - Impact of optimizer choice
   - Image-based vs Audio-based comparison
   - GAN augmentation effectiveness
   - Best performing model and why

5. Formatting:
   - Use CVPR LaTeX template
   - Include name and ECS user ID
   - Professional academic style
   - Proper citations for PyTorch, GTZAN dataset

Please write the 3-page implementation report in LaTeX format.
```

---

#### **Task 5.2: Report Part 2 - Deep Learning Topic Reflection (1 page)**
**Estimated Tokens**: ~8K context needed
**Complexity**: Low-Medium
**Dependencies**: None (can be done in parallel with Phase 4)
**Marks**: 4 out of 20 total

> ⚠️ **IMPORTANT**: The topic MUST come from the first 4 lab sessions of COMP6252. Do NOT pick a topic outside those labs (e.g. Transfer Learning was likely not covered — check your lab notes). Suggested safe choices: CNNs, RNNs/LSTMs, GANs, or Batch Normalisation/Optimisation.

**What to Provide to Claude:**
```
Project: Music Genre Classification - Topic Reflection

Task: Write 1-page reflection on a deep learning topic (CVPR format)

Context:
- Topic must be from the first 4 lab sessions of COMP6252
- Chosen topic: [INSERT YOUR CHOSEN TOPIC HERE]
- 1 page maximum in CVPR LaTeX format

The reflection MUST cover ALL four of the following required points 
exactly as specified in the assignment brief:

REQUIRED POINT 1 — Why the topic is important:
   - Explain the significance of this topic in deep learning
   - Why does it matter in real-world applications?

REQUIRED POINT 2 — Current deep learning technologies for this topic:
   - List and briefly describe the main current DL technologies/methods
     used for this topic (e.g. for GANs: DCGAN, WGAN, StyleGAN, etc.)
   - Reference key papers where relevant

REQUIRED POINT 3 — Implementation analysis (CRITICAL - do not skip):
   - Which of the technologies you listed above do you know how to implement?
     Be specific — name the ones you can implement and briefly say how.
   - Which ones can you NOT yet implement?
   - For those you cannot implement: point out the specific difficulties
     and technical challenges that prevent you from implementing them.
     (e.g. training instability, computational cost, lack of understanding
     of specific components, etc.)

REQUIRED POINT 4 — Impact and future vision:
   - Positive impacts of current DL technologies on this topic
   - Negative impacts or risks (ethical, societal, technical limitations)
   - Your personal vision for where this technology is heading in the future

Structure (1 page CVPR LaTeX):
   - Paragraph 1-2: Topic importance (Point 1)
   - Paragraph 3-4: Current technologies (Point 2)
   - Paragraph 5-6: What I can/cannot implement + specific difficulties (Point 3)
   - Paragraph 7-8: Positive and negative impacts + future vision (Point 4)

Requirements:
   - All 4 points must be addressed — missing any will lose marks
   - Academic but personal writing style (use "I" where appropriate)
   - Reference relevant papers/technologies
   - Draw on personal experience from this coursework where relevant
   - 1 page maximum in CVPR format

Please write the 1-page reflection on [CHOSEN TOPIC], ensuring all 
4 required points above are fully addressed.
```

---

#### **Task 5.3: Report Formatting & Final Review**
**Estimated Tokens**: ~5K context needed
**Complexity**: Low
**Dependencies**: Tasks 5.1 and 5.2 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Report Finalization

Task: Format and finalize the report

Context:
- Part 1 (3 pages) and Part 2 (1 page) written
- Need to compile and format in CVPR template

Requirements:
1. CVPR LaTeX formatting:
   - Download CVPR template if needed
   - Structure: Title, name, ECS ID, sections
   - Format figures and tables properly
   - Add captions and references

2. Content check:
   - Verify 4 pages max (3+1)
   - Check all figures are readable
   - Verify all tables are formatted correctly
   - Ensure consistent terminology

3. Proofreading:
   - Check grammar and spelling
   - Verify technical accuracy
   - Ensure logical flow
   - Check all citations

4. Generate PDF:
   - Compile LaTeX document
   - Verify PDF renders correctly
   - Check page limits
   - Name: report.pdf

Please format the report in CVPR template and generate final PDF.
```

---

### **PHASE 6: CODE ORGANIZATION & SUBMISSION**

#### **Task 6.1: Code Cleanup & Documentation**
**Estimated Tokens**: ~10K context needed
**Complexity**: Medium
**Dependencies**: All implementation tasks completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Code Organization

Task: Organize Jupyter notebook and add comprehensive documentation

Context:
- All 6 models implemented
- Need single clean Jupyter notebook for submission

Requirements:
1. Notebook structure:
   - Section 1: Introduction and Setup
   - Section 2: Data Loading and Preprocessing
   - Section 3: Model 1 - Fully Connected Network
   - Section 4: Model 2 - CNN (Base)
   - Section 5: Model 3 - CNN + Batch Norm
   - Section 6: Model 4 - CNN + Batch Norm + RMSProp
   - Section 7: Model 5 - LSTM
   - Section 8: Model 6 Part A - GAN Implementation
   - Section 9: Model 6 Part B - LSTM + GAN Data
   - Section 10: Results and Comparison
   - Section 11: Visualizations

2. Code cleanup:
   - Remove debug print statements
   - Remove commented-out code
   - Consistent naming conventions
   - Proper indentation

3. Documentation:
   - Add markdown cells explaining each section
   - Comment complex code blocks
   - Document hyperparameter choices
   - Include docstrings for custom classes/functions

4. Reproducibility:
   - Set random seeds (torch, numpy, random)
   - Document Python and library versions
   - Include requirements.txt

5. Make paths configurable:
   - Use variables for data directories
   - No hardcoded absolute paths
   - Easy to run on different machines

Please organize and document the notebook professionally.
```

---

#### **Task 6.2: Code Testing & Validation**
**Estimated Tokens**: ~8K context needed
**Complexity**: Medium
**Dependencies**: Task 6.1 completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Code Validation

Task: Test that notebook runs end-to-end without errors

Context:
- Cleaned and documented notebook ready
- Need to verify everything works

Requirements:
1. Environment verification:
   - Create fresh virtual environment
   - Install from requirements.txt
   - Verify all imports work

2. End-to-end test:
   - Run notebook from top to bottom
   - Use small subset of data for quick testing (if needed)
   - Verify no runtime errors
   - Check all outputs are generated

3. Output validation:
   - Verify plots are generated correctly
   - Check that metrics are calculated
   - Ensure model checkpoints are saved
   - Validate file paths work

4. Performance check:
   - Verify training loops run correctly
   - Check GPU utilization (if available)
   - Ensure memory doesn't overflow

5. Documentation check:
   - Verify markdown cells render correctly
   - Check that all sections are clear
   - Ensure code comments are helpful

Please test the notebook thoroughly and fix any issues found.
```

---

#### **Task 6.3: Final Submission Package**
**Estimated Tokens**: ~5K context needed
**Complexity**: Low
**Dependencies**: All previous tasks completed

**What to Provide to Claude:**
```
Project: Music Genre Classification - Final Submission

Task: Prepare submission package

Context:
- Report.pdf finalized (4 pages)
- Jupyter notebook tested and ready
- Ready to submit

Requirements:
1. Create code.zip:
   - Include main Jupyter notebook (.ipynb)
   - Include requirements.txt
   - Include README.md with:
     - Setup instructions
     - How to run the notebook
     - Expected outputs
     - System requirements
   - Do NOT include dataset (too large)
   - Do NOT include model checkpoints

2. Verify report.pdf:
   - 4 pages max (3 implementation + 1 reflection)
   - Name and ECS user ID included
   - All figures and tables properly formatted

3. Final checklist:
   - [ ] report.pdf (4 pages max)
   - [ ] code.zip contains notebook + requirements.txt + README.md
   - [ ] Notebook runs end-to-end
   - [ ] All requirements met

4. Submission:
   - Submit report.pdf to ECS Handin
   - Submit code.zip to ECS Handin
   - Verify submission successful
   - Note submission timestamp

Please create the final submission package and verify all requirements met.
```

---

## 🔧 TECHNICAL SPECIFICATIONS

### **Dataset Details**
- **Name**: GTZAN Genre Collection
- **Source**: Kaggle
- **Genres**: 10 (blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock)
- **Audio Files**: ~1000 WAV files (30 seconds each, 22050 Hz, mono)
- **Images**: MEL spectrograms in images_original folder
- **Image Resize**: 180x180 pixels (required by assignment)

### **Train/Val/Test Split**
- Training: 70%
- Validation: 20%
- Test: 10%
- Use stratified split for balanced genres

### **Model Specifications Summary**

| Model | Type | Input | Architecture | Optimizer | Epochs |
|-------|------|-------|--------------|-----------|---------|
| Net1 | FC | Image | 2 hidden layers | Adam | 50→100 |
| Net2 | CNN | Image | 4 conv + 2 fc | Adam | 50→100 |
| Net3 | CNN+BN | Image | Net2 + BatchNorm | Adam | 50→100 |
| Net4 | CNN+BN | Image | Net3 architecture | RMSprop | 50→100 |
| Net5 | LSTM | Audio | Multi-layer LSTM | Adam | Until convergence |
| Net6 | LSTM+GAN | Audio | Net5 + GAN data | Adam | Until convergence |

### **Key Hyperparameters to Track**
- Learning rate (default: 0.001)
- Batch size (recommended: 32-64)
- Number of epochs
- CNN: kernel sizes, channels, pool sizes
- LSTM: num layers, hidden size, bidirectional flag
- GAN: noise dimension, discriminator/generator architecture

---

## 💡 IMPLEMENTATION TIPS

### **For Working with Claude:**

1. **One Task at a Time**:
   - Copy one task from this planner
   - Paste to Claude with context
   - Complete before moving to next

2. **Provide Context**:
   - Always mention which phase and task number
   - Reference previous task outputs
   - Specify what files/data are available

3. **Save Checkpoints**:
   - Save model weights after training
   - Save metrics as CSV/JSON files
   - Save plots as PNG files
   - This allows resuming if interrupted

4. **Iterative Refinement**:
   - Start simple, then improve
   - Test with small data first
   - Scale up after verification

5. **Ask for Help**:
   - If stuck, ask Claude for alternative approaches
   - If results are poor, ask for debugging
   - If unclear, ask for clarification

### **Common Pitfalls to Avoid**

1. **Data Leakage**: Never use test data during training or validation
2. **Shape Mismatches**: Carefully check tensor dimensions
3. **Overfitting**: Monitor train/val gap, use regularization
4. **Unstable GAN**: Use techniques like label smoothing, gradient clipping
5. **Memory Issues**: Use appropriate batch sizes, clear GPU cache
6. **Unfair Comparisons**: Use same test set for all models

### **Debugging Strategies**

- Print tensor shapes frequently
- Start with small subset of data
- Visualize intermediate outputs
- Check loss values (should decrease)
- Verify gradients are flowing
- Monitor GPU memory usage

---

## 📝 ASSIGNMENT REQUIREMENTS CHECKLIST

### **Code Submission Requirements**
- [ ] Single Jupyter notebook with all 6 models
- [ ] Clear sections for Net1, Net2, Net3, Net4, Net5, Net6
- [ ] Code runs end-to-end without errors
- [ ] Comprehensive comments and documentation
- [ ] Submitted as code.zip to ECS Handin

### **Report Submission Requirements**
- [ ] 4 pages maximum (3 + 1)
- [ ] CVPR LaTeX template used
- [ ] Name and ECS user ID included
- [ ] Part 1: Implementation, results, discussion (3 pages)
- [ ] Part 2: Topic reflection (1 page)
- [ ] Professional figures and tables
- [ ] Submitted as report.pdf to ECS Handin

### **Model Implementation Requirements**
- [ ] Model 1: Fully connected (2 hidden layers), 50+100 epochs
- [ ] Model 2: CNN (Figure 1 architecture), 50+100 epochs
- [ ] Model 3: CNN + Batch Normalization, 50+100 epochs
- [ ] Model 4: CNN + Batch Norm + RMSprop, 50+100 epochs
- [ ] Model 5: LSTM, train until convergence
- [ ] Model 6: LSTM + GAN augmented data, train until convergence

### **Evaluation Requirements**
- [ ] All models evaluated on same test set (10% of data)
- [ ] Metrics: accuracy, precision, recall, F1-score
- [ ] Confusion matrices for all models
- [ ] Comparative analysis across models
- [ ] Genre-specific performance analysis

### **Technical Requirements**
- [ ] PyTorch framework used throughout
- [ ] Image resize: 180x180 pixels
- [ ] Proper train/val/test splits (70/20/10)
- [ ] Reproducible results (random seeds set)
- [ ] GAN generates equal number of samples as training data

---

## 🚀 GETTING STARTED

**Step 1**: Start with Phase 1, Task 1.1
**Step 2**: Work through tasks sequentially within each phase
**Step 3**: Save outputs after each task
**Step 4**: Review and verify before moving to next phase
**Step 5**: Complete report after all implementations done

---

## 📞 QUICK REFERENCE

**Key Files:**
- Main notebook: `music_genre_classification.ipynb`
- Report: `report.pdf` (LaTeX source: `report.tex`)
- Requirements: `requirements.txt`
- README: `README.md`

**Data Directory Structure:**
```
/data/GTZAN/
├── genres/
│   ├── blues/ (audio files)
│   ├── classical/
│   └── ... (10 genres)
└── images_original/ (MEL spectrograms)
```

**Models Directory:**
```
/models/
├── net1_checkpoint.pth
├── net2_checkpoint.pth
├── ... (6 models)
└── gan_generator.pth
```

**Results Directory:**
```
/results/
├── metrics/
│   ├── model1_metrics.csv
│   └── ... (all model metrics)
├── plots/
│   ├── training_curves.png
│   └── ... (all visualizations)
└── analysis/
    └── comparison_report.txt
```

---

## ⚠️ IMPORTANT NOTES

1. **Training Time**: Models 2-6 may take hours to train. Use GPU if available.
2. **GAN Training**: Most challenging task - may need multiple iterations.
3. **Data Size**: GTZAN is ~1.2GB - don't commit to git.
4. **Checkpointing**: Save model weights frequently to avoid re-training.
5. **Validation**: Use validation set to tune hyperparameters, NOT test set.
6. **Test Set**: Only use test set for FINAL evaluation of all models.

---

## 📚 ADDITIONAL RESOURCES

**PyTorch Documentation:**
- nn.Module, nn.Conv2d, nn.BatchNorm2d, nn.LSTM
- DataLoader, Dataset
- Optimizers: Adam, RMSprop (note: lowercase 'p' in PyTorch — torch.optim.RMSprop)

**Audio Processing:**
- librosa: audio loading and feature extraction
- torchaudio: PyTorch audio processing

**GTZAN Dataset:**
- Paper: "Musical genre classification of audio signals" (Tzanetakis & Cook, 2002)
- Kaggle: Search "GTZAN Genre Collection"

**GAN Resources:**
- Original GAN paper (Goodfellow et al., 2014)
- DCGAN for stable training
- WaveGAN for audio generation

---

## 🎓 SUCCESS CRITERIA

**Code Quality:**
- Clean, readable, well-commented code
- Modular and reusable functions
- Proper error handling
- Reproducible results

**Model Performance:**
- All 6 models implemented correctly
- Training converges properly
- Reasonable accuracy (>50% baseline for 10 classes)
- Clear performance comparisons

**Report Quality:**
- Clear and concise writing
- Professional figures and tables
- Insightful analysis and discussion
- Proper academic formatting

**Submission:**
- All deliverables on time
- Correct file formats
- Complete documentation
- Runs without errors

---

**Good luck with your project! Start with Phase 1, Task 1.1 when ready!**