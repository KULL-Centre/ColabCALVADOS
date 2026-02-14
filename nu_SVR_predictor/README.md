# Instructions

[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/nu_SVR_predictor/nu_SVR_predictor.ipynb)

This [Jupyter Notebook](https://colab.research.google.com/github/KULL-Centre/ColabCALVADOS/blob/main/nu_SVR_predictor/nu_SVR_predictor.ipynb) illustrates how a database of apparent scaling exponents, $\nu$, for human IDRs can be used to develop a support vector regression (SVR) predictor of IDR compaction [1].

The notebook explores how the regularization parameter $C$ affects model accuracy and transferability. Train the model using $C = 1$, $100$, and $1000$. Which values lead to underfitting or overfitting?

Permutation feature importance is used to quantify the relative contribution of the input sequence features to model performance. After training the model for a given value of $C$, run the next cell to inspect how the permutation feature importances change.

## References


