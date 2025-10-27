# scDenorm_reproducibility

## Overview

This repository contains Jupyter notebooks to reproduce the analyses presented in the manuscript **"scDenorm: a denormalisation tool for Integrating Single-cell Transcriptomics Data."**

## Tutorial of running notebooks
- 1.download notebooks
- 2.download docker and data
- 3.move data to scDenorm_reproducibility/data folder
- 4.run docker image

## Notebooks

The repository includes the following notebooks:

- `Fig1.ipynb`: Analysis for Figure 1
- `Fig2.ipynb`: Analysis for Figure 2
- `Fig3.ipynb`: Analysis for Figure 3
- `Fig4.ipynb`: Analysis for Figure 4
- `Fig5.ipynb`: Analysis for Figure 5
- `Fig6.ipynb`: Analysis for Figure 6
- `Fig7.ipynb`: Analysis for Figure 7

## Environment configurations
- `Python=3.2`: config/environment.yaml
- `R=4.0.2`: config/installed_packages.csv


## How to use and install scDenorm
- Install: pip install scDenorm
- Usage: scdenorm data/pbmc3k_norm.h5ad --fout data/pbmc3k_denorm.h5ad
- Documentation: https://changebio.github.io/scDenorm

## Citation
Yin Huang, Anna Vathrakokili Pournara, Ying Ao, Hui Zhang, Yongjian Zhang, Sheng Liu, Alvis Brazma, Irene Papatheodorou, Xinlu Yang, Ming Shi, Zhichao Miao “scDenorm: a denormalisation tool for integrating single-cell transcriptomics data”(Under review)

For any questions or issues, please open an issue in the repository. 
