# Spack deployment on Cheyenne
Documented example of [Spack](https://github.com/spack/spack) deployment on [Cheyenne Supercomputer](https://www2.cisl.ucar.edu/resources/computational-systems/cheyenne).


# Installing using [HPCinstall](https://github.com/NCAR/HPCinstall)

- Get the source code
```bash
$ git clone git@github.com:andersy005/modules-cheyenne.git
$ cd modules-cheyenne/spack
```

- Load HPCinstall module
```bash
$ module use $MODULEPATH_ROOT/system
$ module load hpcinstall
```

NOTE: By default, `hpcinstall` module works with Python 2 only. Therefore, please make sure that you have `python2` as your default on your path by running the following commands:

    $ which python 
    $ python --version 

- Install using HPCinstall. `force` argument is used to force overwrite of existing install. For more details on how to use `hpcinstall`, just run `hpcinstall --help`. 

```bash
$ hpcinstall install_spack --force 
```

# Usage 

```bash
$ module use module use /glade/work/abanihi/softwares/modulefiles/
$ module load spack # Load the module
$ module help spack # Use module help to find more info on the module
```