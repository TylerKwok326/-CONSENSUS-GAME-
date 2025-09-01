# CONSENSUS-GAME

## Overview
This code tests Phi-2 and Qwen2 on 50 calibration questions from the ARC dataset and evaluates four aspects of model performance:
- Accuracy – how often predictions are correct.
- Confidence – average probability assigned to chosen answers.
- Consistency – predictability of answer patterns, measured by entropy.
- Robustness – confidence restricted to correct answers.
These metrics combine into a single base strength score used to weight each model during adversarial training. Calibration questions are removed from testing to prevent data leakage.
## Workflow
Preprocessing: Filter out low-confidence answers (<10%), shuffle remaining choices to avoid position bias.
Adversarial Game:
Generator (Phi-2) proposes answers.
Discriminator (Qwen2) evaluates correctness.
Both update strategies iteratively using weighted softmax and Q-learning.
Temperature Scheduling: Adjusts exploration vs. exploitation depending on strategy stability.
Stopping Criteria: Consensus reached when (a) both models >80% confidence in top choice, (b) max 5 iterations, or (c) strategy change <0.001.
### Results
- Baseline: Generator ~73.4%, Discriminator ~60.9%.
After weighted equilibrium search:
- Generator: 75.0% (+1.6%)
- Discriminator: 68.0% (+7.1%)
- Overall accuracy: 73.6%
