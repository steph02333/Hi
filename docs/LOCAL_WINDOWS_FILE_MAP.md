# Windows File Map — Local FYP Archives & Handover

**Status:** Updated 2026-11-01. **Local path information, not evidence that files are in GitHub.**  
**User-confirmed Windows parent directory:** `D:\Users\TC FANG\Desktop\FYP sem2`

> **Privacy note:** This repository is public. The local path below was provided by the project owner for continuity. It contains a Windows profile-directory name; do not publish private email, credentials, supervisor correspondence, licensed standard content or personal documents. Avoid unnecessary absolute paths in new experiment outputs.

## What a new agent should do immediately

1. Read [AGENTS.md](../AGENTS.md), [README.md](../README.md), [RESEARCH_HISTORY.md](RESEARCH_HISTORY.md), [RESULTS_BASELINE.md](RESULTS_BASELINE.md), [VALIDATION_LIMITATIONS.md](VALIDATION_LIMITATIONS.md) and [ITERATION_LOG.md](ITERATION_LOG.md).
2. Inspect [MIGRATION_STATUS.md](MIGRATION_STATUS.md). Some detailed historical results are **on the Windows machine, not in GitHub**.
3. The user's canonical local parent is `D:\Users\TC FANG\Desktop\FYP sem2`. **Ask for a directory listing or confirm actual nested locations before scripting file access**. The entries labeled **candidate** below derive from archived output names and should NOT be assumed to exist as folders directly beneath the parent.
4. Read raw result files/manifest first; distinguish *planned, solved, exported, QA accepted, published*. Preserve the immutable nine-case GSGSG blind evaluation.
5. When producing new scripts, specify full output folder in the README, file manifest, and iteration log. If needed, request a ZIP of **only** the relevant folder, not all ~hundreds of MB of caches.
6. Update this file and [ITERATION_LOG.md](ITERATION_LOG.md) with verified exact paths/versions after each experiment.

## Known or explicitly recorded local Windows destinations

| Local Windows directory / file | Confidence | Description & what to look for |
|---|---|---|
| `D:\Users\TC FANG\Desktop\FYP sem2` | **USER CONFIRMED ROOT** | Main FYP CA2 workspace on the user's Windows computer |
| `D:\Users\TC FANG\Desktop\FYP sem2\31_CA2_Q3D_MAXWELL_RAW` | **CONFIRMED BY OCT 16 AEDT SCRIPT LOG** | 12 fresh paired geometries; Q3D and Maxwell .aedt projects and 24 exported capacitance matrices |
| `...\31_CA2_Q3D_MAXWELL_RAW\GSG_BASE_Q3D_matrix.txt` | **CONFIRMED BY SCRIPT LOG** | Example original Q3D GSG baseline matrix (lossless matched electrostatic comparison) |
| `...\31_CA2_Q3D_MAXWELL_RAW\GSG_BASE_MAX_matrix.txt` | **CONFIRMED BY SCRIPT LOG** | Matching Maxwell 3D Electrostatic matrix |
| `D:\Users\TC FANG\Desktop\FYP sem2\29_CA2_MAXWELL_CROSS_SOLVER` | **CONFIRMED BY EARLIER AEDT SCRIPT LOG** | Historical pilot: solved Maxwell but matrix export failed; NOT the final successful 12-case validation |
| `D:\Users\TC FANG\Desktop\FYP sem2\CA2_Q3D_MAXWELL_FIXED\CA2_Q3D_MAXWELL_FIXED\00_RECOVER_SOLVED_GSG.py` | **CONFIRMED BY FAILED SCRIPT TRACE** | Older recovery script; failed exporting matrix. **Do not use as the current successful pipeline.** |

The original 12-case campaign used **lossless** Si (epsilon_r 11.9, sigma=0) in both solvers; do **not** combine these matrices with finite-resistivity 1 GHz Q3D labels as if they were identical physical systems.

## Historical output artifacts whose exact Windows folder must be verified

The following filenames or names of archive families are **confirmed from uploaded copies or project history**, but this does **not** establish that each is at `ROOT\filename` or `ROOT\folder` on Windows. First search Windows Explorer from the confirmed root, or run `Get-ChildItem` as documented below.

| Historical name / search term | Status | Purpose |
|---|---|---|
| `17_CA2_GROUNDED_DOE_ML (2).zip` | Archive available in earlier shared workspace | Q3D grounded DOE / production simulation source |
| `18_CA2_GROUNDED_DOE_CHECKPOINTS.zip` | Archive available | Original checkpoints and source traces |
| `20_CA2_GSGSG_BOUNDARY_REPAIR.zip` | Archive available | Supplementary GSGSG difficult-region 45-case campaign; 9 cases frozen blind |
| `19_CA2_ACTUAL_OPTIMUM_Q3D_VERIFY.zip` | Archive available | Original Q3D optimum verification |
| `21_CA2_GSGSG_REPAIRED_OPTIMUM_VERIFY.zip` | Archive available | Refined GSGSG optimum |
| `22_CA2_PRIORITY3_NUMERICAL_VALIDATION.zip` | Archive available | Numerical and analytical validation inputs |
| `23_CA2_CONTROLLED_GEOMETRY_VALIDATION.zip` and possible `(2)` variant | Archive available | 21 controlled geometry physics runs |
| `31_CA2_Q3D_MAXWELL_RAW.zip` | Archive available | Entire completed 12-pair cross-solver project and output copy |
| `CA2_STEP6_216_RESULTS\01_cleaned_dataset.csv` | Filename observed in earlier workspace | Cleaned original 216-case ML dataset |
| `CA2_STEP6_216_RESULTS\03_grouped_split_manifest.csv` | Filename observed | Original geometry-group training/test split |
| `CA2_STEP6_216_RESULTS\07_FINAL_grouped_test_metrics.csv` | Filename observed | Source for five original 216-case held-out metrics |
| `CA2_STEP6_216_RESULTS\07_FINAL_grouped_test_predictions.csv` | Filename observed | Per-observation grouped-test predictions |
| `CA2_STEP6_216_RESULTS\10b_same_validation_108_vs_216.csv` | Filename observed | Matched-validation evidence for expansion benefit |
| `CA2_STEP6_216_COMPLETE_ML_PIPELINE (1).ipynb` | Filename observed | Python/Jupyter ML pipeline |
| `CA2_STEP7_OPTIMIZATION_AND_VERIFICATION (1).ipynb` | Filename observed | Optimisation and Q3D verification notebook |
| `CA2_GEOMETRY_21_VERIFIED\all_21_raw_results.csv` | Filename observed | Geometry endpoint checks |
| `CA2_PRIORITY3_VALIDATION\A3_ANALYTICAL_BENCHMARK_9.csv` | Filename observed | Nine coax analytical checks |
| `CA2_SCIENTIFIC_AUDIT\reference_matrix_12case_audit.csv` | Filename observed | SUB_REF and matrix row-sum cross-solver audit |
| `CA2_cross_solver_capacitance_comparison.csv` and `CA2_cross_solver_12_case_summary.csv` | Filenames observed | Signal-level cross-solver numerical comparisons |
| `CA2_Progress_Report_REFERENCE_AUDITED.pdf` | Filename observed | Most recent report in prior workspace; approximately 34 pages |
| `JESD270-4A_merged.pdf`, `JESD271-4_HBM4_Ballout.xlsx` | Source filenames observed | Licensed standards; **do not commit to public GitHub** |
| `Mail - Fang Tianchi - Outlook.pdf` | Source filename observed | Private supervisor consultation; **do not commit to public GitHub** |

## Fast local discovery (PowerShell)

From a **PowerShell terminal on the user's Windows computer**:

```powershell
$root = 'D:\Users\TC FANG\Desktop\FYP sem2'
Test-Path -LiteralPath $root
Get-ChildItem -LiteralPath $root -Directory | Sort-Object Name | Select-Object Name,FullName
Get-ChildItem -LiteralPath $root -Recurse -File -ErrorAction SilentlyContinue |
  Where-Object { $_.Name -match '(261|216|GSGSG|MAXWELL|Progress_Report|STEP6|STEP7|ITERATION)' } |
  Select-Object FullName,Length | Out-File -Encoding UTF8 "$root\FYP_LOCAL_FILE_INDEX.txt"
```

**Caution:** Full recursive listing over AEDT result caches may be slow/large. For rapid lookup search known subfolder paths or filename patterns. Review `FYP_LOCAL_FILE_INDEX.txt` for private info before uploading or publishing.

## Recommended future subfolders (NOT asserted to exist)

```text
D:\Users\TC FANG\Desktop\FYP sem2\
├── 31_CA2_Q3D_MAXWELL_RAW\       # previously recorded location
├── 32_CA2_V2_VALIDATION_BATCH\   # PROPOSED; not generated
│   ├── run_manifest.csv
│   ├── scripts\
│   ├── q3d_mesh\
│   ├── q3d_gauss\
│   ├── maxwell_reference\
│   └── logs\
└── FYP_LOCAL_FILE_INDEX.txt       # generated only if PowerShell command is run
```

## Evidence and limits

- Explicit local paths above were obtained from the **user's provided root** and **earlier AEDT solver logs**.
- Other artifact titles were observed in the prior assistant workspace/archives and may have been moved, renamed or unzipped elsewhere on the user's PC.
- GitHub cannot browse the user's local `D:` drive. Upload selected source files or a directory inventory to allow next agent to confirm exact locations.
- The proposed mesh convergence / Gauss-law / Maxwell-reference batch is not yet run; no new simulation results claimed.

## What to tell the next agent

> This is the HBM TSV CA2 FYP. Begin at AGENTS.md and docs/LOCAL_WINDOWS_FILE_MAP.md. Local working root: `D:\Users\TC FANG\Desktop\FYP sem2`. Existing 12-pair Q3D/Maxwell RAW location confirmed from logs. Prior results are partly local-only; do not assume GitHub has the full 261-case dataset or raw AEDT models. Our next priority is a multi-task validation batch (mesh convergence, Gauss-law flux accounting, substrate reference). Every change must be logged to docs/ITERATION_LOG.md and paths in this map updated after the runs.
