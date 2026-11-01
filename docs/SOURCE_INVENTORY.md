# Source Inventory and GitHub Migration Status

**This index lists earlier project files, NOT proof they have been pushed.** Use GitHub commit history and `docs/ITERATION_LOG.md` for what is actually committed. Preserve original filenames and SHA-256 if possible.

## Locally present research artifacts as of Nov 1, 2026
- **Latest 34-page report:** `CA2_Progress_Report_REFERENCE_AUDITED.pdf`; earlier variants `CA2_Progress_Report_UPDATED_Maxwell.pdf` and `CA2_Progress_Report.pdf`.
- **Complete reported ML dataset:** `CA2_FULL_REPORT/data/CA2_all_261_Q3D_ML_database.csv` and original 216 sample CSVs.
- **GPR experiments:** `CA2_STEP6_216_COMPLETE_ML_PIPELINE (1).ipynb`, `CA2_STEP6_216_RESULTS/`, `CA2_checkpoint_108_vs_216_cv.csv`.
- **Optimisation:** `CA2_STEP7_OPTIMIZATION_AND_VERIFICATION (1).ipynb`; verified Q3D matrix extracts in optimum archives.
- **Independent physics checks:** `CA2_GEOMETRY_21_VERIFIED/`, `CA2_PRIORITY3_VALIDATION/`, `CA2_CHARGE_FINAL/`, plus coax/numerical source ZIPs.
- **Cross solver:** `31_CA2_Q3D_MAXWELL_RAW.zip` (12 paired Q3D+Maxwell raw projects/matrices), `CA2_cross_solver_capacitance_comparison.csv`, `CA2_cross_solver_12_case_summary.csv`, `CA2_SCIENTIFIC_AUDIT/reference_matrix_12case_audit.csv`.
- **Source ZIP archives:** `17_CA2_GROUNDED_DOE_ML (2).zip`, `18_CA2_GROUNDED_DOE_CHECKPOINTS.zip`, `20_CA2_GSGSG_BOUNDARY_REPAIR.zip`, `22_CA2_PRIORITY3_NUMERICAL_VALIDATION.zip`, and many historical runs.

## Publishing status
- The GitHub API available in this chat supports UTF-8 text file creation and update. Binary PDFs, AEDT projects and ZIP archives **are not automatically uploaded** just because they exist locally.
- For public repository **steph02333/Hi**, first publish reviewed documentation and permitted derived data; DO NOT publish private professor email, licensed JEDEC PDFs, private correspondence, IDs, token files or unpublished proprietary geometry.
- Repository's initial README was committed in a prior turn. This handover document references historical available materials; each additional published file must be listed with correct GitHub path and commit.

## Missing/limited source information
- User's full conversation history is not available as an export; curated milestones are derived from report, archived summaries and logs.
- Supplementary GSGSG 45 rows lack certain conductance fields in merged index; missing != 0.
- Student edition AEDT licences/mesh may differ between host and CI environments.
- `HBM-4E-V2` private repo was not accessible to connector when checked, while `Hi` is accessible and public.

## Migration checklist
1. Commit reviewed scripts, small numerical CSVs, notebooks, split manifests with hashes and dependency versions.
2. Archive raw .aedt/.aedtresults ZIPs outside Git or approved LFS and record SHA-256 + secure retrieval.
3. Publish report PDF only after assessing privacy/licensing; avoid reproducing professor's email or protected standard attachments.
4. Reproduce old metrics from checked-in data and check group leak safeguards.
5. Each new batch gets versioned CSV and iteration entry — NEVER overwrite original dataset.
