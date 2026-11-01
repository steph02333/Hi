# DOE V2 — proposed targeted expansion (**NOT RUN**)

## Goal
Improve independent geometry-group prediction accuracy, particularly original **GSSG signal–signal mutual** MAPE 5.625%, via sample-efficient selection rather than blind random sweeps.

Original data: **261** accepted records = 216 original + 36 extra GSGSG development + 9 frozen GSGSG blind. Proposed addition **30 NEW geometry groups × 3 resistivities = 90 solves**. The total would be **351** only after all 90 cases actually solve, export, pass QA and are accepted.

| Layout | Novel geometry groups | Resistivities (Ω·cm) | Cases |
|---|---:|---|---:|
| GSG | 6 | 5, 10, 100 | 18 |
| GSSG | **18** | 5, 10, 100 | **54** |
| GSGSG | 6 | 5, 10, 100 | 18 |
| **TOTAL** | **30** | | **90** |

## Experimental controls — establish BEFORE new solves
1. Inspect exact original split manifest and 9 blind geometry IDs. Freeze stable **test geometry groups** (and random seed) before acquisition. Keep all three resistivities of a geometry in the same partition.
2. Do not use 9 blind rows to choose new sample locations, hyperparameters, models or stop criteria. Never evaluate repeatedly on blind.
3. Preserve V1 test geometry IDs so V2 can be compared on **identical** held-out cases. If original partitions unavailable, pre-register a new non-blind fixed test set and evaluate *both V1 and V2* against that same set.
4. Keep source baseline immutable with hashes; use unique `V2_LAYOUT_GROUP_R###` IDs and retain rejected/failed runs in manifest.
5. Sample new candidate geometry groups in D 3–6, P 10–20, H 25–50, tox 0.1–0.5 µm, with physical clearance constraint P>D. Use maximin LHS or scrambled Sobol + uncertainty and diversity, include relevant boundaries/optimum neighborhoods.
6. GPR posterior uncertainty is not guaranteed calibrated; pair with grouped-CV error and diversity, avoid only exploiting local maxima of uncertainty. Keep a reproducible seed and dated candidate manifest before executing solver.
7. Simulate 5/10/100 Ω·cm per geometry in Q3D with **same extraction physics** and matrix naming as the 261-case baseline. Record full C/G, solver pass, units, setup, mesh/domain, contact check.
8. QA: successful analyze AND exported matrix, symmetry & positive semidefinite, correctly mapped nets, coupled SUB_REF, no duplicated geometry or leakage. Record all rejected cases with reason.
9. Retrain and compare GPR on **identical** held-out geometry groups: R², MAE (fF), RMSE, MAPE, worst APE, rho-stratified errors and confidence interval coverage. Use geometry-block bootstrap if meaningful.
10. Re-solve selected new optimum geometries independently with Q3D; targeted mesh/domain checks where necessary. Do not represent surrogate accuracy as independent semiconductor accuracy.

## Minimal manifest columns
`case_id,layout,geometry_group_id,D_um,P_um,H_um,tox_um,rho_ohm_cm,solver_version,solver_type,material_model,frequency_hz,mesh_setting,domain_margin_um,solve_status,matrix_file,units,Cself_pF,Cmut_abs_pF,Gself_mS,qa_state,error,git_commit`

## Decision
DOE expansion is promising (earlier matched-validation 108→216 improved every observed target), **but improvement is not guaranteed**. Primary decision metric is GSSG mutual held-out MAPE on unchanged test geometry groups, plus per-target adverse changes and uncertainty. No predetermined percentage improvement is claimed.
