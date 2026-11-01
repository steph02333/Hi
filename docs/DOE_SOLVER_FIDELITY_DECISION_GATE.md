# DOE V2 Decision Gate — Numerical Fidelity Before Dataset Expansion

**Decision date:** 2026-11-01. **Status: proposed policy, not simulation result.**

## Why the order has changed
The project owner correctly raised a methodological problem: if the mesh/domain convergence study changes our accepted Q3D extraction settings, we cannot simply train on the old 261 labels and add 90 cases extracted with a different numerical configuration while pretending all values have homogeneous fidelity.

**STOP-GATE:** Do not execute the proposed 90-case DOE V2 until the solver configuration/fidelity gate below is resolved. Preserve the historical 261 dataset and frozen blind sets unchanged.

## What must be fixed first
1. **Actual mesh convergence:** compare exact same A3 geometry, rho=10 ohm-cm, 1 GHz extraction, contacts, material and domain across existing R10/R15 and proposed higher per-pass refinement values; inspect mesh element counts, adaptive pass histories and individual C/G coefficients. A larger per-pass mesh growth percentage is not itself proof of finer final solution or convergence.
2. **Domain and reference independence:** original domain variants changed both X and Y margins; one-factor-at-a-time isolation and consistent SUB_REF are required, especially if full matrix coefficients are targets.
3. **Gauss-law charge accounting:** separate diagnostic of electrostatic flux; uncertainty here should not be 'fixed' by choosing mesh until charge calculation has correct surfaces and boundary terms.
4. **Dataset fidelity:** compare at least a geometry-distributed paired subset of **old vs candidate new solver settings** before concluding historical labels are reusable. Include nominal, hard/edge, optimum, rho extremes, and all three layouts. Calculate absolute and percentage deviations for Cself, |Cmut| and G targets if used.

## Predeclared decisions

| Outcome | Correct action |
|---|---|
| New mesh reaches stability and old-vs-new labels agree within a justified numerical error budget on a representative paired subset | **Keep original 261 labels** (with documented old extraction settings), use consistent chosen setup for new runs and quantify any solver-setting bias. Label this as a multi-fidelity caution unless equivalence is established. |
| Old-vs-new shift is systematic but small and can be quantified, with clear tolerance relative to surrogate error / optimization ranking | Either rerun affected subset and keep dataset versions separately, or consider a rigorously validated correction approach; **never silently transform all labels** or mix inhomogeneous datasets without provenance. |
| Shift is significant, varies strongly across geometry/rho, impacts target rankings or optimal geometry, or old extraction did not meet credible tolerance | **Redo the production DOE with the validated new settings**: re-run the full 216 original plus 45 supplementary geometry/rho cases as appropriate, or define a fully new dataset version and independent blind set. Keep 261 original as historical V1 and do not use old test scores as evidence for the revised model. |
| No convincing convergence achievable under Student Edition limits | Report numerical uncertainty and scope reduction; consider smaller domain/model, stricter source consistency, other solver licence or partial higher-fidelity re-solves. Do **not** claim a new mesh is validated or that full rerun fixes physics. |

## Proposed evidence thresholds (decision aids, NOT guarantees)
- Last consecutive refinements of **primary signal C** should be below approximately **1%**, in line with professor's requested numerical sensitivity. Also require observable mesh refinement, appropriate adaptive status, and ideally more than one refinement level or robust trend.
- Since old original heldout GPR MAPE is ~2–6%, compare solver-setting shifts against this scale and absolute fF target errors. Near-zero mutual terms need absolute error analysis, not MAPE alone.
- If new-old differences are comparable to ML errors or enough to change candidate ranking, old/new training labels should not be mixed under one identical-fidelity label.
- Domain and SUB_REF differences should be audited separately; a stable signal coefficient does not certify all substrate/G coefficients.

## Correct execution sequence
**A.** Verify old A3 baseline against original source .aedt and matrices (done in source bridge).  
**B.** Run controlled mesh/domain investigation (not yet run).  
**C.** Select one final solver configuration, and establish physics/numerical limitations.  
**D.** Run representative old/new paired bridge set (e.g. 12–24 geometry-rho combinations **chosen before results**, balanced across layouts/rho and boundary regions).  
**E.** Decide Keep / Recalibrate-with-evidence / Full redo.  
**F.** Reconstruct or retrain GPR on the final version with frozen group splits; if redo requires changing evaluation records, explicitly create a new untouched blind benchmark.  
**G.** Only then consider active-learning 90-case expansion if the revised model still needs coverage.

## Data-versioning and handover
- `data/v1_legacy/`: original 216 + 45 accepted, old solver settings. Nine blind remain protected.
- `data/v2_refined_solver/`: new solver settings, raw matrices and case metadata. Never overwrite the old 261.
- Store `old_case_id,new_case_id,geometry_fingerprint,physics_match,mesh_setting,domain_setting,source_hash,Cself_old,Cself_new,Cmut_old,Cmut_new,G_old,G_new,relative_difference,absolute_difference,qa` in a traceable **paired bridge manifest**.
- Compare data with exactly the same geometry, rho, excitation/net/reference and units. If model/domain physics changes, call it a **model revision**, not mere mesh refinement.

**Current status:** No higher-mesh results have yet been accepted, so **a full rerun is not yet scientifically justified or ordered**. The full redo decision must follow measured numerical evidence. This document supersedes the timing (not the proposed allocation) in DOE_EXPANSION_V2.md.
