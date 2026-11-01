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
