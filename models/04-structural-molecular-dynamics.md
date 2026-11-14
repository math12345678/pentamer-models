# Model 4: Structural Co-Binding & GROMACS Molecular Dynamics Model

## Objective

Construct three-dimensional structural models of the sensor complex from PDB entries [`5VOB`](https://www.rcsb.org/structure/5VOB), [`7T4S`](https://www.rcsb.org/structure/7T4S), and [`7M22`](https://www.rcsb.org/structure/7M22) and run all-atom molecular dynamics simulations in **`GROMACS`** to evaluate co-binding geometry, split-enzyme orientation, and flexible dynamics on the pentamer framework, calculating:
- **Root mean square deviation (`RMSD`)**
- **Root mean square fluctuation (`RMSF`)**
- **Centrality measures: `betweenness`, `eigenvector`, and `connectedness` centralities**
- **Solvent-accessible surface area (`SASA`)**
- **Radius of gyration ($R_g$)**

---

## Structural Foundations (PDB Entries)

1. **[`5VOB`](https://www.rcsb.org/structure/5VOB)** (*Chandramouli et al., 2017*): Crystal structure of the assembled HCMV `gH/gL/UL128/UL130/UL131A` pentameric complex, providing baseline atomic coordinates for the five-subunit antigen scaffold.
2. **[`7T4S`](https://www.rcsb.org/structure/7T4S)** (*Kschonsak et al., 2022*): Structure of the HCMV pentamer bound to neutralizing antibodies including `8I21` and `13H11`, defining the exact non-overlapping binding epitopes and inter-paratope geometry on the assembled complex.
3. **[`7M22`](https://www.rcsb.org/structure/7M22)** (*Wrapp et al., 2022*): Structure of the HCMV pentamer in complex with its host cellular receptor neuropilin-2 (`NRP2`) and neutralizing antibodies, enabling structural evaluation of `NRP2` receptor competition in **Experiment 4** and subunit specificity in **Experiment 3**.

From these coordinates, `8I21` and `13H11` are modeled as single-chain variable fragments (scFvs) connected via flexible glycine-serine linkers to the N-terminal (`1-196`) and C-terminal (`198-286`) fragments of `TEM-1` $\beta$-lactamase.

---

## GROMACS Simulation & Trajectory Readouts

All-atom explicit-solvent molecular dynamics simulations are executed in **`GROMACS`** to evaluate whether both scFv fusion arms can simultaneously bind the pentamer and bring the split `TEM-1` $\beta$-lactamase halves into a productive reconstitution orientation without steric clash:

1. **Root Mean Square Deviation (`RMSD`)**:
   - Tracks backbone conformational equilibration and global stability of the assembled pentamer core (`gH/gL/UL128/UL130/UL131A`), the bound `8I21` and `13H11` scFv domains, and the reconstituted `TEM-1` $\beta$-lactamase interface over simulation time.
2. **Root Mean Square Fluctuation (`RMSF`)**:
   - Quantifies per-residue flexibility across the five pentamer subunits, the antibody complementarity-determining regions (CDRs), the flexible glycine-serine linkers, and the `196/198` split-enzyme loop interface.
3. **Residue Network Centralities (`Betweenness`, `Eigenvector`, and `Connectedness` Centralities)**:
   - Constructs dynamic residue contact networks across the `GROMACS` trajectory to compute:
     - **Betweenness centrality**: Identifies key bridging residues along communication pathways between the `8I21`/`13H11` paratope-epitope interfaces and the split-enzyme complementation interface.
     - **Eigenvector centrality**: Measures residue influence within highly connected structural hubs of the pentamer-scFv complex.
     - **Connectedness centrality**: Quantifies local and global contact connectivity across the `UL128/UL130/UL131A` apex and `gH/gL` scaffold during dual-scFv engagement.
4. **Solvent-Accessible Surface Area (`SASA`)**:
   - Measures buried surface area at the `8I21`-pentamer, `13H11`-pentamer, and reconstituted `TEM-1` fragment interfaces, as well as active-site accessibility for nitrocefin entry.
5. **Radius of Gyration ($R_g$)**:
   - Evaluates overall compactness of the ternary sensor complex and conformational extension of the glycine-serine linkers bridging the bound scFv arms to the split `TEM-1` halves.

---

## Coupling to Wet-Lab Validation

- **Experiment 3**: Evaluates specificity against `gH/gL` dimers and `gH/gL/gO` trimers lacking pentamer-specific subunits (`UL128/UL130/UL131A`).
- **Experiment 4**: Assesses binding site structure through receptor competition assays using soluble neuropilin-2 (`NRP2`, PDB `7M22`).
