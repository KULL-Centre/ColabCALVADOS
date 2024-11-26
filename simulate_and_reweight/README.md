# Instructions

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb)

This [Jupyter Notebook](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb) to run molecular dynamics (MD) simulations of intrinsically disordered regions (IDRs) and integrate simulations with small-angle X-ray scattering (SAXS) data. Simulations are performed using CALVADOS, an implicit-solvent coarse-grained model. 
The notebook `CALVADOS_simulate_and_reweight.ipynb` integrates simulations with experimental small-angle X-ray scattering (SAXS) data by applying Bayesian/Maximum-Entropy reweighting to refine the conformational ensemble of the protein of study.

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

4. Make sure to have GPUs enabled: go to `Runtime`, select `Change runtime type`, and select `GPU`.

5. Choose the IDP you want to work with and download its sequence (“.fasta” file) and SAXS data (“.dat” file). Otherwise, you can use your own data. To download files from GitHub, open the file and click on the download button (see image below). If this button is not present (it is not if you are not logged in with a GitHub account), click on “Raw” and then “File>Save page as...” from Chrome’s menu.

The Bayesian/Maximum-Entropy approach is used to reweight the MD simulations so that it better matches the SAXS data. This is done by minimizing the functional, $L(w_1 ... w_n) = \frac{m}{2}\chi^2(w_1 ... w_n)-\theta\; S_{rel}(w_1 ... w_n)$, where $(w_1 ... w_n)$ are the statistical ibme_weights associated with each frame of the simulation, $\chi^2$ quantifies the agreement between simulation and SAXS, $S_{rel}$ quantifies how much the new ibme_weights are different from the initial ones. $\theta$ is a free parameter that must be tuned to strike a balance between obtaining a good agreement with the experimental data (low $\chi^2$) and retaining as much information as possible from the starting simulation (high $S_{rel}$).

## Dependencies

The file `environment.yaml` contains a complete list of the conda and PIPy packages installed on Google Colab in Nov 26 2024.

## Authors

[Fan Cao (@fancaoErik)](https://github.com/fancaoErik)

[Francesco Pesce (@FrPsc)](https://github.com/FrPsc)

[Giulio Tesei (@gitesei)](https://github.com/gitesei)

[Kresten Lindorff-Larsen (@lindorff-larsen)](https://github.com/lindorff-larsen)

