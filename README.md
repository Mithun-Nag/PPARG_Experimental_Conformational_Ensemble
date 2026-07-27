# 🧬 PPARγ Experimental Conformational Ensemble

### Experimental PPARγ structural ensemble reconstruction and molecular dynamics relaxation

This repository contains the computational workflow used to construct an **experimentally derived conformational ensemble of the PPARγ ligand-binding domain (LBD)** from structures deposited in the Protein Data Bank (PDB).

As of **January 2026**, **368 PPARγ LBD crystal structures** were curated from the PDB. Individual PPARγ chains were extracted from these structures, yielding a dataset of **620 PPARγ conformations** spanning diverse crystallization conditions and structures determined in the absence or presence of **ligands and/or coregulator peptides**.

> **368 PDB structures → 620 PPARγ chains → missing-region reconstruction → energy minimization → 10 ns MD relaxation**

Regions lacking crystallographic electron density, including unresolved loops and occasionally **helix 12**, were reconstructed before simulation. The resulting structures were energy-minimized and subjected to **10 ns molecular dynamics (MD) simulations** to relax the reconstructed structures and generate a standardized experimental conformational ensemble for subsequent structural landscape analysis.

---

## 🔬 Workflow

The repository is organized into three main stages:

**1. PDB curation and chain extraction — Google Colab**
PPARγ LBD structures are curated from the PDB, individual PPARγ chains are identified and extracted, and peptides, solvent, hetero atoms, and other non-PPARγ molecules are removed.

**2. Missing-region reconstruction — MODELLER on ACCRE**
Missing crystallographic regions are reconstructed against the canonical PPARγ LBD sequence to produce complete structural models with consistent residue representation.

**3. Structural relaxation — AMBER on ACCRE**
Each reconstructed PPARγ structure is prepared, energy-minimized, and subjected to a **10 ns MD simulation** to relax the structure before conformational landscape analysis.

---

## 📂 Repository Structure

```text
PPARG_Experimental_Conformational_Ensemble/
│
├── README.md
│
├── PDB_Curation_Colab/
│   ├── 1_PPARG_PDB_Curation.ipynb
│   └── Data/
│       ├── PPARG_CHAINS_PDB_all.zip
│       ├── PPARG_chain_metadata.csv
│       └── pdb_files.csv
│
└── Modelling_and_Simulations_ACCRE/
    ├── 2_PPARg_Modeller.ipynb
    ├── 3_PPARg_620_Chains_10ns_Amber_Simulations.ipynb
    │
    └── Scripts/
        ├── tleap.in
        ├── molarity.perl
        │
        ├── Minimization/
        │   └── mesmy.sh
        │
        └── Production/
            ├── production.pl
            ├── prod1.in.start
            └── prod1.in
```

---

## 📊 Dataset

The curated experimental ensemble contains:

* **368** PPARγ LBD crystal structures available as of January 2026
* **620** individual PPARγ chains
* Structures representing diverse crystallographic conditions
* Apo and ligand-bound structures
* Structures determined with and without coregulator peptides
* Reconstructed unresolved regions followed by MD relaxation

The curated chain structures used by the downstream workflow are provided in:

`PDB_Curation_Colab/Data/PPARG_CHAINS_PDB_all.zip`

Associated PDB and chain-level information is provided in:

`PDB_Curation_Colab/Data/pdb_files.csv`
`PDB_Curation_Colab/Data/PPARG_chain_metadata.csv`

---

## 💻 Computational Environments

### Google Colab

PDB retrieval, curation, PPARγ chain identification, extraction, and dataset preparation are performed in **Google Colab**.

### ACCRE

Missing-region reconstruction and molecular dynamics simulations are performed on the **Advanced Computing Center for Research and Education (ACCRE)** high-performance computing environment.

Structural reconstruction uses **MODELLER**, followed by system preparation and molecular dynamics simulations using **AMBER**.

---

## 🎯 Purpose

The resulting ensemble provides an experimentally grounded collection of relaxed PPARγ LBD conformations that can be integrated with conventional and enhanced-sampling MD simulations to characterize the structural landscape connecting experimentally observed PPARγ conformational states.


## 🚀 Reproducing the Workflow

This repository contains the notebooks, curated structural dataset, metadata, and supporting scripts used to construct the PPARγ experimental conformational ensemble.

### 1️⃣ PDB Curation and PPARγ Chain Extraction — Google Colab

Run:

`PDB_Curation_Colab/1_PPARG_PDB_Curation.ipynb`

This notebook contains the **Google Colab workflow used to curate the experimental PPARγ LBD structural dataset**.

As of **January 2026**, **368 PPARγ LBD crystal structures** available in the Protein Data Bank (PDB) were collected and curated. Individual PPARγ chains were extracted, while peptides, solvent, hetero atoms, and other non-PPARγ molecules were removed. Sequence- and chain-level sanity checks were then used to verify the final dataset of **620 individual PPARγ chains**.

The outputs of this curation stage are provided in:

`PDB_Curation_Colab/Data/`

* **`pdb_files.csv`** — records the **368 PDB entries used in the analysis as of January 2026**.
* **`PPARG_chain_metadata.csv`** — provides the associated **chain-level metadata for the 620 curated PPARγ chains**.
* **`PPARG_CHAINS_PDB_all.zip`** — contains the **620 individually extracted and curated PPARγ chain PDB files**.

These files document the experimental structural dataset used in the analysis and provide the curated PPARγ structures required for downstream processing. Users can transfer `PPARG_CHAINS_PDB_all.zip` directly to **ACCRE or another compatible computing environment**, extract the PDB files, and proceed with the modelling stage without repeating the curation workflow.

---

### 2️⃣ Reconstruction of Missing Loops — MODELLER on ACCRE

Run:

`Modelling_and_Simulations_ACCRE/2_PPARg_Modeller.ipynb`

This notebook contains the **MODELLER workflow used to reconstruct missing loops** in the curated PPARγ crystal structures using the canonical PPARγ LBD sequence.

The resulting models are used as the input structures for the subsequent AMBER simulation workflow.

---

### 3️⃣ Energy Minimization and 10 ns MD Relaxation — AMBER on ACCRE

Run:

`Modelling_and_Simulations_ACCRE/3_PPARg_620_Chains_10ns_Amber_Simulations.ipynb`

This notebook contains the **AMBER workflow used to prepare, minimize, and relax the reconstructed PPARγ structures**.

Each structure is prepared for simulation, energy-minimized, and subjected to a **10 ns molecular dynamics simulation**.

Supporting AMBER input and execution files are provided under:

`Modelling_and_Simulations_ACCRE/Scripts/`

including the system-preparation, minimization, and production simulation scripts used by the notebook.

---

## 🔄 Workflow Summary

**368 PPARγ LBD PDB entries as of January 2026**
↓
**620 curated PPARγ chains**
↓
**Missing-loop reconstruction with MODELLER**
↓
**AMBER system preparation and energy minimization**
↓
**10 ns MD relaxation**
↓
**Relaxed experimental PPARγ conformational ensemble**


🛠️ Software and Computational Requirements

The workflow was developed using the following software and computing environments:

Google Colab — PDB curation, chain extraction, and dataset preparation
ProDy — structural parsing and manipulation during PDB curation
MODELLER — reconstruction of missing loops
AMBER — system preparation, energy minimization, and 10 ns molecular dynamics simulations
ACCRE — high-performance computing environment used for MODELLER and AMBER calculations
Python / Jupyter Notebook — workflow execution, data processing, and analysis

The notebooks contain the environment setup, software installation, and execution commands used for each stage of the workflow.
