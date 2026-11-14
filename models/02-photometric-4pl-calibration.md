# Model 2: Photometric 4PL Calibration & Hook-Effect Model

## Objective

Fit a **four-parameter logistic (`4PL`) sigmoid curve** to optical signal against pentamer concentration to define the exact analytical **limit of detection (`LOD`)** and detect potential **high-dose hook effects**.

---

## Signal Processing & Calibration Framework

### 1. Reader Signal Acquisition & Drift Rejection
- Across the three open-source hardware reader tiers, optical measurements of nitrocefin cleavage (`486 nm`) or fluorogenic `CCF2` turnover are converted into background-corrected reaction rates:
  - **Baseline tier**: 3D-printed dark box with smartphone camera and color reference card normalization.
  - **Mid-tier unit**: `ESP32` microcontroller paired with an LED source and photodiode detector. The `ESP32` switches the LED on and off rapidly and reads the photodiode signal synchronously at that switching frequency, rejecting ambient room light and low-frequency sensor drift.
  - **Advanced tier**: Filtered-LED fluorescence reader paired with a disposable cartridge containing a secondary reaction chamber that subtracts background bacterial $\beta$-lactamase activity.

### 2. Four-Parameter Logistic (`4PL`) Sigmoid Curve Fitting
- Across serial mock-virion titration standards, optical response is modeled with a four-parameter logistic (`4PL`) curve:
  $$y(x) = d + \frac{a - d}{1 + (x / c)^b}$$
  where:
  - $x$ is the target pentamer concentration,
  - $a$ is the lower asymptote (zero-antigen baseline),
  - $d$ is the upper asymptote (saturated complementation response),
  - $c$ is the inflection point ($\text{EC}_{50}$), and
  - $b$ is the Hill slope governing the steepness of the sigmoid transition.

### 3. Defining the Analytical Limit of Detection (`LOD`)
- Using the zero-antigen baseline variance from **Experiment 1** and serial titration curves from **Experiment 5**, the model computes the minimum distinguishable optical signal above background noise and inverts the fitted `4PL` sigmoid curve to determine the exact analytical limit of detection (`LOD`) for each hardware reader tier.

### 4. Detecting High-Dose Hook (Prozone) Effects
- Because PENTA(mer) is a homogeneous, wash-free ternary sandwich assay (`8I21-scFv` + `Pentamer` + `13H11-scFv`), extreme antigen excess (`[Pentamer] >> [scFv]`) can cause `8I21-scFv` and `13H11-scFv` to bind separate pentamer complexes rather than co-occupying the same complex.
- This partitioning reduces the concentration of doubly bound ternary complexes at very high viral loads, causing the dose-response curve to hook downward after peaking.
- The calibration software monitors the initial kinetic cleavage rate alongside the endpoint `4PL` curve to flag high-dose hook regimes and prevent false-low concentration readouts at elevated antigen levels.

---

## Experimental Validation

- **Experiment 5**: Establishes sample concentration and serial titration protocols using pentamer-coated beads in synthetic saliva to parameterize the `4PL` sigmoid curve and quantify the analytical `LOD`.
- **Experiment 6**: Evaluates dual-chamber background subtraction between filtered and unfiltered saliva.
