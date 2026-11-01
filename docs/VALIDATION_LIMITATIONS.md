# What Can Be Claimed — and What Cannot

## Completed evidence
- 216 original production Q3D finite-resistivity cases + 45 supplementary GSGSG cases; nine of 45 are frozen blind.
- 5 target-specific Matérn GPR grouped held-out test results; nine GSGSG independent blind cases.
- Three-layout constrained optimisation with fresh Q3D re-solves.
- Nine analytical coax benchmarks, 21 controlled geometry cases, 16 mesh/domain experiments.
- Internal full C/G symmetry and passivity checks.
- 12 paired Q3D and Maxwell **lossless** electrostatic simulations with successfully exported raw matrices.

## Unresolved or partial — do not overstate
1. **Substrate-reference discrepancy:** signal self average difference 3.69%, signal mutual 2.19%; SUB_REF diagonal coefficient differs 32.37–71.88%. Matrix row sums differ: Maxwell near zero, Q3D ~1.035–1.357 fF maximum row sum. These observations may relate to reference boundaries, solver terminal convention or numerical setup. Root cause **not uniquely established**. Row sums alone are not proof of Gauss law.
2. **Lossy Si physics:** original Q3D data used rho=5,10,100 Ω·cm, with conductance at 1 GHz. In *this separate validation campaign*, BOTH Maxwell and Q3D were deliberately set epsilon_r=11.9 and sigma=0. Thus comparison does **not** independently validate lossy AC silicon.
3. **SUB_REF geometry:** finite side copper pad/contact, not a uniform equipotential silicon bulk. Q3D net assignment and Maxwell electrode voltage assignment are not by themselves proof of identical external-boundary charge accounting.
4. **Gauss-law accounting:** conductor/oxide surface integrals were attempted but do not establish a complete independent closed-surface displacement-flux balance; the script's ~90% diagnostic discrepancy is NOT a physical violation of Maxwell equations.
5. **Mesh and domain:** signal self mostly stable in tested comparisons, but mutual/substrate terms sometimes exceed 1%; 16 cases do not prove continuum convergence.
6. **ρ=1 Ω·cm:** suggested by consultant but not in accepted dataset, due to solver/student edition limitations; 5/10/100 only.
7. **Bias and semiconductor physics:** Q3D/Maxwell Electrostatic do not automatically capture MOS inversion, accumulation, depletion, carrier dynamics. Sentaurus voltage-biased MOS study **not done**, and access/licence unverified.
8. **Vendor/measurement:** reduced TSV neighbourhood, not a proprietary commercial HBM4E die, complete DRAM transistor array, package SI, lab capacitance measurements, or cross-vendor independent validation.
9. **Student edition:** mesh limits/features may restrict fidelity; do not invent solver configurations, memory or mesh-size values.

**Terminology:** call Maxwell comparison *partial cross-solver validation of selected signal capacitance coefficients under matched lossless electrostatic assumptions*, not validation of complete finite-conductivity TSV physics.
