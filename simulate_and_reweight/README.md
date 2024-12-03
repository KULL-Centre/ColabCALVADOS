# Instructions

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb)

This [Jupyter Notebook](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb) is designed to run molecular dynamics (MD) simulations of intrinsically disordered proteins (IDPs) and multi-domain proteins (MDPs), and integrate simulations with small-angle X-ray scattering (SAXS) data. Simulations are performed using CALVADOS, an implicit-solvent coarse-grained model. Bayesian/Maximum-Entropy reweighting is used to
refine against SAXS data the conformational ensemble of the IDP or MDP of study.

## Getting Started

1. Open the following link (Google Chrome is required for everything to work properly) [CALVADOS_simulate_and_reweight.ipynb](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/simulate_and_reweight/CALVADOS_simulate_and_reweight.ipynb)
2. Ensure GPUs are enabled: Navigate to `Runtime > Change runtime type`, select `T4 GPU`, and click `Save`. 
3. Run "1. Set the environment for simulation". After running this cell, you will notice a prompt informing you that "Your session crashed for an unknown reason". This is required for all packages to work properly. Ignore it and move on to the next step.
4. In "2. Configure your protein", input the protein name, sequence, temperature, ionic strength, pH, and domain boundary. You can find those information in [data/SAXS/exp_conditions.csv](https://github.com/KULL-Centre/ColabCALVADOS/blob/main/data/SAXS/exp_conditions.csv) for 13 IDPs and 13 MDPs (see DOI: 10.1016/j.bpj.2022.12.013, 10.1002/pro.5172). In [data/SAXS](https://github.com/KULL-Centre/ColabCALVADOS/tree/main/data/SAXS) you will also find structure files (`.pdb` for 13 MDPs) and SAXS data files (`.dat`). Choose the protein you want to work with and download its `.pdb` file (for MDPs) and SAXS curve (`.dat` file). You can also use your own data for the protein of your choice. By checking `example`, all the inputs in fields will be ignored and the MDP Ubq4 will serve as an example with pre-defined settings.

*Tip: To download files from GitHub, open the file and click on the download button. If this button is not present (it is not if you are not logged in with a GitHub account), click on “Raw” and then “File>Save page as…” from Chrome’s menu.*

## Uploading PDB structure and SAXS curve

5. If you are simulating a MDP, please run "3. Upload a PDB file for MDPs" and upload your pdb file. **Skip** this cell if your protein is an IDP. The residues in the PDB file need to be listed in the same order as they appear in the protein sequence. This ensures the PDB file is consistent with the definition of the folded domains. 
6. Run "4. Upload SAXS data" to upload the SAXS data file. The unit will be automatically detected, and converted if necessary.

## Setting up and running an MD simulation

7. In "5. Set force field and simulation time", the default option “AUTO” will set the simulation time depending on sequence length. The longer the IDR, the more heterogeneous the ensemble of conformations it can adopt. Moreover, the reconfiguration time of IDRs increases with increasing sequence length. Therefore, longer sequences will require more sampling. Typical simulation times range from ca. 5 min (a 71-ns-long simulation of an IDR of 70 residues), 7 min (71-ns-long simulation of an IDR of 140 residues), to 34 min for a 373-ns-long simulation of an IDR of 351 residues.<br>
The option "Break_CALVADOS" adds random noise to the amino acid stickiness parameters of the CALVADOS model (λ values). The resulting simulations will not be trustworthy. This function is added for teaching purposes, so that the effect of reweighting could be appreciated more when using a force field that does not reproduce experimental data accurately. 
8. Run the subsequent three cells one by one to import relevant modules.
9. Start simulations by running "6. Run MD simulation".

## Analyses and visualization

10. Run "Install Pepsi-SAXS and download BLOCKING, BME, and BIFT" to install necessary packages for reweighting.
11. "7. Analysis" plots the distributions and averages of some structural parameters: radius of gyration, R<sub>g</sub>; end-to-end distance, R<sub>ee</sub>; contact map between residues and apparent Flory scaling exponent, ν (only for IDPs). ν is calculated from a nonlinear fit to the ensemble-averaged inter-residue distances, &#8730;&#9001;R<sup>2</sup><sub>ij</sub>&#9002;, as a function of sequence separations, |i-j|.
12. "8. Visualize trajectory" will visualize your protein. You can rotate the protein or zoom in/out.

## Backmapping, BME reweighting, and downloading output

13. "Install `cg2all` for all-atom reconstruction (will take ~5 mins)" will install `cg2all` package to reconstruct the All-atom trajectory.
14. Run "Reconstruct all-atom trajectory" to Reconstruct all-atom trajectory.
15. In "9. Ensemble reweighting against experimental data", the Bayesian/Maximum-Entropy approach is used to reweight the MD simulations so that it better matches the SAXS data. This is done by minimizing the function<br>
$L(w_1 ... w_n) = \frac{m}{2}\chi^2(w_1 ... w_n)-\theta \times S_{rel}(w_1 ... w_n)$,<br>
where $(w_1 ... w_n)$ are the statistical weights associated with each frame of the simulation.<br>
$\chi^2(w_1...w_n)=\frac{1}{m}\sum_i^m\frac{(\sum_j^nw_jI_j^{CALC}(q_i)-I^{EXP}(q_i))^2}{\sigma(q_i)^2}$<br>
quantifies the agreement between simulation and SAXS, where $\sigma(q_i)$ is the error on the experimental SAXS intensities, $I^{EXP}(q)$.<br>
$-S_{rel}(w_1...w_n)=\sum_j^nw_j\ln(\frac{w_j}{w_j^0})=\sum_j^nw_j\ln(w_j\times n)$<br>
quantifies how much the new weights are different from the initial ones.<br> 
$\theta$ is a free parameter that must be tuned to strike a balance between obtaining a good agreement with the experimental data (low $\chi^2$) and retaining as much information as possible from the starting simulation (high $S_{rel}$).<br> 
We do two types of calculation in this cell:
    1. We calculate SAXS curves for each trajectory frame using Pepsi-SAXS.
    2. We execute BME reweighing using different $\theta$ values. For each $\theta$ value, we calculate $\chi^2$ and $\phi_{eff}=\exp(S_{rel})$.
16. In "Setting θ", you will scan θ and for each value plot $\chi^2$ vs $\phi_{eff}=\exp(S_{rel})$. A good value of θ is located at the elbow of the curve. After switching the “THETA_LOCATOR” option from “AUTO” to “INTERACTIVE”, and running the cell once more, you can select a θ value of your choice from the drop-down menu.
17. In "10. Analyze reweighted ensemble", This cell shows comparisons between SAXS curves and conformational properties from <font color='#808080'>experiments (grey) </font> and from the simulation trajectory <font color='#058ED9'>before (blue) </font> and after BME <font color='#d42828'>reweighting (red) </font>. As an exercise, go back to cell 5 and check the "Break_CALVADOS" box. That will add random noise to the amino acid stickiness parameters of the CALVADOS model ($\lambda$ values). The resulting force field will likely not reproduce the experimental data accurately and the effect of reweighting will be more evident. 
18. In "11. Download results", you can download all the relevant files:

    `${protein_name}_cg.dcd`: the coarse-grained trajectory file;

    `${protein_name}_cg.pdb`: the coarse-grained topology file;
    
    After reconstruction
    
    `$traj_AA.dcd`: the reconstructed trajectory file;
    
    `$top_AA.pdb`: the all-atom topology file;
    
    Plots and analyses
    
    `${protein_name}/analyses/conformational_properties.pdf`;
    
    `${protein_name}/analyses/conf_properties.csv`;
    
    `${protein_name}/analyses/contact_map.csv`;
    
    `${protein_name}/analyses/calc_saxs.dat`;
    
    `${protein_name}/analyses/reweighted_calc_saxs.dat`;
    
    `${protein_name}/analyses/saxs_reweighted_conf_prop.pdf`;

## Dependencies

The file `environment.yaml` contains a complete list of the conda and PyPI packages installed on Google Colab in Nov 26 2024.

## Authors

[Fan Cao (@fancaoErik)](https://github.com/fancaoErik)

[Francesco Pesce (@FrPsc)](https://github.com/FrPsc)

[Giulio Tesei (@gitesei)](https://github.com/gitesei)

[Kresten Lindorff-Larsen (@lindorff-larsen)](https://github.com/lindorff-larsen)

