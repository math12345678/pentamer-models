# Model 1: Kinetic Sensor & Split-Enzyme Complementation Model

## Objective

Model the binding of both neutralizing antibody single-chain variable fragments (`8I21` and `13H11`) to the assembled HCMV epithelial-entry pentamer complex (`gH/gL/UL128/UL130/UL131A`) and apply **Michaelis-Menten enzyme kinetics** to the reconstituted split `TEM-1` $\beta$-lactamase enzyme to predict signal output, optimal scFv working concentrations, and background tolerance.

---

## Biological & Biochemical Mechanism

1. **Dual-Epitope Target Recognition**:
   - The HCMV pentameric complex (`gH/gL/UL128/UL130/UL131A`) mediates viral entry into human epithelial and endothelial cells.
   - The sensor uses two single-chain variable fragments (`8I21-scFv` and `13H11-scFv`) that bind non-overlapping epitopes on the assembled complex (Kschonsak et al., 2022).
2. **Proximity-Induced Split-Enzyme Reconstitution**:
   - Each scFv arm is fused via a flexible glycine-serine linker to one half of `TEM-1` $\beta$-lactamase split between residues `196` and `198` (Marsh & Owen, 2025).
   - Neither fragment exhibits enzymatic activity alone. When both scFv arms bind to the same assembled pentamer complex, the two halves are held in proximity and refold into an active `TEM-1` $\beta$-lactamase enzyme.
3. **Michaelis-Menten Substrate Turnover**:
   - The reconstituted enzyme catalyzes hydrolysis of the chromogenic cephalosporin substrate **nitrocefin**, producing a visible yellow-to-red shift measured at `486 nm`.
   - Substrate cleavage follows Michaelis-Menten kinetics:
     $$v = \frac{V_{\max}[S]}{K_m + [S]} = \frac{k_{\text{cat}}[E_{\text{active}}][S]}{K_m + [S]}$$
     where $[S]$ is the nitrocefin concentration and $[E_{\text{active}}]$ is the concentration of reconstituted `TEM-1` $\beta$-lactamase formed on the pentamer complex.

---

## Modeling Tasks & Predictions

### 1. Predicting Signal Output Across Pentamer & Substrate Concentrations
- Couples the reversible binding of `8I21-scFv` and `13H11-scFv` on the epithelial-entry pentamer complex with Michaelis-Menten turnover of nitrocefin at `486 nm` (or fluorogenic `CCF2` turnover in the advanced reader tier).
- Predicts absorbance velocity curves over time as a function of assembled pentamer concentration.

### 2. Optimizing `8I21` and `13H11` scFv Working Concentrations
- At low scFv concentrations, insufficient pentamer complexes are doubly occupied by both `8I21` and `13H11`, limiting active enzyme formation and signal velocity.
- At excessively high scFv concentrations, unbound split fragments can undergo concentration-dependent spontaneous complementation in solution without antigen, raising the baseline background rate.
- The model sweeps `[8I21-scFv]` and `[13H11-scFv]` concentrations to identify the optimal working window that achieves the target **$\ge 10$-fold signal over either part of the dual scFv system alone** (at the conservative end of the 10- to 250-fold range reported for split `TEM-1` $\beta$-lactamase *in vitro*; Galarneau et al., 2002).

### 3. Quantifying Background Tolerance & Split-Site Selection
- Evaluates two distinct sources of background nitrocefin cleavage:
  1. **Spontaneous split-fragment reassembly**: Unassisted complementation of the `196/198` split `TEM-1` halves in the absence of pentamer (calibrated against Mock-Virion **Experiment 1**, testing individual and paired scFv arms without antigen).
  2. **Endogenous oral bacterial $\beta$-lactamase activity**: Background hydrolysis present in unfiltered saliva relative to $0.2\,\mu\text{m}$-filtered saliva and corrected via the dual-chamber reference cartridge (calibrated against Mock-Virion **Experiment 6**).
- Establishes quantitative thresholds for deciding when background signal requires replacing the `196/198` split site with a lower-background split site such as `63/64` (Marsh & Owen, 2025) or replacing nitrocefin with the fluorogenic $\beta$-lactamase substrate `CCF2` (Galarneau et al., 2002).

---

## Experimental Validation

- **Experiment 1**: Measures baseline signal from individual scFv fusion arms alone without antigen.
- **Experiment 2**: Measures enzyme complementation velocity when placing both `8I21` and `13H11` scFv fusions simultaneously with pentamer-coated nickel-charged beads in synthetic saliva.
- **Experiment 6**: Compares filtered saliva against unfiltered saliva to parameterize background interference from bacterial $\beta$-lactamases.
