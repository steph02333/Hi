# HBM4/HBM4E TSV FYP — AI Agent Handover Protocol

**MANDATORY READ ORDER:** [README](README.md) → [Research history](docs/RESEARCH_HISTORY.md) → [Baseline](docs/RESULTS_BASELINE.md) → [Limitations](docs/VALIDATION_LIMITATIONS.md) → [Source inventory](docs/SOURCE_INVENTORY.md) → [Iteration log](docs/ITERATION_LOG.md) → [DOE V2](docs/DOE_EXPANSION_V2.md).

## Research integrity rules

1. Q3D is a **high-fidelity reference solver**, NOT experimentally established ground truth. Historical statistics are prediction-to-Q3D.
2. Original 261-case dataset = **216 original + 45 supplementary GSGSG**; **9 of the supplementary records are frozen blind**. Never use these nine in training, model selection, active-learning acquisition or tuning.
3. Original Q3D finite-resistivity silicon: **5, 10, 100 Ω·cm**. The 12 Q3D–Maxwell cross-checks instead used **lossless** silicon in BOTH solvers (epsilon_r 11.9, sigma=0). They do not validate lossy 1 GHz conductance or MOS C–V.
4. Signal self and signal mutual comparisons in the 12-case cross-check agree on average 3.69% and 2.19%; **SUB_REF and full matrices differ significantly**. Do not assert full-matrix validation or claim a proven root cause.
5. **Global Gauss-law surface-flux balance remains unverified**. Solver convergence, C/G symmetry and passivity are not independent physical calibration.
6. Geometry: D 3–6 µm, P 10–20 µm, H 25–50 µm, tox 0.1–0.5 µm. Pitch is centre-centre, clearance is P-D.
7. GSG has only one signal: signal–signal mutual is undefined. GSSG and GSGSG have two signals; preserve explicit terminal name mapping, sign convention, units and matrix grounding/reduction state.
8. Never invent runs, commits, notebooks, data points, physics explanations or solver versions. Cite the original file when possible. Missing supplemental G fields are **missing, not zero**.
9. The **proposed 90-case DOE V2 is NOT run yet**. Do not call 351 an achieved count. Software licensing, adaptive mesh and domain errors must be noted.
10. This repository currently is **PUBLIC**. Do not commit correspondence, protected JEDEC standards, user-identifying PDFs, credentials, restricted data or large AEDT caches. Preserve binary source archives off-repo with provenance/hashes.

## GitHub-first workflow

Before working: fetch the repository HEAD and examine the latest README, log and manifest. Always start from latest GitHub state rather than chat attachment names.

For *every* meaningful iteration: update **docs/ITERATION_LOG.md in the same code/data change**. Preserve a stable baseline and append new records; never rewrite historical outcomes. Where possible, use feature branch → PR → verification → merge.

### Required iteration record
```markdown
### YYYY-MM-DD — EXP-YYYYMMDD-NNN
**Objective / hypothesis:**
**Git commit and immutable input data hashes:**
**Case IDs / layout / D, P, H, tox, rho / solver version:**
**Changes, scripts, setup, environment and seed:**
**Outputs, original matrix files and SHA-256:**
**QA checks and comparable holdout metrics:**
**What failed / potential confounders / software limitations:**
**Scientific conclusion (demonstrated vs hypothesized):**
**Next reproducible action:**
```

## Known failure/recovery history

The first Maxwell pilot solved but matrix exports failed. Later a fresh *single-script* 12-pair campaign succeeded with **24 raw matrices**; don't conflate failed export with solver physics. A Q3D–Maxwell reference audit showed nontrivial row-sum convention and side copper SUB_REF contact; root cause still open.

At session end, always report exact paths, changed Git commits, what is **not** committed or verified, and the next action that another agent can execute.
