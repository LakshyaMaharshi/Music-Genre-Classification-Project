# Net3 (CNN + BatchNorm) Final Tuning Note

## Final configuration that worked
- Model: Net3 (same conv/fc layout as Net2, with BatchNorm after each conv)
- Dropout: 0.1
- Optimizer: Adam
- Initial learning rate: 0.0003
- Scheduler: ReduceLROnPlateau with factor=0.5, patience=12, min_lr=1e-5
- Gradient clipping: clip_grad_norm_ with max_norm=5.0
- Loss: CrossEntropyLoss
- Epoch plan: train to 50 epochs, then continue to 100 epochs

## Why this setup worked
- Lower dropout (0.1) reduced underfitting pressure seen in earlier runs.
- Conservative LR (0.0003) avoided unstable early updates after adding BatchNorm.
- Scheduler lowered LR when validation loss plateaued, improving late-stage validation accuracy.
- Gradient clipping prevented occasional large updates and kept training stable.

## Final observed outcome (current split)
- Net2 test accuracy: 58.0%
- Net3 test accuracy: 71.0%
- Improvement: +13.0 percentage points over Net2

## Report-ready summary line
Batch normalization improved generalization only after optimizer and regularization retuning; with tuned LR, low dropout, LR scheduling, and gradient clipping, Net3 outperformed Net2 by a clear margin on the fixed test split.
