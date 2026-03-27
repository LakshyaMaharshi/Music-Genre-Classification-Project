# 📚 Documentation Overview - Music Genre Classification Project

Welcome to your comprehensive project planner for the Deep Learning Music Genre Classification coursework!

---

## 📖 DOCUMENT GUIDE

I've created **4 reference documents** to help you complete this assignment efficiently with Claude Opus/Sonnet:

### **1. PROJECT_REFERENCE.md** ⭐ MAIN DOCUMENT
**Purpose**: Complete task planner with detailed prompts
**Use When**: Starting each new task
**Contains**:
- 19 sequential tasks across 6 phases
- Exact prompts to copy-paste to Claude
- Technical requirements for each task
- Expected context window sizes
- Task dependencies and prerequisites

**How to Use**:
1. Find your current task (e.g., "Task 2.1")
2. Read the task description
3. Copy the "What to Provide to Claude" section
4. Paste it to Claude Opus/Sonnet
5. Let Claude implement it
6. Move to next task

### **2. QUICK_START.md** 🚀 START HERE
**Purpose**: Quick reference and getting started guide
**Use When**: Beginning the project or need quick overview
**Contains**:
- High-level task list with time estimates
- Current task pointer
- Productivity tips and workflow suggestions
- Troubleshooting guide
- Session planning recommendations
- Milestone tracking

**How to Use**:
- Read this FIRST to understand the workflow
- Use the quick task reference to navigate
- Follow the suggested timeline
- Track milestones as you progress

### **3. TASK_TRACKER.md** ✅ PROGRESS TRACKING
**Purpose**: Track your progress through all tasks
**Use When**: After completing each task, daily reviews
**Contains**:
- Task completion checkboxes
- Model performance table (fill as you train)
- Progress bars for each phase
- Session logs
- Important reminders

**How to Use**:
- Update after completing each task
- Fill in model accuracy as you train
- Use as your project dashboard
- Track dates and time spent
- Log any issues encountered

### **4. TECHNICAL_SPECS.md** 🔧 QUICK REFERENCE
**Purpose**: Technical specifications and requirements
**Use When**: Need quick lookup of technical details
**Contains**:
- Model architecture specifications
- Hyperparameter recommendations
- Dataset specifications
- Code templates and snippets
- Evaluation metrics definitions
- Testing procedures

**How to Use**:
- Reference while implementing
- Copy code templates
- Verify technical requirements
- Look up hyperparameters
- Check expected performance ranges

---

## 🗺️ RECOMMENDED WORKFLOW

### **Getting Started (Day 1)**

**Step 1**: Read the Documents in Order
1. ✅ Read **QUICK_START.md** (10 min) - Get overview
2. ✅ Read **PROJECT_REFERENCE.md** - Phase 1 section (15 min) - Understand first tasks
3. ✅ Open **TASK_TRACKER.md** (5 min) - Prepare to track progress
4. ✅ Bookmark **TECHNICAL_SPECS.md** - Keep for reference

**Step 2**: Environment Setup (30 min)
1. Open **PROJECT_REFERENCE.md**
2. Go to "Phase 1, Task 1.1"
3. Copy the prompt under "What to Provide to Claude"
4. Paste to Claude Opus and let it implement
5. Verify setup works
6. Mark Task 1.1 as complete in **TASK_TRACKER.md**

**Step 3**: Continue Sequential Tasks
1. Move to Task 1.2
2. Repeat the process
3. Complete all of Phase 1

### **During Implementation (Days 2-10)**

**Daily Routine**:
1. Open **TASK_TRACKER.md** - Check current task
2. Open **PROJECT_REFERENCE.md** - Read task details
3. Copy prompt to Claude - Let it implement
4. Verify implementation - Test the code
5. Update **TASK_TRACKER.md** - Mark complete, log results
6. Save checkpoints - Models, metrics, plots
7. Move to next task - Stay sequential

**Reference as Needed**:
- Check **TECHNICAL_SPECS.md** for architecture details
- Check **QUICK_START.md** for troubleshooting tips

### **During Report Writing (Days 11-12)**

1. Complete Phase 4 (Analysis) first
2. Use Phase 5 tasks in **PROJECT_REFERENCE.md**
3. Reference **TECHNICAL_SPECS.md** for specifications
4. Check **TASK_TRACKER.md** for your performance results

### **Final Submission (Day 13)**

1. Follow Phase 6 tasks in **PROJECT_REFERENCE.md**
2. Use submission checklist in **TASK_TRACKER.md**
3. Double-check requirements in **TECHNICAL_SPECS.md**

---

## 💡 KEY PRINCIPLES

### **1. Sequential Execution**
- Complete tasks in order (1.1 → 1.2 → 1.3 → 2.1 → ...)
- Don't skip ahead (later tasks depend on earlier ones)
- Finish phases before moving to next

### **2. One Task Per Claude Session**
- Each task is sized for Claude's context window
- Focus on one thing at a time
- Complete before moving on

### **3. Save Everything**
- Model checkpoints after training
- Metrics and logs
- Plots and visualizations
- Notebook progress

### **4. Track Progress**
- Update TASK_TRACKER.md regularly
- Log issues and solutions
- Record model performance
- Track time spent

### **5. Test Early and Often**
- Test data loading before training
- Test model forward pass before full training
- Test on subset first, then scale up
- Validate outputs at each step

---

## 🎯 TASK DEPENDENCIES MAP

```
Phase 1 (Foundation)
    ├─ 1.1 (Setup)
    ├─ 1.2 (Exploration) ← depends on 1.1
    └─ 1.3 (DataLoader) ← depends on 1.2

Phase 2 (Image Models) ← depends on Phase 1
    ├─ 2.1 (Net1) ← parallel start
    ├─ 2.2 (Net2) ← parallel start OR after 2.1
    ├─ 2.3 (Net3) ← after 2.2
    └─ 2.4 (Net4) ← after 2.3

Phase 3 (Audio Models) ← depends on Phase 1
    ├─ 3.1 (Audio Prep)
    ├─ 3.2 (Net5) ← depends on 3.1
    ├─ 3.3 (GAN) ← depends on 3.1
    └─ 3.4 (Net6) ← depends on 3.2 AND 3.3

Phase 4 (Analysis) ← depends on Phase 2 AND Phase 3
    ├─ 4.1 (Metrics)
    ├─ 4.2 (Visualization) ← depends on 4.1
    └─ 4.3 (Interpretation) ← depends on 4.2

Phase 5 (Report) ← depends on Phase 4
    ├─ 5.1 (Main Report)
    ├─ 5.2 (Reflection) ← CAN DO IN PARALLEL
    └─ 5.3 (Formatting) ← depends on 5.1 AND 5.2

Phase 6 (Submission) ← depends on ALL phases
    ├─ 6.1 (Cleanup)
    ├─ 6.2 (Testing) ← depends on 6.1
    └─ 6.3 (Package) ← depends on 6.2
```

---

## 🎬 EXAMPLE: YOUR FIRST INTERACTION WITH CLAUDE

### **Scenario**: You're ready to start the project

**Step 1**: Open PROJECT_REFERENCE.md and find Task 1.1

**Step 2**: Copy this to Claude Opus/Sonnet:

```
I'm working on Music Genre Classification using GTZAN dataset for my Deep Learning coursework.

CURRENT TASK: Phase 1, Task 1.1 - Environment Setup & Dataset Download

Please help me:
1. Create project directory structure:
   - /data (for dataset)
   - /models (for checkpoints)
   - /results (for outputs)
   - /notebooks (for .ipynb)

2. Create requirements.txt with:
   - torch, torchvision, torchaudio
   - numpy, pandas, matplotlib, seaborn
   - librosa, scikit-learn
   - jupyter, kaggle

3. Guide me to download GTZAN dataset from Kaggle:
   - I need the GTZAN Genre Collection
   - Should have 10 genre folders
   - Should have images_original folder with MEL spectrograms

4. Verify the dataset structure once downloaded

Please implement step by step.
```

**Step 3**: Claude will implement it

**Step 4**: Verify everything works

**Step 5**: Update TASK_TRACKER.md - mark Task 1.1 as ✅ completed

**Step 6**: Move to Task 1.2 and repeat!

---

## 🔄 ITERATION STRATEGY

### **If a Task Fails or Results are Poor**

1. **Don't Panic** - This is expected in ML projects
2. **Debug with Claude**:
   ```
   Previous task didn't work as expected. Here's the issue:
   [describe the problem]

   Error/Poor Results:
   [paste error or metrics]

   Can you help debug and fix this?
   ```
3. **Iterate** - Refine and re-run
4. **Update Tracker** - Log what went wrong and how you fixed it
5. **Continue** - Move on once resolved

### **If You Need to Modify an Approach**

Claude can help you:
- Adjust hyperparameters
- Try different architectures
- Debug training issues
- Improve performance
- Understand results

Just provide context about what you've tried and what's not working.

---

## 📊 PROGRESS MILESTONES & CHECKPOINTS

### **Checkpoint 1: Foundation Ready** (Day 1-2)
**Phase 1 Complete**
- [ ] Environment set up
- [ ] Dataset downloaded and verified
- [ ] DataLoaders working
- [ ] Can load and visualize sample data

→ **Proceed to Phase 2**

### **Checkpoint 2: First Model Trained** (Day 2-3)
**Task 2.1 Complete**
- [ ] Net1 (FC network) implemented
- [ ] Trained for 50 and 100 epochs
- [ ] Metrics saved
- [ ] Baseline accuracy established

→ **Continue with remaining CNN models**

### **Checkpoint 3: All Image Models Done** (Day 5-6)
**Phase 2 Complete**
- [ ] All 4 models (Net1-4) trained
- [ ] All checkpoints saved
- [ ] Performance comparison available
- [ ] Best CNN identified

→ **Proceed to Phase 3 (Audio models)**

### **Checkpoint 4: Audio Pipeline Ready** (Day 6-7)
**Task 3.1-3.2 Complete**
- [ ] Audio preprocessing working
- [ ] Net5 (LSTM) trained
- [ ] Audio-based approach validated

→ **Proceed to GAN (most complex task)**

### **Checkpoint 5: GAN Working** (Day 8-9)
**Task 3.3 Complete**
- [ ] GAN implemented
- [ ] Synthetic data generated
- [ ] Quality validated

→ **Train Net6 with augmented data**

### **Checkpoint 6: All Models Complete** (Day 9-10)
**Phase 2 & 3 Complete**
- [ ] All 6 models trained
- [ ] All checkpoints saved
- [ ] Ready for comprehensive evaluation

→ **Proceed to Phase 4 (Analysis)**

### **Checkpoint 7: Analysis Done** (Day 10-11)
**Phase 4 Complete**
- [ ] All metrics calculated
- [ ] All visualizations created
- [ ] Insights extracted

→ **Proceed to Phase 5 (Report)**

### **Checkpoint 8: Report Draft Ready** (Day 12)
**Phase 5 Complete**
- [ ] Implementation section written
- [ ] Reflection section written
- [ ] Report formatted in CVPR template

→ **Proceed to Phase 6 (Final prep)**

### **Checkpoint 9: Submission Ready** (Day 13)
**Phase 6 Complete**
- [ ] Code cleaned and documented
- [ ] Everything tested
- [ ] code.zip created
- [ ] report.pdf finalized

→ **SUBMIT TO ECS HANDIN!**

---

## 🎓 ACADEMIC INTEGRITY REMINDER

### **Allowed:**
✅ Using PyTorch tutorials and documentation
✅ Referencing Stack Overflow for specific technical issues
✅ Using Claude to help implement code
✅ Discussing general approaches with classmates
✅ Reading research papers for background

### **Not Allowed:**
❌ Copying code from classmates
❌ Sharing your implementation with others
❌ Using pre-trained models without disclosure
❌ Plagiarizing report content
❌ Submitting someone else's work

### **Using AI Assistants (like Claude)**
- ✅ You CAN use Claude to help implement and debug
- ✅ You should understand all code Claude generates
- ✅ Be able to explain your implementation
- ❌ Don't just copy-paste without understanding

---

## 🗂️ DOCUMENT SUMMARY

| Document | Purpose | When to Use | Size |
|----------|---------|-------------|------|
| **QUICK_START.md** | Getting started guide | First read, overview | 3 min read |
| **PROJECT_REFERENCE.md** | Detailed task planner | During implementation | 15 min read |
| **TASK_TRACKER.md** | Progress tracking | Daily updates | 2 min update |
| **TECHNICAL_SPECS.md** | Technical reference | During coding | Quick lookup |
| **README.md** (you create) | Setup instructions | For submission | - |

---

## 🚀 YOUR IMMEDIATE NEXT STEPS

### **Right Now (Next 30 minutes)**:

1. **Read QUICK_START.md** (5 min)
   - Understand the overall workflow
   - See the task overview

2. **Skim PROJECT_REFERENCE.md** (10 min)
   - Focus on Phase 1 section
   - Understand task structure

3. **Open TASK_TRACKER.md** (2 min)
   - Familiarize yourself with tracking system

4. **Start Task 1.1** (15 min)
   - Go to PROJECT_REFERENCE.md → Task 1.1
   - Copy prompt to Claude
   - Begin setup!

### **This Week**:
- Complete Phase 1 (Setup & Data)
- Complete Phase 2 (Image Models 1-4)
- Start Phase 3 (Audio Models)

### **Next Week**:
- Complete Phase 3 (Audio + GAN)
- Complete Phase 4 (Analysis)
- Complete Phase 5 (Report)
- Complete Phase 6 (Submit!)

---

## 💪 YOU'VE GOT THIS!

This project is well-structured and manageable when broken down into these tasks. Each task is:
- ✅ **Scoped appropriately** for Claude's context window
- ✅ **Self-contained** with clear inputs/outputs
- ✅ **Sequential** with proper dependencies
- ✅ **Tested** for feasibility

By following this planner systematically, you'll:
- 🎯 Complete all 6 required models
- 📊 Generate comprehensive analysis
- 📝 Write an excellent report
- ✅ Submit on time with confidence

---

## 🆘 NEED HELP?

### **During Implementation**:
- Stuck on a task? → Ask Claude for debugging help
- Don't understand something? → Ask Claude to explain
- Results not good? → Ask Claude for improvements
- Code errors? → Provide full error trace to Claude

### **Using This Planner**:
- Confused about workflow? → Re-read QUICK_START.md
- Need task details? → Check PROJECT_REFERENCE.md
- Need specifications? → Check TECHNICAL_SPECS.md
- Need to track progress? → Update TASK_TRACKER.md

### **For Course-Specific Questions**:
- Check assignment PDF again (DLT COURSEWORK 1.pdf)
- Review lecture materials
- Check Blackboard/course resources
- Email instructor if requirements unclear

---

## 📞 QUICK REFERENCE COMMANDS

### **Open Documents**:
```bash
# Read documents in your editor
code PROJECT_REFERENCE.md
code QUICK_START.md
code TASK_TRACKER.md
code TECHNICAL_SPECS.md
```

### **Navigate to Current Task**:
```bash
# Search for your current task in PROJECT_REFERENCE.md
grep -n "Task 1.1" PROJECT_REFERENCE.md
```

### **Track Progress**:
```bash
# Count completed tasks
grep -c "✅" TASK_TRACKER.md
```

---

## 🎯 FINAL CHECKLIST

Before you start coding:
- [ ] Read QUICK_START.md
- [ ] Review PROJECT_REFERENCE.md (at least Phase 1)
- [ ] Open TASK_TRACKER.md in editor
- [ ] Bookmark TECHNICAL_SPECS.md
- [ ] Have Jupyter ready
- [ ] Have Claude Opus/Sonnet access ready

Ready to start?
- [ ] Go to PROJECT_REFERENCE.md
- [ ] Find "Task 1.1: Environment Setup & Dataset Download"
- [ ] Copy the prompt to Claude
- [ ] Begin your journey! 🚀

---

## 📈 EXPECTED OUTCOMES

**By Following This Planner, You Will:**
- ✅ Complete all 6 model implementations
- ✅ Have comprehensive evaluation and analysis
- ✅ Write a high-quality report
- ✅ Submit clean, documented code
- ✅ Understand deep learning concepts deeply
- ✅ Achieve excellent coursework grade!

---

**Good luck! Start with QUICK_START.md and then dive into Phase 1, Task 1.1!** 🎉

---

## 📝 NOTES

- These documents are designed to work together
- Update TASK_TRACKER.md as you progress
- Use PROJECT_REFERENCE.md as your main guide
- Reference TECHNICAL_SPECS.md when coding
- QUICK_START.md is your overview map

**Remember**: You're not alone - Claude Opus/Sonnet will help you implement each task!

---

**Created**: 2026-03-25
**For**: Deep Learning Technologies (ELEC6215) Coursework 1
**Project**: Music Genre Classification using GTZAN Dataset
