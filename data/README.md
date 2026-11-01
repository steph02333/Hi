# Dataset Schema and Leakage Prevention

**Current GitHub state:** this file documents data; it does not imply the complete source 261-row CSV has been committed.

## Features
`D_um`: TSV diameter. `P_um`: center-to-center pitch; edge spacing `S_um = P_um − D_um`. `H_um`: TSV height. `tox_um`: SiO2 liner. `rho_ohm_cm`: Si resistivity, ML input `log10(rho)`. Different topologies modelled separately.

## Targets and conventions
`Cself_pF`: diagonal signal self in grounded/reduced capacitance convention; `Css_abs_pF`: absolute negative off-diagonal signal–signal coupling (GSSG/GSGSG only). GSG mutual undefined. G matrix where available; **missing G in 45 supplemental rows is not zero**.

## Partitions
- 216 original Q3D finite-conductivity runs.
- 36 supplementary GSGSG development cases.
- **Nine frozen GSGSG blind** cases: never select/tune/train on them.
- Separate 12 lossless Maxwell/Q3D pairs: external validation, not extra lossy-silicon ML rows.
- Planned DOE V2 90 rows not generated.

Never split identical geometry at different rho values across training and testing; use GroupKFold or geometry-disjoint split. Save exact group ID list, seed, preprocessing, model version and numeric predictions. Compare V1/V2 on same evaluation observations.
