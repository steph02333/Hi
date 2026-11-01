# Repository migration status — 2026-11-01

**Destination:** steph02333/Hi (**public**, main). Initial README: commit 44a053b5f36d08cb2a5eced8386971ae6281a913.

## Committed and GitHub-readable
- README.md (short initial version, followed by expanded README update).
- AGENTS.md; docs/RESEARCH_HISTORY.md, RESULTS_BASELINE.md, VALIDATION_LIMITATIONS.md, DOE_EXPANSION_V2.md, SOURCE_INVENTORY.md, REPRODUCIBILITY.md, ITERATION_LOG.md; data/README.md; .gitignore.
- data/processed/216_grouped_test_metrics.csv (original five target rows, with full precision).
- data/validation/maxwell_q3d_12_case_summary.csv (original twenty case/metric aggregate rows).

## Not yet committed (do not infer presence)
- Full **261-row** dataset, original **216-row** cleaned CSV, the original 108-to-216 matched comparison CSV and **all geometry-group split manifests**.
- Historical Python scripts and original Jupyter notebooks; full pipeline and environment have not been reproduced directly from repository checkout.
- Last reference-audited **34-page PDF**, LaTeX source, figures, field QA outputs and raw Maxwell/Q3D capacitance TXT matrices.
- All zipped raw AEDT projects / results; large archives should be off-repo or Git LFS (after review).
- Licensed JEDEC standard PDFs/spreadsheets and professor correspondence must not be uploaded to this public repo without authorization.

**Status rule:** Documentation of an external filename in docs/SOURCE_INVENTORY.md is NOT a claim the file is in GitHub. Every future agent must verify files using the repo tree.

## Next migration actions
1. Decide whether this public staging repo should be made private; user wanted full FYP source and dedicated private HBM-4E-V2 exists but integration access previously failed.
2. Upload reviewed source files from the local starter bundle, versioned CSVs and scripts using local git or a GitHub binary-capable connector; record SHA-256 and git commit.
3. Once verified, replace this status with specific file paths and SHA-256. Do not record 'complete' until all intended components are actually present.
