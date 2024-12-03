# Instructions

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate/CALVADOS_simulate.ipynb)

This [Jupyter Notebook](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate/CALVADOS_simulate.ipynb) is designed to run molecular dynamics (MD) simulations of intrinsically disordered proteins (IDPs) and multi-domain proteins (MDPs) using CALVADOS, an implicit-solvent coarse-grained model. 

## Getting Started

1. Open the following link (Google Chrome is required for everything to work properly) [CALVADOS_simulate.ipynb](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate/CALVADOS_simulate.ipynb)
2. Ensure GPUs are enabled: Navigate to `Runtime > Change runtime type`, select `T4 GPU`, and click `Save`. 
3. Run "1. Set the environment for simulation". After running this cell, you will notice a prompt informing you that "Your session crashed for an unknown reason". This is required for all packages to work properly. Ignore it and move on to the next step.
4. In "2. Configure your protein", input the protein name, sequence, temperature, ionic strength, pH, and domain boundary. You can find those information in [data/SAXS/exp_conditions.csv](https://github.com/KULL-Centre/ColabCALVADOS/blob/main/data/SAXS/exp_conditions.csv) for 13 IDPs and 13 MDPs (see DOI: 10.1016/j.bpj.2022.12.013, 10.1002/pro.5172). In [data/SAXS](https://github.com/KULL-Centre/ColabCALVADOS/tree/main/data/SAXS) you will also find structure files (`.pdb`) for 13 MDPs. Choose the protein you want to work with and download its `.pdb` file. You can also use your own PDB for the protein of your choice. By checking `example`, all the inputs in fields will be ignored and the MDP Ubq4 will serve as an example with pre-defined settings.

*Tip: To download files from GitHub, open the file and click on the download button. If this button is not present (it is not if you are not logged in with a GitHub account), click on “Raw” and then `File>Save page as…` from Chrome’s menu.*

## Uploading PDB structure and SAXS curve

5. If you are simulating a MDP, please run "3. Upload a PDB file for MDPs" and upload your pdb file. **Skip** this cell if your protein is an IDP. The residues in the PDB file need to be listed in the same order as they appear in the protein sequence. This ensures the PDB file is consistent with the definition of the folded domains. 

## Setting up and running an MD simulation

6. In "4. Set force field and simulation time", the default option “AUTO” will set the simulation time depending on sequence length. The longer the IDR, the more heterogeneous the ensemble of conformations it can adopt. Moreover, the reconfiguration time of IDRs increases with increasing sequence length. Therefore, longer sequences will require more sampling. Typical simulation times range from ca. 5 min (a 71-ns-long simulation of an IDR of 70 residues), 7 min (71-ns-long simulation of an IDR of 140 residues), to 34 min for a 373-ns-long simulation of an IDR of 351 residues.
7. Run the subsequent three cells one by one to import relevant modules.
8. Start simulations by running "5. Run MD simulation".

## Analyses and visualization

9. "6. Analysis" plots the distributions and averages of some structural parameters: radius of gyration, R<sub>g</sub>; end-to-end distance, R<sub>ee</sub>; contact map between residues and apparent Flory scaling exponent, ν (only for IDPs). ν is calculated from a nonlinear fit to the ensemble-averaged inter-residue distances, &#8730;&#9001;R<sup>2</sup><sub>ij</sub>&#9002;, as a function of sequence separations, |i-j|.
10. "7. Visualize trajectory" will visualize your protein. You can rotate the protein or zoom in/out.

## Backmapping and downloading output

11. "Install `cg2all` for all-atom reconstruction (will take ~5 mins)" will install `cg2all` package to reconstruct the All-atom trajectory.
12. Run "Reconstruct all-atom trajectory" to Reconstruct all-atom trajectory.
13. In "8. Download results", you can download all the relevant files:

    `${protein_name}_cg.dcd`: the coarse-grained trajectory file;

    `${protein_name}_cg.pdb`: the coarse-grained topology file;
    
    After reconstruction
    
    `$traj_AA.dcd`: the reconstructed trajectory file;
    
    `$top_AA.pdb`: the all-atom topology file;
    
    Plots and analyses
    
    `${protein_name}/analyses/conformational_properties.pdf`;
    
    `${protein_name}/analyses/conf_properties.csv`;
    
    `${protein_name}/analyses/contact_map.csv`;
    
## Dependencies

The file `environment.yaml` contains a complete list of the conda and PyPI packages installed on Google Colab in Nov 26 2024.

## Authors

[Fan Cao (@fancaoErik)](https://github.com/fancaoErik)

[Francesco Pesce (@FrPsc)](https://github.com/FrPsc)

[Giulio Tesei (@gitesei)](https://github.com/gitesei)

[Kresten Lindorff-Larsen (@lindorff-larsen)](https://github.com/lindorff-larsen)

