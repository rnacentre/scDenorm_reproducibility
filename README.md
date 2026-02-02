# scDenorm_reproducibility

## Overview

This repository contains Jupyter notebooks to reproduce the analyses presented in the manuscript **"scDenorm: a denormalisation tool for Integrating Single-cell Transcriptomics Data."**

## Tutorial for Running Notebooks

1. **Download the Notebooks**: Clone or download this repository from GitHub: [scDenorm GitHub Repository](https://github.com/rnacentre/scDenorm_reproducibility.git) or from Zenodo: [scDenorm Data](https://zenodo.org/records/17275776).
2. **Download and install Docker and Jupyter**: Follow the instructions for installation: [Docker Get Started](https://docs.docker.com/get-started/).
3. **Download Data**: 
   - Download the data file from Zenodo: [scDenorm Data](https://zenodo.org/records/17275776).
   - Unzip the downloaded data and place the relevant files into the `scDenorm_reproducibility/data` folder.
4. **Run Docker Image**: 
   - Ensure Docker is running.
   - Load the Docker image directly from the `.tar.gz` file:
     ```bash
     docker load < scdenorm_v0.tar.gz
     ```
     or
     ```bash
     tar -xzf scdenorm_v0.tar.gz
     docker load -i scdenorm_v0.tar
     ```
   - Run the Docker container with the following command (update the local path accordingly):
     ```bash
     docker run --platform linux/amd64 \
     -p 8888:8888 \
     -v /path/to/scDenorm_reproducibility/data:/app \
     scdenorm_v0 \
     jupyter lab --ip=0.0.0.0 --no-browser --allow-root
     ```
   - **Note**: Ensure to share the project folder with Docker. Go to Docker → Preferences → Resources → File Sharing and add the local project path.

### Example running `Fig5.ipynb`
1. Open `Fig5.ipynb`.
2. **Select** Kernel > Change Kernel > Python [conda env: sc].
3. Data Import: Copy the data from Zenodo into `scDenorm_reproducibility/data`, including:
   - `fig5_input.h5ad`
   - `PBMC_before_scDenorm.h5ad`
   - `PBMC_after_scDenorm.h5ad`
   - `PBMC_groundgo.csv`
   - `PBMC_beforego.csv`
   - `PBMC_aftergo.csv`
4. Run the notebook cells in order.

### Example running `Fig5_R_goanalysis.ipynb`
1. Open `Fig5_R_goanalysis.ipynb`.
2. **Select** Kernel > Change Kernel > R [conda env: sc].
3. Data Import: Copy the data from Zenodo into `scDenorm_reproducibility/data`, including:
   - `PBMC_raw_count_b0_deg.csv`
   - `PBMC_raw_count_b1_deg.csv`
   - `PBMC_normlized_data_1e3_b1_deg.csv`
4. Run the notebook cells in order.

## Notebooks

The repository includes the following notebooks:

- `Fig1.ipynb`: Analysis for Figure 1
- `Fig2.ipynb`: Analysis for Figure 2
- `Fig3.ipynb`: Analysis for Figure 3
- `Fig4.ipynb`: Analysis for Figure 4
- `Fig5.ipynb`: Analysis for Figure 5
- `Fig6.ipynb`: Analysis for Figure 6
- `Fig7.ipynb`: Analysis for Figure 7

## Environment Configurations on local computer

- **Python**: 
  - Environment file: `config/environment.yaml`
  - To create a Conda environment using the specifications in the environment.yaml file:
    ```bash
    conda env create -f environment.yaml
    ```
- **R**: 
  - Installed packages: `config/installed_packages.csv`
  - To install necessary R packages, run the following in the R terminal:
    ```R
    pkg_list <- read.csv("installed_packages.csv", stringsAsFactors = FALSE)
    for (pkg in pkg_list$Package) {
      if (!requireNamespace(pkg, quietly = TRUE)) {
        message(" Installing the package: ", pkg)
        install.packages(pkg, dependencies = TRUE)
      }
    }
    ```

## How to Use and Install scDenorm
- Documentation: https://changebio.github.io/scDenorm
- **Install**: 
  - Using pip: 
    ```bash
    pip install scDenorm
    ```
  
- **Usage**: 
  ```bash
  scdenorm data/pbmc3k_norm.h5ad --fout data/pbmc3k_denorm.h5ad
  ```

## Citation
Yin Huang, Anna Vathrakokili Pournara, Ying Ao, Ziliang Huang, Hui Zhang, Yongjian Zhang, Sheng Liu, Alvis Brazma, Irene Papatheodorou, Xinlu Yang, Ming Shi, Zhichao Miao “scDenorm: a denormalisation tool for integrating single-cell transcriptomics data”(Under review)

For any questions or issues, please open an issue in the repository. 
