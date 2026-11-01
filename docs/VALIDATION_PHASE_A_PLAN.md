# Phase A — targeted validation, 2026-11-01 (planned + baseline audit)

**Read first:** AGENTS.md, RESULTS_BASELINE.md, VALIDATION_LIMITATIONS.md, LOCAL_WINDOWS_FILE_MAP.md. **Do not claim new AEDT simulations have been run.**

## A0: Re-audit existing 12 paired cross-solver matrices (DONE, READ-ONLY)
An offline Python 3 (stdlib-only) parser successfully re-read the original `31_CA2_Q3D_MAXWELL_RAW.zip` with 12 Q3D/Maxwell matrix pairs, checked terminal mapping and compared raw C values. Independently recomputed: **20 signal self comparisons mean 3.6915%, max 5.1450%; 8 mutual comparisons mean 2.1934%, max 5.1008%**. It saved `matrix_QA.csv` and `signal_comparison.csv` in local `V2_EXISTING_MATRIX_QA`; those new outputs are not yet necessarily committed in GitHub. Matrix row sums do **not** establish Gauss-law conservation.

## A1: Mesh convergence (TO RUN)
Four finite-resistivity Q3D geometries at rho=10 Ω·cm: baseline GSG, GSSG, GSGSG D4.5/P15/H35/tox0.3 µm; optimized GSGSG D3/P20/H25/tox0.5. Four successive *actual* refinements M1–M4 per geometry; save full C/G matrices, mesh tetrahedra/pass counts, adaptation histories, setup and solver versions. Verify stronger settings genuinely refine the mesh. Calculate consecutive relative changes in signal self/mutual, signal-to-SUB_REF and reduced outputs. Aim <1% signal coefficients at last two refinements; report student-limit failures and other coefficient discrepancies openly.

## A2: Domain independence (TO RUN)
Use same mesh/excitations/materials and nominal structure across three growing exterior domain margins (e.g., 20/25/30 µm). **Check whether SUB_REF side copper contact and exterior boundary move**: modifying both simultaneously would confound attribution. Report dimension and reference geometry changes explicitly.

## A3: Gauss law (METHOD REDO, TO RUN)
First establish a **simple lossless coax/single-conductor** field-charge audit with a legitimate closed, consistently oriented surface and `Q_flux=∮D·n dA`; compare against matrix charge for identical excitation. Document dielectric interface/free-charge distinction and outer-boundary contribution. Do not reuse old oxide-surface ~90% diagnostic as verified physical conservation error. If AEDT field postprocess cannot implement the integral reliably, state that limitation.

## A4: Maxwell/Q3D SUB_REF reference mismatch (CONTROLLED, TO RUN)
Start from original matched **lossless** GSG baseline pair and original matrix exports. Verify matching geometry, terminal mapping, matrix types, outer boundaries, side-contact copper SUB_REF. Then run matched-condition pair and vary **one** suspected boundary/reference factor. Do not rerun all 12 just for aesthetics or tune until error falls below an arbitrary threshold. Existing source data show substrate terms differ by tens of percent, root cause unproven.

## A5: rho=1 Ω·cm (FEASIBILITY FOLLOW-UP)
After mesh protocol established, test one nominal case per layout at conductivity 100 S/m. If successful, consider larger campaign; if Student Edition fails record logs. Not part of original accepted 5, 10, 100 Ω·cm production DOE.

## Run management
Recommended local root: `D:\Users\TC FANG\Desktop\FYP sem2\32_CA2_V2_VALIDATION_BATCH`; keep separate `00_existing_matrix_audit`, `01_mesh`, `02_domain`, `03_gauss`, `04_reference`, `05_rho1`, `logs`. Freeze case IDs, input model and solver configurations before runs. Append `docs/ITERATION_LOG.md` in each data/code commit. Until actually run and verified, A1–A5 remain **planned**.

## Why not add 90 DOE rows first?
GSSG mutual original grouped-test MAPE was 5.625%, so DOE V2 is promising, but it only improves agreement with the Q3D reference; it cannot rectify unreliable fields, boundary mismatch, full Gauss law or semiconductor MOS physics. The nine blind GSGSG cases remain **frozen**.
