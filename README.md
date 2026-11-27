# auditory-ddm-modeling

## Overview
Fits drift-diffusion models (PyDDM) to choices and response times from an auditory decision task, where participants judge high vs low tone frequency at varying coherence. It compares "regular" and "irregular" blocks separately for each participant. The project is advised by Yale Cohen (University of Pennsylvania) in the Cohen Lab.

## Methods
- `ddm_pipeline.py`
  - Loads each participant's CSV files separately (no pooling). Excludes timeouts and RTs ≤ 0.1 s.
  - **Base model:** drift = v · signed coherence, constant noise, linearly collapsing bound, non-decision time, and a uniform-mixture lapse term.
  - **Bias model:** the base model plus a starting point expressed as a fraction of the bound.
  - Grid settings: dx = dt = 0.005, T_dur = 5 s. The stimulus has 10 bursts and lasts 1.04 s.
  - Fits every participant × condition × model and saves each fit immediately, so runs can resume.
  - Summaries:
    - choice accuracy with a binomial test against chance
    - regular vs irregular RT comparison (Mann–Whitney)
    - AIC, BIC, ΔAIC and ΔBIC vs the base model
    - flags for parameters pinned at their bounds
  - Fit-quality checks compare predicted and observed choice proportions and RT quantiles.
  - Report figures: RT distributions and quantiles, plus psychometric and chronometric curves with DDM fits overlaid.

Results: TODO: confirm. The code computes fit statistics at run time but stores no results.

## Tools
Python, PyDDM, NumPy, pandas, SciPy, Matplotlib, Google Colab.

## Status
In progress.

**Data:** not included. This is human-participant behavioral data. Participants are labeled P1, P2, …; folder names and fit-file prefixes use the same labels.

**Paths:** the Google Drive path was replaced with the placeholder `/path/to/auditory_project/`.

**Notes:** The `.py` files are exports of Google Colab notebooks. Lines starting with `!` (and the bare `pip install` line, where present) are notebook shell commands, and `drive.mount(...)` calls are Colab-only. Run the files cell by cell in a notebook, not as plain scripts. Additional exploratory analysis code: TODO: confirm before adding.
