# CA2 Numerical Baseline — historical, evidence-qualified

**Status:** completed historical campaigns, not rerun by GitHub documentation migration. Every new result should state original source file and commit/hash.

## 261-case dataset accounting
| Dataset | Count | Use |
|---|---:|---|
| Original DOE | 216 | Three topologies × 24 distinct geometry groups × 3 resistivities |
| Supplementary GSGSG development | 36 | Hard/low-C design region |
| Supplementary GSGSG frozen blind | 9 | Three held-out geometry groups, never train or tune |
| **Total accepted** | **261** | **252 non-blind + 9 blind** |

Input features: TSV D (3–6 µm), edge spacing S=P-D (P 10–20 µm), height H (25–50 µm), oxide liner tox (0.1–0.5 µm), log10 rho (5,10,100 Ω·cm). Layout GSG/GSSG/GSGSG handled separately. Finite-resistivity silicon Q3D labels, not measurement ground truth.

## Original 216-case geometry-group-disjoint held-out GPR results
| Layout | Target | R² | MAPE |
|---|---|---:|---:|
| GSG | Self C | 0.993905 | 3.336% |
| GSSG | Self C | 0.993571 | 4.087% |
| GSSG | Signal mutual | 0.988524 | **5.625%** |
| GSGSG | Self C | 0.996372 | 2.566% |
| GSGSG | Signal mutual | 0.999007 | 2.058% |

Selected model: Matérn-kernel Gaussian Process Regression. These *original 216-stage test scores* must not be passed off as a new 252-development-stage score.

### Frozen independent GSGSG blind (9 rows)
Self: R² 0.999243, MAE 0.1195 fF, MAPE 1.104%, max APE 2.792%. Mutual: R² 0.999725, MAE 0.0139 fF, MAPE 0.707%, max APE 1.583%. No blind observations may guide V2 acquisitions.

## Independently Q3D re-solved constrained geometries
At rho 10 Ω·cm: GSG min self **13.85497 fF**; GSSG min self **15.217 fF**; GSGSG refined min both, D=3 P=20 H=25 tox=0.5 µm, self **14.284483 fF**, mutual |C| **2.429250 fF**, self conductance **0.0181003 mS**. Optima are within selected geometry/objectives and were re-solved in Q3D; they are not vendor HBM performance optima.

## Separate numerical/physical checks
- **9 coaxial analytical comparisons**: 3.61% mean relative difference; 3.14–4.02% range. Simplified cylinder, not complete TSV array.
- **21 controlled geometry solves**: 9/9 self-C and 6/6 applicable mutual-C *endpoint* trend directions passed. Not global monotonicity.
- **16 adaptive/domain sensitivity cases**: max pairwise signal self-C difference 0.640%, mutual up to 4.868%, substrate up to 13.084%. Not continuum-convergence proof.
- Recorded full C/G matrix symmetry and PSD checks for 261 accepted ML labels. Global Gauss-law closure unresolved.
- **12 lossless Q3D–Maxwell pairs** (24 successfully exported C matrices): **20 signal self entries mean relative difference 3.69%; 8 signal mutual entries 2.19%**. Q3D SUB_REF diagonals differ from Maxwell **32.37–71.88%**, signal/SUB_REF often about 39–70%; full-matrix mismatch remains unresolved.
- Original 108→216 matched-validation DOE experiment improved all five studied targets, but cannot guarantee continued improvement with expansion.

## Evaluation conventions
Surrogate APE = 100 × |C_pred − C_Q3D|/|C_Q3D|. Cross-solver difference = 100 × |C_Maxwell − C_Q3D|/|C_Q3D|. Off-diagonal signal mutual magnitude is absolute Maxwell-convention coupling. GSG has no signal-to-signal mutual.

**Do not count** the optimization verification, 21 geometry, nine coax, 16 sensitivity or 12 cross-solver experiments as new 261 production ML rows.
