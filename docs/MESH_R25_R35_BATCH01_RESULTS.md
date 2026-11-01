# 2026-11-01 — First R25/R35 mesh batch: 4/8 matrix exports, 4/8 geometry-mesher failures

**Evidence:** user-uploaded `01_mesh.zip` from `D:\Users\TC FANG\Desktop\FYP sem2\32_CA2_V2_VALIDATION_BATCH\01_mesh`. Analysis is a **read-only parse of actual files**; no new AEDT simulations run by this reviewer. Historical R10/R15 comparisons and full adaptive mesh statistics require additional cross-audit. Do not call R35 "converged".

## Observed job status

| Geometry | R25 | R35 |
|---|---|---|
| NOM_GSG | EXPORTED_NEEDS_QA | EXPORTED_NEEDS_QA |
| NOM_GSSG | EXPORTED_NEEDS_QA | EXPORTED_NEEDS_QA |
| NOM_GSGSG | ERROR on Analyze(C_Setup1) | ERROR |
| OPT_GSGSG | ERROR on Analyze(C_Setup1) | ERROR |

Errors in all four GSGSG runs: `Phi mesher: Vertical facet cutting across Z level could not be split`, body `Si_Substrate`. Nominal near Z=13.5 µm; optimum near Z=8.5 µm. This diagnoses **initial meshing / geometry** failure, not a capacitance-convergence failure; inspect exact face intersections and diagnostic facet before proposing changes. Some surviving `.aedtresults` include failed-mesh diagnostics; their existence is not proof of successful solution.

## Parsed raw C/G matrices

| Target | R25 | R35 | (R35-R25)/R25 |
|---|---:|---:|---:|
| GSG S2 self C (fF) | 37.880312974 | 37.863347702 | -0.0448% |
| GSG abs(S2,SUB_REF) C (fF) | 1.646350271 | 1.597202783 | -2.985% |
| GSG S2 self G (mS) | .076462609 | .076231215 | -0.303% |
| GSSG S2 self C (fF) | 40.298842815 | 40.592121385 | +0.7278% |
| GSSG abs(S2,S3) mutual C (fF) | 12.777671006 | 12.915552570 | +1.0791% |
| GSSG abs(S2,SUB_REF) C (fF) | 1.245753405 | 1.226252339 | -1.565% |
| GSSG S2 self G (mS) | .082341885 | .085933843 | +4.362% |

All new exported matrices state `C_Setup1:LastAdaptive`, `Reduce Matrix: Original`, `Frequency: 1GHz`, `C Units:pF`, `G Units:mSie`. Embedded project files confirm `PerRefine=25` or `35`, `MaxPass=15`, `PerError=1`, `AdaptiveFreq=1GHz`. A larger `PerRefine` does not prove actual final mesh is finer: extract element counts/pass histories and numerical statuses.

## Interpretation and next decision

1. **Do not choose new mesh settings yet**. Only two topologies exported, substrate terms are >1% sensitive, GSSG mutual 1.079% sensitive, GSSG G diagonal ~4.36% sensitive; no final mesh size/pass histories extracted from this first audit.
2. **GSGSG repair priority**: preserve original physical model, contacts and excitation; locate the narrow/unsplittable `Si_Substrate` facet identified by nominalmesh.g3derr. Prefer controlled mesher/geometry healing that provably preserves geometry and report any differences; re-run source-aligned GSGSG R25/R35.
3. **Old R10/R15 pairing**: compare same named C/G coefficients, full matrix symmetry, PSD, solver configuration and mesh counts from original `22_CA2_PRIORITY3_NUMERICAL_VALIDATION` archive.
4. **DOE fidelity gate remains active:** freeze original 261 labels and nine blind. No decision to rerun full DOE until a credible final solver setup and representative paired old/new labels exist.
5. Report solver errors as *failed runs*, not missing rows or physics nonconvergence.

**This Markdown captures evidence already read from the ZIP, not the original full ZIP pushed to GitHub.** Raw Q3D .aedt and .aedtresults remain on local Windows or in user upload.
