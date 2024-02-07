# Snakemake for reproducible analyses

This repository is used as a base for the workshop "Introduction to Snakemake for reproducible analyses". The repository contains:

- A conda environment with all the dependencies required during the workshop
- A reference implementation of solutions for all exercises
- A 'workflow' directory with sample data in which participants will implement the exercises

The structure of the workshop loosely follows that of the official [Snakemake tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html), with a few modifications.

All the exercises and material required to complete them are available on the repository's [wiki](https://github.com/ThibaultLatrille/workshop-snakemake-unil2023/wiki).

## Setup the workshop environment

## Note for Windows user

Although Snakemake and Conda can work on Windows, the shell and general environment are very different from unix-based operating systems. If you are using a Windows machine for this workshop, please refer to the [Windows installation instructions](https://snakemake.readthedocs.io/en/stable/tutorial/setup.html#setup-on-windows) in the official documentation. We recommend you to setup the WSL if you can, as it is the most efficient way to run Snakemake on Windows, and it will be useful for many other Bioinfomatics applications in the future.

### Installing Conda and Mamba

Detailed instructions [here](https://github.com/conda-forge/miniforge).

**Download the installer script and run it:**

Unix-like platforms (Mac OS & Linux)

```bash
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash Miniforge3-$(uname)-$(uname -m).sh
```

Follow instructions from the prompt, and restart your shell.

To verify that the installation process completed correctly, run:

```bash
conda env list
```

The output should look like this (username and hostname will be different):

```bash
(base) user@host:~$ conda env list
# conda environments:
#
base                  *  /opt/homebrew/Caskroom/miniforge/base
```

### Clone the workshop's repository

**With SSH (recommended in general for GitHub, need to set it up if you haven't already):**

```bash
git clone git@github.com:ThibaultLatrille/workshop-snakemake-unil2023.git
```

**With HTTPS (default, no setup required):**

```bash
git clone https://github.com/ThibaultLatrille/workshop-snakemake-unil2023.git
```

### Create a Conda environment with all software required by the workshop

We provide an environment file `workshop.yaml` that contains all software required to complete the workshop.

Navigate to the workshop's base directory. If you followed the previous instructions exactly, you can do with:

```bash
cd workshop-snakemake-unil2023
```

Create the conda environment from the environment file with mamba:

```bash
mamba env create -f workshop.yaml
```

This step usually takes some time (up to 20-30 minutes), as there is a lot of dependencies to install.

Once the environment is created, activate it with:

```bash
conda activate snakemake-workshop
```

Note for Mac users on Apple Silicon (M1/M2/M3), the previous commands won't work and you need to instead use:
```bash
CONDA_SUBDIR=osx-64 mamba create -n snakemake-workshop python=3.9
conda activate snakemake-workshop
conda config --env --set subdir osx-64
mamba env update --file workshop.yaml
```

You can now run Snakemake and complete the workshop's exercises.

### Additional note: creating a Conda environment for Snakemake

For this workshop, for the sake of simplicity, we created a single Conda environment that contains both Snakemake and all the tools used in the workflow. In practice, this is not the correct way to use Conda with Snakemake workflows, as we will discuss during the workshop. This step is not part of the setup process, but if you want to use Snakemake by yourself in the future, the recommended way to run it is to create a conda environment specifically and only for Snakemake:

```bash
# Create a new empty environment called "snakemake"
conda create --name snakemake
# Activate the environment "snakemake"
conda activate snakemake
# Install snakemake from the Bioconda channel (conda-forge contains dependencies)
mamba install -c conda-forge -c bioconda snakemake
```

You can now activate the environment snakemake and run Snakemake from it. It is advised to keep the environment as clean as possible, *i.e.* only install software related to running snakemake in general, not software specifically for your workflow.
