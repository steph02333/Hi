# A3 Source-Aligned Redo — Primary Next Experiment (2026-11-01)

**Status:** Historical source A3 ZIP independently audited here. Follow-up AEDT script **prepared, not yet executed in AEDT**. Do not call candidate settings numerical results.

## Actual legacy source and exact reproducibility anchors

Original source: `22_CA2_PRIORITY3_NUMERICAL_VALIDATION.zip`  
SHA-256: `f93a0c2c6c25306b86bde308dc012104a78c62ec582e26143535bf4746e2a40e`  
Confirmed Windows original project location: `D:\Users\TC FANG\Desktop\FYP sem2\22_CA2_PRIORITY3_NUMERICAL_VALIDATION\`.

Independent parsing of `A3_RUN_MANIFEST.tsv` and source `.aedt` confirmed **16 ACCEPTED SOLVED** records: four geometry families × four variants each (**BASE_R15, MESH_R10, DOMAIN_25, DOMAIN_30**). **These are NOT four consecutive mesh refinement levels.** Every case uses silicon rho=10 Ω·cm, Q3D's 1GHz electrical extraction and the model's actual SUB_REF contact.

| Source family | D | P | H | tox | Baseline Cself (fF) | Baseline signal mutual (fF) |
|---|---:|---:|---:|---:|---:|---:|
| NOM_GSG | 4.5 | 15 | 35 | .3 | 37.834550 | N/A |
| NOM_GSSG | 4.5 | 15 | 35 | .3 | 40.261570 | 12.738304 |
| NOM_GSGSG | 4.5 | 15 | 35 | .3 | 40.909254 | 6.778877 |
| OPT_GSGSG | 3 | 20 | 25 | .5 | 14.284483 | 2.429250 |

Legacy baseline setup, verified from embedded AEDT `C_Setup1`: `AdaptiveFreq=1GHz`, `MaxPass=15`, `MinPass=2`, `MinConvPass=2`, `PerError=1`, `PerRefine=15`, `AutoIncreaseAccuracy=true`, `AccuracyLevel=High`, `Solver Type=Direct`, `Compression Tolerance=1e-6`, `SaveFields=true`. Historical MESH_R10 only changed the percentage refinement from 15 to 10.

## Source-aligned next batch

A Python 3 standard-library audit generated `existing_16_source_inventory.csv`, `actual_A3_pairwise_changes.csv`, and `candidate_redo_manifest_NOT_RUN.csv` and source verification summary, available as **locally generated `CA2_VALIDATION_BRIDGE_V2.zip`** (not necessarily uploaded to GitHub). It also contains an **EXPERIMENTAL, AEDT-untested** IronPython script `RUN_AEDT_MESH_REFINEMENT.py` that copies **the four actual old A3 baseline .aedt files** to `32_CA2_V2_VALIDATION_BATCH\01_mesh\` and requests **25% and 35% per-pass mesh refinement** in new copies (8 candidate runs).

We chose 25 and 35 instead of 7 and 5 because **in AEDT PerRefine specifies mesh growth percentage per pass**; smaller percentages do not automatically represent tighter mesh. <https://ansyshelp.ansys.com/public/Views/Secured/Electronics/v252/en/Subsystems/Q3DExtractor/Subsystems/Q3DExtractor%20Scripting/Content/InsertSetupQ3DExtractor.htm>

Check adaptive mesh element counts, pass counts, exported C/G names/units, unchanged geometry, contact positions, solver version and student-edition failures before claiming actual refinement or convergence. Any scripting API setup alias/export error is **not** a field-physics failure.

## Match old vs new by physics, not filename

- A3 is **lossy finite-resistivity rho=10 Ω·cm Q3D**. The separate 12-pair Q3D–Maxwell campaign used **lossless sigma=0** in both tools. Never compare raw self-C from these as if matched material physics.
- Original A3 `DOMAIN_25` / `DOMAIN_30` variants changed **both** `xmargin_pitch` and `yhalf_pitch`. They cannot isolate which boundary causes substrate sensitivity. For a stronger test, hold one factor/contact constant while varying only the other, and record the actual SUB_REF contact position.
- The old `MESH_R10` vs `BASE_R15` comparison is **only a two-setting numerical sensitivity**, not full mesh convergence.
- If new settings don't produce increased mesh or if C/G drifts, report the observed limitation and plan a stricter test rather than cherry-picking.
- Do not reuse the prior Gauss-law flux diagnostic as validated physical nonconservation.

## Next action

User unzips existing archive under verified Windows root and runs `RUN_AEDT_MESH_REFINEMENT.py` through **Tools → Run Script**, uploads `mesh_runs.tsv` and `*_CGmatrix.txt` plus adaptive profiles. New results are only accepted after matrix QA and comparison with the old baseline. Append `docs/ITERATION_LOG.md` upon results.
