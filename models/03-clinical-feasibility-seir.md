# Model 3: Clinical Feasibility & SEIR Viral Load Model

## Objective

Use **`SIR`/`SEIR` compartmental modeling** to measure the impact of cytomegalovirus on the infant and model viral load dynamics, mapping expected newborn saliva viral loads to target pentamer concentration thresholds and comparing them against the assay's measured **limit of detection (`LOD`)** to test whether a real infant sample will clear the detection threshold.

---

## Modeling Framework

### 1. `SIR` / `SEIR` Viral Load & Infection Dynamics in the Infant
- Models congenital CMV replication and target-cell dynamics in the infant using Susceptible-Infected-Recovered (`SIR`) and Susceptible-Exposed-Infected-Recovered (`SEIR`) compartmental differential equations:
  - Tracks susceptible host epithelial/endothelial target cells ($S$), latently or eclipse-phase exposed cells ($E$), productively infected virus-shedding cells ($I$), and cleared/refractory compartments ($R$).
  - Couples the productively infected compartment ($I$) to viral shedding into neonatal saliva to evaluate how viral load evolves over the perinatal screening window and how viral burden relates to clinical progression risk.

### 2. Mapping Newborn Saliva Viral Loads to Pentamer Concentration Thresholds
- Converts expected newborn saliva viral loads (viral particles / genome equivalents per mL of saliva) into molar concentrations of assembled surface pentameric complex (`gH/gL/UL128/UL130/UL131A`), accounting for sample collection volume and virion pre-concentration in the disposable cartridge.

### 3. Independent Clinical Feasibility Test Against Quantified `LOD`
- Independently evaluates assay viability by comparing the mapped newborn saliva pentamer concentrations directly against the analytical limit of detection (`LOD`) quantified in **Model 2** and **Experiment 5**.
- Determines whether a real cCMV-positive infant saliva specimen clears the detection threshold across each reader tier without DNA amplification:
  - If the nitrocefin colorimetric `LOD` on the `196/198` split construct is insufficient for the lower tail of newborn saliva viral loads, the feasibility model triggers the two engineering contingencies specified in the proposal:
    1. Replacing the `196/198` split site with a lower-background split site such as `63/64` (Marsh & Owen, 2025).
    2. Replacing colorimetric nitrocefin with the fluorogenic $\beta$-lactamase substrate `CCF2` (Galarneau et al., 2002) paired with the filtered-LED reader tier.
