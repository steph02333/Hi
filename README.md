# HBM4/HBM4E-Relevant TSV Parasitic Modelling — NUS FYP

**Machine-learning-assisted modelling and optimization of TSV parasitic capacitance in HBM4/HBM4E-relevant interconnects**  
**Current phase:** CA2 numerical baseline completed; DOE V2 planned  
**Repository:** steph02333/Hi (**public**) · **Documentation and selected numerical CSVs uploaded; full simulation archive migration incomplete.**

> **Scientific integrity:** Q3D is a high-fidelity reference solver, **not measured ground truth**. Geometry is an HBM-relevant research abstraction, not proprietary HBM4E hardware. Do not claim a full cross-solver/semiconductor validation.

## Research overview

The work studies grounded local TSV layouts **GSG, GSSG and GSGSG**, models self and signal–signal mutual capacitance using **Matérn-kernel Gaussian Process Regression (GPR)**, and verifies surrogate-selected optima through fresh **Ansys Q3D Extractor** solves.

**Q3D DOE inputs:** diameter 3–6 µm; pitch 10–20 µm (center-to-center; edge spacing = P−D); height 25–50 µm; SiO2 liner thickness 0.1–0.5 µm; bulk Si resistivity 5/10/100 Ω·cm. The dataset does not include the proposed 1 Ω·cm endpoint.

## Achievements and honest limitations

| Completed stage | Evidence / result |
|---|---|
| Accepted ML observations | **261** = 216 original DOE + 36 supplementary GSGSG development + 9 frozen GSGSG blind |
| Original 216-case grouped held-out GPR | Self-C MAPE: GSG **3.336%**, GSSG **4.087%**, GSGSG **2.566%** |
| Original 216-case mutual GPR | GSSG **5.625%**, GSGSG **2.058%** MAPE |
| Frozen blind GSGSG (9) | Self **1.104%**, mutual **0.707%** MAPE |
| Geometry optimization | Fresh Q3D verified all 3 layouts; GSGSG min-both self **14.2845 fF**, mutual **2.42925 fF** |
| Analytical validation | 9 coax estimates, average difference **3.61%** |
| Physics/numerical checks | 21 controlled geometry tests and 16 targeted mesh/domain studies |
| Partial external solver check | 12 **lossless** Q3D–Maxwell matched geometries: mean self discrepancy **3.69%** and mutual **2.19%** |

**Unresolved:** cross-solver SUB_REF/full-matrix discrepancy (SUB_REF diagonals 32–72%), rigorous closed-surface Gauss-law accounting, full continuum mesh/domain convergence, lossy Q3D independent comparison, voltage-dependent MOS TCAD, real-device measurements and vendor-specific geometry. The 12-case cross-check used **lossless Si in both tools**; it does not validate original finite-resistivity 1 GHz Q3D data.

## Navigating this project — handover-first

1. **[AGENTS.md](AGENTS.md)** — mandatory instructions for subsequent AI agents; read first.
2. **[Research history](docs/RESEARCH_HISTORY.md)** — curated technical decisions, troubleshooting and history from CA1 through Nov 2026.
3. **[Verified numerical baseline](docs/RESULTS_BASELINE.md)** — carefully qualified model, optimization and validation scores.
4. **[Validation limitations](docs/VALIDATION_LIMITATIONS.md)** — demonstrated results versus unresolved physical and software limitations.
5. **[DOE V2 proposal](docs/DOE_EXPANSION_V2.md)** — 90 **planned, not simulated** new cases (GSG 18, GSSG 54, GSGSG 18).
6. **[Reproducibility protocol](docs/REPRODUCIBILITY.md)** — versions, QA, split isolation and experiment procedure.
7. **[Iteration log](docs/ITERATION_LOG.md)** — append-only experiment ledger; required update with every substantive change.
8. **[Source inventory](docs/SOURCE_INVENTORY.md)** and **[migration status](docs/MIGRATION_STATUS.md)** — what exists historically vs what is actually uploaded.

### Numerical CSVs currently in GitHub

- [Original 216-stage grouped-test metrics](data/processed/216_grouped_test_metrics.csv)
- [12-case Q3D–Maxwell aggregate comparison](data/validation/maxwell_q3d_12_case_summary.csv)

**Do not assume raw matrices, 261 dataset, source scripts, Jupyter notebooks or the reference-audited PDF are already uploaded.** See [migration status](docs/MIGRATION_STATUS.md).

## DOE V2 next phase

Proposed **30 additional independent geometry groups × 3 resistivities = 90 new Q3D solves**, prioritizing GSSG signal-to-signal mutual prediction where original held-out MAPE was highest. Freeze matched test splits and nine blind cases before any new data acquisition. Compare before/after performance on the **same** untouched geometry groups. More data may improve surrogate accuracy relative to Q3D, not automatically improve physical model accuracy.

## Mandatory GitHub iteration policy

**Pull latest → read source/manifest and history → create experiment plan → generate/validate → commit scripts/data + update `docs/ITERATION_LOG.md` → verify output hashes and metrics → summarize remaining limitations.** Future agents must be able to reproduce what was done, including failures and rejected runs.

## Licensing, privacy and publication

This repo is currently **public**. No passwords, licensed JEDEC standard files, private supervisor correspondence, unpublished vendor data or large solver caches should be publicly committed. Keep original AEDT projects in checksum-tracked secure storage or appropriate Git LFS after capacity/license review.

**Last reviewed:** 2026-11-01.
