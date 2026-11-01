# Research Iteration Log — append-only

Historical milestones are reconstructed from original report and conversation context, not a full exported transcript. Append experiment evidence *at the same time* as code/data changes.

### 2026-09-16 — CA1 prototype
Original 3×3 TSV, ~120 simulations, early surrogate. CA1 model/net arrangements differ from CA2; no direct metric comparison.

### 2026-09-26 — Prof. Lim consultation
Recommendations: grounded GSG/GSSG/GSGSG, finite-resistivity rho study, analytical coax validation, C/G checks, mesh/domain, independent solver, Gauss surface charge and potential MOS bias-dependent Sentaurus. Q3D designated high-fidelity reference, not ground truth.

### October 2026 — production DOE + GPR
**Completed:** 216 original Q3D runs, 24 geometry groups × 3 layouts × 3 rho. Matérn GPR with geometry-group split. Original heldout MAPE self GSG 3.336%, GSSG 4.087%, GSGSG 2.566%; GSSG mutual 5.625%, GSGSG mutual 2.058%.

### October 2026 — hard-region GSGSG supplementary + blind
**Completed:** 45 extra Q3D cases; 36 development plus 9 frozen blind (3 geometries). Database 261 including blind. Blind GSGSG self 1.104%, mutual 0.707% MAPE. Some supplementary G targets missing in consolidated CSV.

### October 2026 — optima and physics checks
**Completed:** three-layout Q3D re-verification of optimum/tradeoff candidates; nine coax analytical checks; 21 geometry endpoints; 16 mesh/domain sensitivity configurations; matrix reciprocity/PSD. **Not completed:** rigorous global Gauss-law closure, full stable substrate reference convergence.

### 2026-10-16 — Maxwell independent numerical cross-check
**Historical failure:** first Maxwell model solved but scripting export failed; later fresh all-12 single AEDT script solved **24 cases** and exported 24 matrices successfully. **Measured:** matched lossless electrostatic signal self mean 3.69%, mutual mean 2.19%; SUB_REF diagonal 32–72% disagreement. Root cause unproven; lossy finite-resistivity production model not cross-validated by this experiment.

### 2026-11-01 — targeted DOE V2 planned
**Proposed, not run:** 30 new geometry groups × 3 resistivities = 90 cases, focused 18 groups on GSSG plus 6 each GSG/GSGSG; 261→351 only upon acceptance. Preserve matched heldout groups and nine blind. Evaluate predictive gain rather than assume more samples automatically improve physics.

### 2026-11-01 — GitHub bootstrap
**Repository:** steph02333/Hi, public. **Initial README committed:** 44a053b5f36d08cb2a5eced8386971ae6281a913. **Documentation stage:** current migration. Check GitHub commits for what was actually written. Original AEDT source projects, paid JEDEC standards, personal emails and binary PDF reports not automatically published.

## Required template for all future work
```markdown
### YYYY-MM-DD — EXP-YYYYMMDD-NNN
Objective/hypothesis:
Base Git commit + exact dataset hash/split IDs:
Simulation geometry, material, solver setup and random seed:
Files changed; output CSV/matrix manifests:
QA: solver completion, matrix properties, leakage, group metrics:
Observed errors and limitations:
Scientific conclusion; what remains unverified:
Next step + owner:
```


### 2026-11-01 — GitHub local Windows file-location handover
**Objective:** make project state understandable to another agent after this chat ends.
**Completed:** published `docs/LOCAL_WINDOWS_FILE_MAP.md`, based on user-confirmed Windows root `D:\Users\TC FANG\Desktop\FYP sem2` and prior AEDT logs. Confirmed successful 12-pair source directory `31_CA2_Q3D_MAXWELL_RAW`, historical Maxwell pilot `29_CA2_MAXWELL_CROSS_SOLVER`; tagged other source filenames as *to verify* rather than inventing paths.
**Limitations:** no direct access to Windows D: filesystem; full raw source archives and full 261-case data are not automatically present in GitHub.
**Next:** design a consolidated but scientifically separable mesh/charge/reference validation batch, output to a versioned folder, and update map with exact file paths and run results.


### 2026-11-01 — PHASE-A0: read-only verification and validation plan
**Objective:** identify the most defensible next experiments before expanding DOE.  
**Inputs:** existing `31_CA2_Q3D_MAXWELL_RAW.zip` (12 Q3D and 12 Maxwell matrices; original lossless comparison).  
**Actions:** independently parsed raw matrix TXT files with a Python 3 standard-library reader, matched terminal labels, computed signal coefficient differences and matrix-QA rows.  
**Observed:** 20 signal self comparisons mean **3.6915%** (max **5.1450%**), 8 mutual comparisons mean **2.1934%** (max **5.1008%**). Reproduces earlier reported aggregate values.  
**Output:** offline `FYP_VALIDATION_V2_STARTER.zip` contains the reader, two generated baseline CSVs, and detailed batch plan; the ZIP is a local deliverable, not presently committed to GitHub. New GitHub document: `docs/VALIDATION_PHASE_A_PLAN.md`.  
**Limitations:** no new AEDT solve, Gauss-law verification or substrate-root-cause proof performed in this iteration.  
**Next:** verify original Q3D model setup and automate mesh/domain experiments with explicit solver failure handling; keep Gauss-law as separately testable field methodology before blending into unattended run.  


### 2026-11-01 — EXP-A3-SOURCE-BRIDGE: old solver project → controlled mesh redo
**Inputs:** original `22_CA2_PRIORITY3_NUMERICAL_VALIDATION.zip` (SHA-256 `f93a0c2c6c25306b86bde308dc012104a78c62ec582e26143535bf4746e2a40e`).
**Verified:** A3 run manifest has 16 solved/accepted combinations: four geometry families each with BASE_R15, MESH_R10, DOMAIN_25, DOMAIN_30. Embedded baseline AEDT setup is `C_Setup1`, 1GHz, MaxPass15, MinPass2, MinConvPass2, PerError1, PerRefine15, high/direct. Domain variants changed both x and y bounds.
**Created locally:** `CA2_VALIDATION_BRIDGE_V2.zip` with Python A3 audit, comparison CSV, NOT_RUN candidate manifest, experimental `RUN_AEDT_MESH_REFINEMENT.py` and instructions. This script **has not been tested in AEDT**. It copies existing .aedt models and attempts 25%/35% mesh growth variants, not new physics/geometry.
**Published GitHub:** `docs/A3_SOURCE_ALIGNED_REDO_2026-11-01.md` details exact baseline and planned checks.
**No new simulations completed:** mesh convergence, substrate-reference matching and Gauss-law remain open. Next: run script locally, capture errors/profiles/matrices, reject mismatches, then log analysis.
