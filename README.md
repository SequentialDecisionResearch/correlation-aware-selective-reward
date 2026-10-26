# Correlation-Aware Selective Reward Acquisition for Group-Relative Policy Updates

This repository provides the manuscript, LaTeX source, experimental code, and archived results accompanying the paper:

**Correlation-Aware Selective Reward Acquisition for Group-Relative Policy Updates**

**Authors:** Shenggang Li, Bilian Song, Yunfeng Qi, and Joseph Li.

## Paper and Reproducibility Materials

The repository contains three downloadable files:

1. [CORR_GRPO.pdf](CORR_GRPO.pdf)  
   Complete research manuscript, including theoretical analysis and experimental results.

2. [CORR_GRPO_LaTeX.zip](CORR_GRPO_LaTeX.zip)  
   LaTeX source files required to compile the manuscript.

3. [GRPO_Phase1_to_6C_Reviewer_Reproducibility_v1.zip](GRPO_Phase1_to_6C_Reviewer_Reproducibility_v1.zip)  
   Experimental implementations, tests, archived numerical results, and reproducibility documentation covering Phases 1 through 6D.

The reproducibility archive retains its original filename but has been updated to include the complete Phase 6D experiment.

## Research Overview

The paper studies correlation-aware selection of reward observations for group-relative policy updates.

The analysis examines how dependence among candidate observations affects acquisition risk and how correlation-aware selection can be evaluated under controlled experimental conditions.

The experimental program includes theoretical checks, controlled comparisons, holdout evaluations, and frozen-checkpoint gradient diagnostics.

## Phase 6D: Gradient Alignment Diagnostics

Phase 6D evaluates whether reductions in acquisition risk under the original score-sketch geometry also hold when risk is measured using saved LoRA-gradient geometry.

The experiment contains 144 frozen-checkpoint group records:

- 3 random seeds
- 2 source acquisition policies
- 3 training checkpoints
- 2 task families
- 4 groups per configuration

Each group contains six candidates, with all 20 subsets of size three evaluated for the fixed-size acquisition-risk calculation.

For the 96 post-initial-checkpoint conditions:

- Pooled score-sketch risk reduction: 26.91%
- Pooled saved LoRA-gradient risk reduction: 3.27%
- The true-gradient risk effect is negative for one of the three seeds.

The original Phase 6C holdout evaluation found identical final accuracy for uniform and joint-EWMA acquisition.

These results indicate that improvements under a surrogate gradient geometry do not necessarily translate into comparable improvements under the saved LoRA-gradient geometry or into better downstream accuracy.

## Reproducing the Archived Results

Download and extract:

`GRPO_Phase1_to_6C_Reviewer_Reproducibility_v1.zip`

From the extracted archive directory, install the package and run:

```bash
python -m pip install -e ".[figures]"
python -m unittest discover -s tests -q
python scripts/reproduce_archived_results.py --verify-only
python scripts/reproduce_phase6d_archived.py
