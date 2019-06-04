# CLM-R2

_Steps to build CLM on Boise State's R2 cluster._
<br>

## File Structure
```bash
$HOME
├── .cime
│   ├── config_compilers.xml
│   ├── config_batch.xml
│   └── config_machine.xml
├── clm5.0
│   ├── bld
│   ├── cime
│   ├── cime_config
│   ├── CODE_OF_CONDUCT.md
│   ├── components
│   ├── CONTRIBUTING.md
│   ├── Copyright
│   ├── CTSMMasterChecklist
│   ├── doc
│   ├── Externals.cfg
│   ├── Externals_CLM.cfg
│   ├── LICENSE
│   ├── manage_externals
│   ├── parse_cime.cs.status
│   ├── README
│   ├── README_EXTERNALS.rst
│   ├── README.rst
│   ├── src
│   ├── src_clm40
│   ├── test
│   └── tools
├── cesm
│   ├── scratch
│   |   ├── archive
|   │   |   └── $CASE
│   |   └── build/run
|   │   |   └── run
│   ├── inputdata
|   │   |   └── atm
|   |   │   |   └── wrf
│   └── cesm_baselines
├── clmcases
└── .cesmproj
```


### README.md File Contents
#### 1. [Overview](#1-overview-1)
#### 2. [Quick Start Guide](#2-quick-start-guide-1)
###### &nbsp;&nbsp;&nbsp; 2.1 [Clone CLM Repository and config files](#21-clone-clm-repository-and-config-files)
###### &nbsp;&nbsp;&nbsp; 2.2 [Load necessary modules](#22-load-necessary-modules)
###### &nbsp;&nbsp;&nbsp; 2.3 [Create, built and submit a case](#23-create,-build-and-submit-a-case)
####  3. [Links](#4-links-1)
---
<br>
<br>

## 1. Overview
This repository is a collection of scripts to build the Community Land Model (CLM) 5.0. 
<br>
<br>

## 2. Quick Start Guide
#### 2.1 Clone CLM Repository and config files
  * From a `bash terminal` navigate (`cd`) to your home directory, where you will clone the CLM repository:
    
      ```bash
      $ cd
      ```
      > *When you use `cd` without any arguments, the shell will automatically take you back to $HOME*
      > *In R2, your $HOME is `/home/<yourusername>/`. The '`~`' is also an alias in bash for 'home directory'*
     
  * The URL for the CLM repo is:  `https://github.com/ESCOMP/ctsm.git`
  * At the `bash` command prompt (`$`) issue the command:
  
      ```bash
      $ git clone -b release-clm5.0 https://github.com/ESCOMP/ctsm.git clm5.0 
      ```
      
      > *This command string asks the the version control system `git` to `clone` (think 'copy' or* 
      > *or 'download') the GitHub repository located at `https://github.com/ESCOMP/ctsm.git`,*
      > *to your account on R2.*
  * Next be prompted for your github `username` and `password`.
  * If authentication is successful, `git` will transfer all the contents of the repository to your computer,
  then you will have a new directory, `clm5.0/`, in your current working directory.
  * In your same current working directory, make a new directory called '.cime'
  
    ```bash
    $ mkdir ~/.cime
    ```
    >*This is where the config files describing R2 for CLM will live.*
    >*The '`.`' that comes before the directory name means that this directory will be hidden when you list a*
    >*directory's contents using `ls`. To see directories with a '`.`' in front of them, you use the command `ls -a`*
  * At the `bash` command prompt, issue the command:
  
      ```bash
      $ git clone https://github.com/LEAF-BoiseState/CLM-R2.git
      ```
  * There should now have a directory titled "CLM-R2" in your home directory
  * You will want to move the files contained in this directory into .cime, using the following command:
  
      ```bash
      $ mv CLM-R2/* ./.cime
      ```
      > *This command string is telling the shell to move (`mv`) all of the files (`*`) contained in directory CLM-R2*
      > *into the `.cime` directory. The '`.`' is an alias in bash for 'current working directory'*
      > *The '`*`' is a "wildcard" variable that stands in for any number of alphanumerics, and is often used to select*
      > *or display everything in a given repository*
  * Navigate into `.cime` using the `cd` command.
  
      ```bash
      $ cd .cime
      ```
      
  * To _list_ &nbsp;the contents of the .cime directory, issue an `ls` at the command prompt:
   
      ```bash
      $ ls
      ```
  * Confirm that there are three xml files located there: config_batch.xml, config_compilers.xml, config_machines.xml
  * Navigate back to your home directory, where you can now delete the original CLM-R2 directory as follows:
  
      ```bash
      $ rm -rf CLM-R2
      ```
  <br>
  <br>

#### 2.2 Load necessary modules
  * Load the following modules
  
  ```bash
  $ module load intel/compiler/64/2017/17.0.7 intel/mkl/64/2017/7.259 intel/mpi/64/2017/7.259 python/intel/2.7 netcdf/intel/64/4.4.1
  ```
  
  * xxxx may need to compile in gnu! xxxx
  <br>
  <br>
  
#### 2.3 Create, built and submit a case
  * From your home directory, create a new directory called '`clmcases`'
    
      ```bash
      $ mkdir ./clmcases
      ```
      
  * Navigate into $HOME/clm5.0/cime/scripts
  
      ```bash
      $ cd clm5.0/cime/scripts
      ```

  * The file `create_newcase` is located in the directory `clm5.0/cime/scripts/`, so from this location in the directory tree we 
  can issue the command to run the contents of this file as follows:
     
     ```bash
     $ ./create_newcase --case ~/clmcases/I1850CLM50_001 --res f19_g17 --compset I1850Clm50Sp --project UCGD0004
     ```
     
     > *The command string above creates a new simulation titled I1850CLM50_001, which it is creating in a new case directory*
     > *The commands you will neeed to set-up, build and submit a case will all be located in this case directory*
  
  * Navigate to your case directory
  
      ```bash
      $ cd ~/clmcases/I1850CLm50_001
      ```
      
  * Set up your case using the following command:
  
      ```bash
      $ ./case.setup
      ```
      
  * Build your case using the following command:

      ```bash
      $ ./case.build
      ```
  <br>
  <br>
   
#### 3. Links
  * <sup><a name="1">1</a></sup> [CLM5.0 Tutorial - Danica Lombardozzi](https://leaf-boisestate.atlassian.net/wiki/spaces/LTH/pages/813727746/Running+CLM+on+R2?preview=/813727746/813793299/2019CLMTutorial_practical1-lombardozzi.pdf) 
    >* A tutorial put together by Danica Lombardozzi for the CLM 5.0 Tutorial in 2019 that has greater detail about the steps outlined above
  * <sup><a name="1">1</a></sup> [CESM Documentation: Introduction](https://escomp.github.io/cesm/release-cesm2/introduction.html) 
    >* A step-by-step guide to installing CESM and building cases. Assumes you are on NCAR's cluster. 
  * <sup><a name="1">1</a></sup> [Porting CIME based models](https://docs.google.com/presentation/d/1min2MUtyqXdjSYLTZOZaU8Iv2FQVWOBGXDL0uOcxqh8/edit#slide=id.p) 
    >* A guide to porting CIME based models by Jim Edwards. 
  <br>
  <br>
  <br>
  <br>
  
  
  
