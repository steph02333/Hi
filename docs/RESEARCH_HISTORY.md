# Curated Research History and Engineering Decisions

This history summarizes the important **known** technical milestones from prior project chats, source report and uploaded scripts/solver logs. It is not a verbatim complete chat export. All facts requiring source verification should be checked against original matrices, notebooks and report.

## CA1 — September 2026
Initial 3×3 TSV geometry-only approach, ~120 simulations, four geometry features, Q3D reference, early GPR and Q3D-optimum closure. Initial report dated September 16, 2026. Its definitions/scores are **not** directly interchangeable with CA2.

## September 26 — consultation
Prof. Yeow Kheng Lim recommended using term *high-fidelity reference solver* rather than ground truth; triangulation via coax analytical physics, mesh/domain numerical checks, C/G reciprocity and PSD, Gauss-law closure and independent field solver; local GSG, GSSG and GSGSG grounding patterns; resistivity study about 1/10/100 Ω·cm; later Sentaurus MOS bias study if meaningful. Suggested geometry D3–6 P10–20 H25–50 tox0.1–0.5 µm.

## CA2 — grounded finite-resistivity extraction
Parameterised Cu TSVs and SiO2 liners in simplified Si with top contacts and explicit SUB_REF. ρ values actually accepted = **5/10/100 Ω·cm** (the low-ρ 1 Ω·cm setting caused student solver difficulties). 1 GHz G matrix quantities, C matrix nets; no real DRAM 1T1C physical modelling or biased MOS charge transport. Five ML inputs D, P−D, H, tox, log10 ρ.

## Original 216 → supplementary 45
24 geometry groups per each of GSG/GSSG/GSGSG, times 3 rho → **216 accepted**. Group-aware splits keep same-geometry rho replicates together; Matérn GPR obtained high geometry-heldout R² with GSSG mutual the weakest original target (5.625% MAPE). A historical **108 versus 216 matched-validation comparison** showed benefit from extra geometry groups, not guaranteed linear improvement indefinitely.

Next, **45 more GSGSG** observations near low-C design region. 36 went to development and **9 were frozen** in a 3-geometry independent blind set. GSGSG blind self 1.104%, mutual 0.707% MAPE; full ML observation index **261**, including 9 evaluation-only rows. Some supplementary conductance entries absent from merged CSV; do not impute them.

## Optimisation and physical checks
Constrained GSG, GSSG and GSGSG ML-designed geometry candidates re-solved in Q3D. Refined GSGSG min-both D3 P20 H25 tox0.5 rho10: self14.2845 fF, signal mutual2.42925 fF. Nine coax analytical cases mean 3.61% difference; 21 controlled geometry endpoint tests passed 15/15 applicable directional checks; 16 adaptive/domain sensitivity cases found selected mutual/substrate variation >1%.

Gauss-law/charge surface integration tried with explicit excitation, but did **not** demonstrate a rigorous global closed-surface flux balance. This remains open.

## October 16 — Maxwell troubleshooting, then fresh complete run
AEDT full Electronics Desktop targeted configuration made Maxwell 3D Electrostatic accessible; earlier Twin Builder targeted configuration obscured options. First test solved but failed exporting Maxwell matrix, followed by unsuccessful existing-project export recovery attempts. Do **not** claim model failed just because API export failed.

User requested a single end-to-end 12-case Q3D+Maxwell script rather than more pilot/recovery iterations. Fresh 12 Q3D and 12 Maxwell designs subsequently solved and exported 24 matrices. Signal self comparison 3.69% mean difference (20 terms); signal mutual 2.19% (8 terms); substrate/reference terms differed by tens of percent.

Subsequent audit established **both models in this cross-solver campaign were lossless** (epsilon_r 11.9, sigma0), preventing a casual explanation of substrate mismatch via lossy Si alone. SUB_REF was a copper side contact. Differences in row sums/matrix reference remain unexplained; investigate boundary/terminal treatment without fitting a desired percentage.

## November 1 — revision planning and GitHub migration
User requested more DOE points, full technical review, and GitHub-first cross-agent handover. Proposed **90** new cases: 6 GSG geometry groups, 18 GSSG groups, 6 GSGSG groups, each 5/10/100 Ω·cm → 90 new rows; anticipated 351 total **if all succeed**. Hypothesis: prioritize GSSG mutual. No such new cases run yet.

GitHub account **steph02333** selected. Desired dedicated private repo HBM-4E-V2 previously inaccessible; public repo **steph02333/Hi** granted GitHub connector write access after GitHub App installation settings were fixed. Initial README committed on main at `44a053b5f36d08cb2a5eced8386971ae6281a913`. Research documents are being appended in later commits; do not claim binaries/raw AEDT archives present unless explicitly verified.

## Repeated mistakes to avoid
- A new printed report PDF is not equivalent to preserving raw matrices and source scripts.
- Different physical models should not be expected to produce matching capacitance; matched lossless electrostatics still requires matching nets/reference.
- Don't regenerate all 12 solver cases just to make a plot; use exported raw matrix and independent QA first.
- Don't let optimizer or active learning use frozen blind samples.
- Never claim more simulation data or GitHub migration than has actually occurred.
