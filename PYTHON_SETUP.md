---
title: Python set-up basics
layout: default
---
## Setting up Python
### Conda environments
When you install Python, it comes with a number of basic functionalities, but most people need to install extra _packages_ for their specific use-case. Packages contain extra functions and
classes that you can use for whatever you are doing. For example, Pandas is a powerful data manipulation package that is popular with data scientists, and Geopandas is its extension to 
geospatial data. Coders all over the world create packages and most packages have multiple versions, different versions of packages can conflict with eachother so its important to download 
the right versions. The safest and best-practise way to manage packages is to install them in _virtual environments_, this way you can have a virtual environment for each project you work on
and you are less likely to accidentally mess up your base environment (just the default environment on your system) or create package conflicts. _To be continued ..._ <br> <br>

### Uninstalling conda
```
conda install anaconda-clean
anaconda-clean

rm -rf anaconda3 (or whatever version you have)
rm -rf ~/anaconda3
rm -rf ~/opt/anaconda3
```
Open `~/.bashrc`, `~/.bash_profile`, `~/.zshrc`, `~/.zprofile` in your preferred code editor and remove all blocks of text related to conda. If you have mambaforge, miniconda, micromamba etc.
installed you can remove their directories with `rm -rf micromamba` etc. also.

### Fresh install
Navigate to the [Anaconda website](https://www.anaconda.com) and follow the installation instructions for your system.

### Conda commands
* `conda info`: get info about your conda install
* `--help`: after any command you want documentation on, e.g. `conda --help`, `conda env --help`
* `conda config --get`: list all channels used by conda
* `conda config --remove channels 'channel-name'` : remove a channel from conda 


### Jupyter notebooks
Lots of ways to do this. In terminal, making sure ipykernel and notebook are installed in your env:
```
cd <directory you want to run Jupyter Notebook from>
conda activate <myenv>
python -m ipykernel install --user -n <myenv>
jupyter notebook
```
This should open Jupyter notebook using your default web browser in the current directory.

### Mac Silicon Chips
If you have a Mac with an M1 or M2 chip, you may experience some issues with channel subdirectories. Conda detects your system type and chooses subdirectories based-on this. For example if you have 
an M1 chip, conda will use the conda-forge subdirectories conda-forge/osm-arm63 or conda-forge/noarch, but if you have an Intel chip it will use conda-forge/osx-64. This can cause issue with certain
channels such as bioconda, where the osm-arm64 does not have many of the popular packages. Luckily, if you have [Rosetta 2 installed](https://support.apple.com/en-gb/HT211861) you can set up virtual
environments that use packages downloaded from the osx-64 subdirectories. To do this create your environment using the following commands
```
CONDA_SUBDIR=osx-64 conda create -n intel_env python
conda activate intel_env
conda config --env --set subdir osx-64
```
You can modify this in the usual way to set up from a YAML file, just make sure to include the line `CONDA_SUBDIR=osx-64` at the beginning and `conda config --env --set subdir osx-64` after activating the environment.


### Mamba
