# Using conda module on Cheyenne/Casper

- [Using conda module on Cheyenne/Casper](#using-conda-module-on-cheyennecasper)
  - [Load the miniconda module](#load-the-miniconda-module)
  - [One-Time Setup](#one-time-setup)
    - [Initialize your shell](#initialize-your-shell)
    - [Update conda configuration to your liking](#update-conda-configuration-to-your-liking)
  - [View the contents of the generated config file. You should now have a `.condarc` file in your home directory](#view-the-contents-of-the-generated-config-file-you-should-now-have-a-condarc-file-in-your-home-directory)
  - [Check the location of the user's conda installation:](#check-the-location-of-the-users-conda-installation)
  - [Create a test environment](#create-a-test-environment)

## Load the miniconda module

```bash
$ ml
No modules loaded

$ # This is needed for the module loading to work
$ module use /glade/work/abanihi/softwares/modulefiles
$ module load miniconda
$ module save

$ ml

Currently Loaded Modules:
  1) miniconda/3

$ which conda
/glade/work/abanihi/softwares/miniconda3/bin/conda
```

## One-Time Setup

### Initialize your shell

```bash
$ conda init <SHELL_NAME>
```

Currently supported shells are:

    - bash
    - fish
    - tcsh
    - xonsh
    - zsh
    - powershell

After running `conda init`, log out and log in again.

### Update conda configuration to your liking

See [conda config](https://docs.conda.io/projects/conda/en/latest/commands/config.html) for more info.

```bash
# Add conda-forge channels
conda config --add channels conda-forge
conda config --set channel_priority flexible
conda config --set show_channel_urls True

# Specify the location to use when creating new environments
# Make sure to change this to some place more permanent and with more space
# such as your work directory i.e /glade/work/YOURUSERNAME/miniconda/envs
# Replace $YOURUSERNAME with your username
conda config --add envs_dirs /glade/work/$YOURUSERNAME/miniconda3/envs
conda config --add pkgs_dirs /glade/work/$YOURUSERNAME/miniconda3/pkgs

# Install pip any time Python is installed.
conda config --set add_pip_as_python_dependency True

# cleanly remove pip-installed software, and replace them with
# conda packages when appropriate.
conda config --set pip_interop_enabled True

# Do not activate base.
# conda config --set auto_activate_base False

# Install these packages by default when using `conda create`.
conda config --append create_default_packages ipykernel \
             --append create_default_packages jupyter
```

## View the contents of the generated config file. You should now have a `.condarc` file in your home directory

```bash
$ cat ~/.condarc
add_pip_as_python_dependency: true
channels:
  - conda-forge
  - defaults
channel_priority: flexible
show_channel_urls: true
pip_interop_enabled: true
...
```

## Check the location of the user's conda installation:

```bash
$ conda info

     active environment : None
       user config file : /glade/u/home/abanihi/.condarc
 populated config files : /glade/u/home/abanihi/.condarc
          conda version : 4.8.3
    conda-build version : not installed
         python version : 3.8.3.final.0
       virtual packages : __cuda=10.1
                          __glibc=2.17
       base environment : /glade/work/abanihi/softwares/miniconda3  (writable)
           channel URLs : https://conda.anaconda.org/conda-forge/linux-64
                          https://conda.anaconda.org/conda-forge/noarch
                          https://conda.anaconda.org/pytorch/linux-64
                          https://conda.anaconda.org/pytorch/noarch
                          https://conda.anaconda.org/rapidsai/linux-64
                          https://conda.anaconda.org/rapidsai/noarch
                          https://repo.anaconda.com/pkgs/main/linux-64
                          https://repo.anaconda.com/pkgs/main/noarch
                          https://repo.anaconda.com/pkgs/r/linux-64
                          https://repo.anaconda.com/pkgs/r/noarch
         ...
```

## Create a test environment

```bash
$ conda create -n test-env -c conda-forge python=3.8 xarray netcdf4
$ conda activate test-env
$ ipython # Launch Ipython
```

Confirm the environment was properly created:

```python
In [1]: import xarray as xr

In [2]: import sys

In [3]: sys.executable
Out[3]: '/glade/scratch/abanihi/miniconda3/envs/test-env/bin/python'
```

**You are now all set!**
