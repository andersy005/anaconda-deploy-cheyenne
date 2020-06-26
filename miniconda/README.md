# Conda deployment on Cheyenne

- [Conda deployment on Cheyenne](#conda-deployment-on-cheyenne)
  - [Installing using HPCinstall](#installing-using-hpcinstall)
  - [Usage](#usage)

Documented script example of Miniconda deployment on [Cheyenne Supercomputer](https://www2.cisl.ucar.edu/resources/computational-systems/cheyenne).

## Installing using [HPCinstall](https://github.com/NCAR/HPCinstall)

- Get the source code

  ```bash
  $ git clone https://github.com/andersy005/modules-cheyenne.git
  $ cd modules-cheyenne/miniconda
  ```

- Load HPCinstall module

  ```bash
  $ module purge
  $ module use $MODULEPATH_ROOT/system
  $ module load hpcinstall
  ```

NOTE: By default, `hpcinstall` module works with Python 2 only. Therefore, please make sure that you have `python2` as your default on your path by running the following commands:

```bash
$ which python
$ python --version
```

- Install using HPCinstall. `force` argument is used to force overwrite of existing install. For more details on how to use `hpcinstall`, just run `hpcinstall --help`.

  ```bash
  $ hpcinstall build_conda --force
  ```

## Usage

Hpcinstall sets some environment variables that are needed when loading a newly created module.
To get these environment variables, look for `hpci.main.log` file in the directory from which you executed the installation command above.

You will see something that looks like:

```bash
abanihi@cheyenne1: /glade/work/abanihi/devel/personal/modules-cheyenne/conda $ cat hpci.main.log
On 2018-10-11T11:36:58.229174 abanihi
called HPCinstall from /gpfs/u/apps/ch/opt/hpcinstall/1.2.6/hpcinstall.py
invoked as /gpfs/u/apps/ch/opt/hpcinstall/1.2.6/hpcinstall build_miniconda --force

Setting environmental variables:
HPCI_SW_DIR       = /glade/work/abanihi/softwares/miniconda/3/
HPCI_SW_NAME      = miniconda
HPCI_SW_VERSION   = 3
HPCI_MOD_DIR      = /glade/work/abanihi/softwares/modulefiles/
HPCI_MOD_DIR_IDEP = /glade/work/abanihi/softwares/modulefiles/idep/
HPCI_MOD_DIR_CDEP = not_compiler_dependent
HPCI_MOD_PREREQ   =
Running ./build_conda...
Done running ./build_conda - exited with code 0
For more details about this code, see URL: https://conda.io/docs/
Hashdir: d41d8cd98f00b204e9800998ecf8427e /glade/work/abanihi/softwares/miniconda/3
```

To load the `conda` module, you will need to run:

`$ module use $HPCI_MOD_DIR`

`$ module load conda`

NOTE: Replace `HPCI_MOD_DIR` with the corresponding value printed above.

```bash
$ module use /glade/work/abanihi/softwares/modulefiles/
$ module load miniconda # Load the module
$ module help miniconda # Use module help to find more info on the module
```

**You are now all set!**
