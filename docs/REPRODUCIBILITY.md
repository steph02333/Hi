# Reproducibility Protocol

Original tools: Ansys Electronics Desktop **Student 2025 R2.4**, Q3D Extractor and Maxwell 3D Electrostatic; AEDT scripted automation using its compatible interpreter; Python/Jupyter/scikit-learn for DOE/GPR. **Do not guess exact package versions** until notebooks/environment files are checked.

Workflow: `frozen candidate manifest → parameterized Cu/SiO2/Si TSV geometry → Q3D solve → C/G matrices → QA → versioned CSV → group-disjoint GPR → model-assisted optimization → fresh Q3D verify → report`.

## Naming / immutable data
- Case IDs `BATCH_LAYOUT_GEOM_R###`, identical geometry group across rho replicates.
- All columns need physical units; explicit whether exported matrices are full, grounded or reduced, and terminal sign convention.
- Original raw matrix and solver logs are immutable; derivatives always trace back to source checksums.
- Keep split manifests in `data/splits/`; never move rho replicates of the same geometry across train/validation.
- Save actual solver version, frequency, material conductivity, adaptive settings, boundary/domain dimensions, postprocessing conventions and timestamp.

## Experiment QA gate
1. Solver completed **and** output matrix exported correctly.
2. Source, ground and SUB_REF nets match intended topology; symmetrical, physically plausible C/G and positive-semidefiniteness within documented tolerance.
3. Training subset excludes frozen blind geometry families; no new duplicate test geometry in acquisition.
4. Recompute MAE/RMSE/MAPE/R² on frozen groups; include worst-case and rho-specific errors.
5. New optimum re-solved in field solver and physics/numerical assumptions stated.
6. Log any failed simulation, export or invalid solve as a failed attempt, not a missing row.

## GitHub-first iteration
```bash
git pull --ff-only origin main
git checkout -b experiment/doe-v2-acquisition
# edit scripts / data / docs; include docs/ITERATION_LOG.md update
git add <reviewed paths>
git commit -m "exp: document DOE V2 acquisition and result provenance"
git push -u origin experiment/doe-v2-acquisition
# open PR with reproducibility details and meaningful test comparison
```

Large files: use Git LFS or off-repo secure archive + CHECKSUMS manifest. Public repositories must not host restricted JEDEC standards, private emails, credentials or private semiconductor IP.
