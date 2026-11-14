# PENTA(mer): Computational Modeling Framework

Extended documentation for the four computational models driving **PENTA(mer): A Wash-Free Saliva Assay for Congenital Cytomegalovirus Screening** (Lambert High School iGEM Proposal, Smyan Reddy).

## Assay & Modeling Overview

Congenital cytomegalovirus (cCMV) affects approximately 1 in 200 newborns in the United States and is the leading non-genetic cause of sensorineural hearing loss. Most infected infants are asymptomatic at birth, causing hearing-targeted screening workflows to miss children whose hearing loss develops or progresses later in early childhood.

**PENTA(mer)** is a wash-free saliva assay targeting the assembled human cytomegalovirus (HCMV) epithelial- and endothelial-entry pentameric complex (`gH/gL/UL128/UL130/UL131A`). The sensor uses two neutralizing antibodies, `8I21` and `13H11`, which bind non-overlapping epitopes on the assembled complex (Kschonsak et al., 2022). Each antibody is engineered as a single-chain variable fragment (scFv) fused via a flexible glycine-serine linker to one half of `TEM-1` $\beta$-lactamase split between residues `196` and `198` (Marsh & Owen, 2025). Neither fragment is enzymatically active alone; simultaneous binding of both scFv arms to the same assembled pentamer brings the two fragments together to reconstitute the active enzyme, cleaving nitrocefin to produce a yellow-to-red colorimetric transition at `486 nm` (or cleaving fluorogenic `CCF2` if higher sensitivity is required).

Color changes are measured using a stratified three-tier open-source hardware reader ladder:
1. **Baseline tier**: 3D-printed dark box with a smartphone camera and color reference card.
2. **Mid-tier unit**: `ESP32` microcontroller paired with a high-frequency switched LED source and photodiode detector, reading the signal synchronously at the switching rate to negate ambient room light and sensor drift.
3. **Advanced tier**: Filtered-LED fluorescence reader integrated with a disposable cartridge designed to filter oral bacteria, concentrate virions, and hold a secondary reaction chamber to correct for background bacterial $\beta$-lactamase activity.

---

## The Four Integrated Computational Models

Assay engineering, reader calibration, clinical sensitivity evaluation, and construct geometry verification are driven by four computational models:

| Model | Focus | Extended Documentation |
| :--- | :--- | :--- |
| **1. Kinetic Sensor Model** | Dual-scFv (`8I21` and `13H11`) binding to the epithelial-entry pentamer complex and Michaelis-Menten enzyme kinetics of reconstituted `TEM-1` $\beta$-lactamase cleaving nitrocefin (`486 nm`). | [`models/01-kinetic-sensor-model.md`](models/01-kinetic-sensor-model.md) |
| **2. Photometric Calibration Model** | Four-parameter logistic (`4PL`) sigmoid curve fitting optical signal against concentration, assigning detection probabilities between `0` and `1`, defining the limit of detection (`LOD`), and flagging high-dose hook effects. | [`models/02-photometric-4pl-calibration.md`](models/02-photometric-4pl-calibration.md) |
| **3. Clinical Feasibility Model** | `SIR`/`SEIR` compartmental modeling of infant viral load dynamics and congenital CMV impact, mapping expected newborn saliva viral loads against the assay's measured limit of detection (`LOD`). | [`models/03-clinical-feasibility-seir.md`](models/03-clinical-feasibility-seir.md) |
| **4. Structural Molecular Dynamics Model** | `GROMACS` molecular dynamics simulations built from PDB entries [`5VOB`](https://www.rcsb.org/structure/5VOB), [`7T4S`](https://www.rcsb.org/structure/7T4S), and [`7M22`](https://www.rcsb.org/structure/7M22), calculating `RMSD`, `RMSF`, `betweenness`, `eigenvector`, and `connectedness` centralities, `SASA`, and `radius of gyration`. | [`models/04-structural-molecular-dynamics.md`](models/04-structural-molecular-dynamics.md) |

---

## Coupling to Wet-Lab Validation Experiments

The modeling framework provides testable predictions across three core areas: **scFv working concentration**, **dose-response curve shape**, and **limit of detection (`LOD`)**. Models are iteratively refined against six mock-virion validation experiments using nickel-charged beads coated with recombinant pentamer suspended in synthetic saliva:

1. **Experiment 1 (Single-arm baseline)**: Tests individual scFv fusion arms alone without antigen to parameterize baseline signal in Model 1.
2. **Experiment 2 (Dual-scFv complementation)**: Places both `8I21` and `13H11` scFv fusions simultaneously with pentamer-coated beads in synthetic saliva to validate the Michaelis-Menten turnover and complementation kinetics in Model 1.
3. **Experiment 3 (Complex specificity)**: Evaluates specificity against related HCMV glycoprotein complexes (`gH/gL` dimers and `gH/gL/gO` trimers lacking pentamer-specific `UL128/UL130/UL131A` subunits), paired with Model 4 structural geometry.
4. **Experiment 4 (Receptor competition)**: Assesses binding site structure through receptor binding assays using soluble neuropilin-2 (`NRP2`, PDB `7M22`), paired with Model 4.
5. **Experiment 5 (Serial titration & LOD)**: Establishes sample concentration and titration protocols to define the analytical limit of detection (`LOD`) via Model 2 (`4PL` sigmoid calibration) and evaluate clinical saliva clearance in Model 3.
6. **Experiment 6 (Saliva matrix interference)**: Compares filtered saliva against unfiltered saliva to quantify background interference from endogenous oral bacterial $\beta$-lactamases for Models 1 and 2.

---

## References

- Chandramouli, S., et al. (2017). Structural basis for potent antibody-mediated neutralization of human cytomegalovirus. *Science Immunology*, 2. (PDB `5VOB`)
- Fowler, K. B., et al. (1997). Progressive and fluctuating sensorineural hearing loss in children with asymptomatic congenital cytomegalovirus infection. *Journal of Pediatrics*, 130, 624-630.
- Galarneau, A., Primeau, M., Trudeau, L. E., & Michnick, S. W. (2002). $\beta$-Lactamase protein fragment complementation assays as in vivo and in vitro sensors of protein-protein interactions. *Nature Biotechnology*, 20, 619-622.
- Gantt, S., et al. (2020). Performance of the Alethia CMV assay for detection of cytomegalovirus by use of neonatal saliva swabs. *Journal of Clinical Microbiology*, 58.
- Heras, R. de las, et al. (2008). Development of homogeneous immunoassays based on protein fragment complementation. *Biochemical and Biophysical Research Communications*, 370, 164-168.
- Kimberlin, D. W., et al. (2015). Valganciclovir for symptomatic congenital cytomegalovirus disease. *New England Journal of Medicine*, 372, 933-943.
- Kschonsak, M., et al. (2022). Structural basis for HCMV Pentamer receptor recognition and antibody neutralization. *Science Advances*, 8. (PDB `7T4S`)
- Lebel, P., et al. (2024). A handheld luminometer with sub-attomole limit of detection for distributed applications in global health. *PLOS Global Public Health*, 4.
- Lobstein, J., et al. (2012). SHuffle, a novel *Escherichia coli* protein expression strain capable of correctly folding disulfide bonded proteins in its cytoplasm. *Microbial Cell Factories*, 11.
- Lutz, C. S., et al. (2025). Updated national and state-specific prevalence of congenital cytomegalovirus infection, United States, 2018-2022. *Journal of Public Health Management & Practice*, 31, 234-243.
- Ni, Y., et al. (2021). A plug-and-play platform of ratiometric bioluminescent sensors for homogeneous immunoassays. *Nature Communications*, 12.
- Wrapp, D., et al. (2022). Structural basis for HCMV Pentamer recognition by neuropilin 2 and neutralizing antibodies. *Science Advances*, 8. (PDB `7M22`)
- Yu, F., Alesand, V., & Nygren, P. A. (2018). Site-specific photoconjugation of beta-lactamase fragments to monoclonal antibodies enables sensitive analyte detection via split-enzyme complementation. *Biotechnology Journal*, 13.
