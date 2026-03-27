# Task Progress Tracker

**Project**: Music Genre Classification using GTZAN
**Last Updated**: 2026-03-25
**Current Status**: Not Started

---

## 📊 OVERALL PROGRESS

**Phases Completed**: 0/6
**Tasks Completed**: 0/19
**Overall Progress**: ░░░░░░░░░░ 0%

---

## ✅ PHASE 1: PROJECT SETUP & DATA PREPARATION

**Status**: ⬜ Not Started | ⏳ In Progress | ✅ Completed

| Task | Description | Status | Date | Notes |
|------|-------------|--------|------|-------|
| 1.1 | Environment Setup & Dataset Download | ⬜ | - | - |
| 1.2 | Data Exploration & Preprocessing | ⬜ | - | - |
| 1.3 | Base DataLoader Implementation | ⬜ | - | - |

**Phase 1 Progress**: ░░░░░░░░░░ 0% (0/3)

---

## ✅ PHASE 2: IMAGE-BASED MODELS (Models 1-4)

**Status**: ⬜ Not Started

| Task | Model | Description | Status | Accuracy | Date | Notes |
|------|-------|-------------|--------|----------|------|-------|
| 2.1 | Net1 | Fully Connected Network | ⬜ | - | - | - |
| 2.2 | Net2 | CNN (Base) | ⬜ | - | - | - |
| 2.3 | Net3 | CNN + Batch Norm | ⬜ | - | - | - |
| 2.4 | Net4 | CNN + BatchNorm + RMSProp | ⬜ | - | - | - |

**Phase 2 Progress**: ░░░░░░░░░░ 0% (0/4)

---

## ✅ PHASE 3: AUDIO-BASED MODELS (Models 5-6)

**Status**: ⬜ Not Started

| Task | Model | Description | Status | Accuracy | Date | Notes |
|------|-------|-------------|--------|----------|------|-------|
| 3.1 | - | Audio Preprocessing | ⬜ | - | - | - |
| 3.2 | Net5 | LSTM (Base) | ⬜ | - | - | - |
| 3.3 | GAN | GAN for Data Augmentation | ⬜ | - | - | - |
| 3.4 | Net6 | LSTM + GAN Data | ⬜ | - | - | - |

**Phase 3 Progress**: ░░░░░░░░░░ 0% (0/4)

---

## ✅ PHASE 4: EVALUATION & ANALYSIS

**Status**: ⬜ Not Started

| Task | Description | Status | Date | Notes |
|------|-------------|--------|------|-------|
| 4.1 | Performance Metrics Collection | ⬜ | - | - |
| 4.2 | Visualization & Results | ⬜ | - | - |
| 4.3 | Results Interpretation | ⬜ | - | - |

**Phase 4 Progress**: ░░░░░░░░░░ 0% (0/3)

---

## ✅ PHASE 5: REPORT WRITING

**Status**: ⬜ Not Started

| Task | Description | Status | Date | Notes |
|------|-------------|--------|------|-------|
| 5.1 | Implementation & Results (3 pages) | ⬜ | - | - |
| 5.2 | Topic Reflection (1 page) | ⬜ | - | - |
| 5.3 | Formatting & Final Review | ⬜ | - | - |

**Phase 5 Progress**: ░░░░░░░░░░ 0% (0/3)

---

## ✅ PHASE 6: CODE ORGANIZATION & SUBMISSION

**Status**: ⬜ Not Started

| Task | Description | Status | Date | Notes |
|------|-------------|--------|------|-------|
| 6.1 | Code Cleanup & Documentation | ⬜ | - | - |
| 6.2 | Code Testing & Validation | ⬜ | - | - |
| 6.3 | Final Submission Package | ⬜ | - | - |

**Phase 6 Progress**: ░░░░░░░░░░ 0% (0/3)

---

## 📈 MODEL PERFORMANCE SUMMARY

**Update this table as you complete each model:**

| Model | Type | Optimizer | Test Accuracy | Precision | Recall | F1-Score | Training Time | Notes |
|-------|------|-----------|---------------|-----------|--------|----------|---------------|-------|
| Net1 | FC | Adam | - | - | - | - | - | Baseline |
| Net2 | CNN | Adam | - | - | - | - | - | Base CNN |
| Net3 | CNN+BN | Adam | - | - | - | - | - | With BatchNorm |
| Net4 | CNN+BN | RMSProp | - | - | - | - | - | Different optimizer |
| Net5 | LSTM | Adam | - | - | - | - | - | Audio-based |
| Net6 | LSTM+GAN | Adam | - | - | - | - | - | With augmentation |

**Best Performing Model**: TBD

---

## 🎯 CURRENT TASK

**Phase**: 1
**Task**: 1.1 - Environment Setup & Dataset Download

**Next Action**:
Go to PROJECT_REFERENCE.md → Phase 1 → Task 1.1 → Copy prompt to Claude Opus/Sonnet

---

## 📝 SESSION LOG

### Session 1: YYYY-MM-DD
- [ ] Task X.X started
- [ ] Issues encountered: [describe]
- [ ] Solutions applied: [describe]
- [ ] Task X.X completed
- [ ] Next task: X.X

### Session 2: YYYY-MM-DD
- [ ] Task X.X started
- [ ] ...

---

## 🔔 IMPORTANT REMINDERS

### Before Each Session:
- [ ] Check which task you're on in this tracker
- [ ] Read the task details in PROJECT_REFERENCE.md
- [ ] Have previous task outputs available
- [ ] Open Jupyter notebook

### After Each Task:
- [ ] Update this tracker (mark task as completed)
- [ ] Save model checkpoints
- [ ] Save metrics/plots
- [ ] Commit notebook progress
- [ ] Update model performance table

### Critical Reminders:
- ⚠️ Use same test set for ALL models (don't recreate it)
- ⚠️ Set random seeds for reproducibility
- ⚠️ Images must be 180x180 (assignment requirement)
- ⚠️ Save everything - training takes time!
- ⚠️ GAN is complex - allocate extra time

---

## 🛠️ TROUBLESHOOTING GUIDE

### Common Issues & Solutions

**Issue**: CUDA out of memory
**Solution**: Reduce batch size, clear GPU cache with `torch.cuda.empty_cache()`

**Issue**: Model not converging (loss not decreasing)
**Solution**: Check learning rate, verify data loading, check loss function

**Issue**: Very low accuracy (<20%)
**Solution**: Check data preprocessing, verify labels are correct, check model architecture

**Issue**: Overfitting (train acc high, val acc low)
**Solution**: Add dropout, reduce model complexity, increase data augmentation

**Issue**: GAN mode collapse
**Solution**: Adjust learning rates, use label smoothing, add noise to discriminator

**Issue**: Dataset download fails
**Solution**: Use Kaggle API, ensure kaggle.json is configured, check internet connection

---

## 💾 FILES & CHECKPOINTS

### Files to Track:

**Code:**
- [ ] music_genre_classification.ipynb (main notebook)
- [ ] requirements.txt
- [ ] README.md

**Models:** (save after training)
- [ ] net1_checkpoint.pth
- [ ] net2_checkpoint.pth
- [ ] net3_checkpoint.pth
- [ ] net4_checkpoint.pth
- [ ] net5_checkpoint.pth
- [ ] gan_generator.pth
- [ ] gan_discriminator.pth
- [ ] net6_checkpoint.pth

**Results:**
- [ ] model1_metrics.csv
- [ ] model2_metrics.csv
- [ ] model3_metrics.csv
- [ ] model4_metrics.csv
- [ ] model5_metrics.csv
- [ ] model6_metrics.csv
- [ ] training_curves.png
- [ ] confusion_matrices.png
- [ ] comparison_table.csv

**Report:**
- [ ] report.tex (LaTeX source)
- [ ] report.pdf (final submission)

---

## 🎓 SUBMISSION CHECKLIST

### Before Final Submission:

**Code Submission (code.zip):**
- [ ] Jupyter notebook included
- [ ] requirements.txt included
- [ ] README.md with setup instructions
- [ ] Code runs end-to-end
- [ ] All 6 models implemented
- [ ] No hardcoded absolute paths
- [ ] Comprehensive comments
- [ ] File size reasonable (<50MB without dataset)

**Report Submission (report.pdf):**
- [ ] 4 pages maximum (3 implementation + 1 reflection)
- [ ] CVPR LaTeX template used
- [ ] Name and ECS user ID included
- [ ] All figures properly captioned
- [ ] All tables properly formatted
- [ ] References included
- [ ] Proofread for typos
- [ ] PDF renders correctly

**ECS Handin:**
- [ ] report.pdf uploaded
- [ ] code.zip uploaded
- [ ] Submission confirmed
- [ ] Before deadline
- [ ] Submission receipt saved

---

## 📅 TIMELINE SUGGESTION

| Days | Phase | Tasks | Focus |
|------|-------|-------|-------|
| 1 | Phase 1 | 1.1-1.3 | Setup & Data |
| 2-5 | Phase 2 | 2.1-2.4 | Image Models (4 CNNs) |
| 6-9 | Phase 3 | 3.1-3.4 | Audio Models + GAN |
| 10 | Phase 4 | 4.1-4.3 | Evaluation |
| 11-12 | Phase 5 | 5.1-5.3 | Report Writing |
| 13 | Phase 6 | 6.1-6.3 | Final Submission |

**Total**: ~2 weeks (adjust based on your schedule)

**Buffer**: Add 2-3 extra days for unexpected issues (especially GAN training!)

---

## 🎯 MILESTONES

- [ ] **Milestone 1**: Data pipeline working (Phase 1 complete)
- [ ] **Milestone 2**: First model trained (Task 2.1 complete)
- [ ] **Milestone 3**: All CNN models trained (Phase 2 complete)
- [ ] **Milestone 4**: Audio pipeline working (Task 3.1 complete)
- [ ] **Milestone 5**: LSTM model trained (Task 3.2 complete)
- [ ] **Milestone 6**: GAN working (Task 3.3 complete)
- [ ] **Milestone 7**: All 6 models completed (Phase 3 complete)
- [ ] **Milestone 8**: Analysis complete (Phase 4 complete)
- [ ] **Milestone 9**: Report draft done (Tasks 5.1-5.2 complete)
- [ ] **Milestone 10**: Submission ready (Phase 6 complete)

---

## 💡 PRODUCTIVITY TIPS

1. **Start Early**: GAN training is unpredictable
2. **Save Frequently**: Training takes hours - don't lose progress
3. **Use GPU**: If available, enables much faster training
4. **Batch Process**: Train multiple models overnight
5. **Document As You Go**: Don't wait until end to write report
6. **Ask Questions**: Use Claude to explain concepts you don't understand
7. **Review Literature**: Read GTZAN paper and CNN/LSTM papers

---

**🚀 READY TO START? Open PROJECT_REFERENCE.md and begin with Task 1.1!**
