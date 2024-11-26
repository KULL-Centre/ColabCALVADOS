# ColabCALVADOS

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb)

This repository contains Jupyter Notebooks to investigate the conformational properties of intrinsically disordered regions (IDRs) and multi-domain proteins (MDPs) through molecular dynamics (MD) simulations on Google Colaboratory. Simulations are performed using CALVADOS, an implicit-solvent coarse-grained model. The notebook `CALVADOS_simulate_and_reweight.ipynb` also integrates simulations with experimental small-angle X-ray scattering (SAXS) data, applying Bayesian/Maximum-Entropy reweighting to refine the conformational ensemble of the protein of study.

## Getting Started

1. **Browse the Data**
   Visit the [data/SAXS](https://github.com/KULL-Centre/ColabCALVADOS/tree/main/data/SAXS) folder to find example sequences and SAXS data for several IDRs and MDPs.
   - Select a protein and download its corresponding SAXS data file (`.dat`).
   - Alternatively, you can analyze a protein of your choice by providing your own sequence and SAXS data files.

2. **Access the Notebook**
   The lab exercise is conducted using a Jupyter Notebook hosted on Google Colab. You will need a Google account and preferably Google Chrome to work with the notebook.

3. **Open the Notebook**
   To access the notebook, click the **"Open in Colab"** badge below:

   [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb)

## Authors

[Fan Cao (@fancaoErik)](https://github.com/fancaoErik)

[Francesco Pesce (@FrPsc)](https://github.com/FrPsc)

[Giulio Tesei (@gitesei)](https://github.com/gitesei)

[Kresten Lindorff-Larsen (@lindorff-larsen)](https://github.com/lindorff-larsen)

