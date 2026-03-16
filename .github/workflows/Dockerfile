# Use the specified Miniforge base image
FROM condaforge/miniforge3:25.3.1-0

# Set the working directory
WORKDIR /app

# Copy repository files into container
COPY . /app

# Install system dependencies including fonts
RUN apt-get update && apt-get install -y \
    font-manager \
    debconf-utils \
    fonts-dejavu \
    fonts-liberation \
    fonts-freefont-ttf \
    ttf-mscorefonts-installer \
    && echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
    && fc-cache -fv \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Install JupyterLab, nb_conda, and ipykernel in the base environment
RUN conda install -n base jupyterlab nb_conda ipykernel

# Create a Conda environment named 'sc' with Python
RUN conda create -n sc python=3.9

# Install required packages in the 'sc' environment
RUN conda run -n sc conda install numpy==1.22.4 pandas==1.5.3 scipy==1.10.1 \
    matplotlib==3.6.3 \
    matplotlib-inline=0.1.2 matplotlib-venn \
    seaborn=0.11.2 scanpy=1.9.6=pyhd8ed1ab_0 anndata=0.10.3=pyhd8ed1ab_0 \
    ipykernel=6.9.1 python-annoy=1.17.3

# Install additional pip packages
# Note: numpy is upgraded to 1.26.4 as per your new list
RUN conda run -n sc pip install \
    bbknn==1.6.0 \
    colorlog==6.9.0 \
    cython==3.1.4 \
    fastcore==1.8.9 \
    harmonypy==0.0.10 \
    numpy==1.26.4 \
    pathlib==1.0.1 \
    psutil==7.1.0 \
    pyqt5-sip \
    pyqtchart==5.12 \
    pyqtwebengine==5.12.1 \
    sccaf \
    scdenorm

# Install R and IRkernel
RUN conda run -n sc conda install r-base=4.0.2=he766273_1 r-irkernel=1.3=r40hc72bb7e_0

RUN conda run -n sc R -e "IRkernel::installspec(name='ir', displayname='R (sc)')"

RUN apt-get update && apt-get install -y \
    libxml2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libfontconfig1-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    build-essential \
    libx11-6 libxt6 libxrender1 libxext6 \
    && rm -rf /var/lib/apt/lists/*

RUN conda run -n sc conda install -y -c conda-forge r-ggplot2 r-stringr r-purrr

RUN conda run -n sc conda install -c conda-forge r-fastmap r-bit r-cachem r-bit64 r-memoise r-rsqlite

RUN conda run -n sc conda install -c bioconda bioconductor-org.hs.eg.db==3.12.0 bioconductor-clusterprofiler

# Set up Jupyter kernel for the 'sc' environment
RUN python -m ipykernel install --user --name sc --display-name "Python (sc)"

# Expose the default Jupyter port
EXPOSE 8888

# Command to run JupyterLab
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--no-browser", "--allow-root"]


