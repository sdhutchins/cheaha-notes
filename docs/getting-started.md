# UAB Compute Cluster a.k.a. Cheaha

[TOC]

## Overview

Cheaha is a large, multi-unit computational system for running massively
parallel compute tasks. It is managed by the [UAB Research Computing Group](https://www.uab.edu/it/home/research-computing)

Cheaha is currently the fastest supercomputer in the state of Alabama with a theoretical throughput of
approximately 450 TFlop/s (HUGE COMPUTE!) and consists of over 3000 CPU cores and 72 NVIDIA-P100 GPU's. Cheaha is
supported by a high-speed parallel filesystem (GPFS) that can store 6 PB non-redundantly and 4 PB redundantly (with
more to come!) interconnected by a high speed infiniband network. UAB researchers use Cheaha for wide variety of
research such as genomics, neuro-imaging, machine learning, statistical genetics, cancer detection etc.

Use of this resource is governed by the
[UAB Acceptable Use Policy for Computer and Network Resources](https://www.uab.edu/policies/content/Pages/UAB-IT-POL-0000004.aspx)

For more information on Cheaha and the tools available to support research please review the documentation:
<http://docs.uabgrid.uab.edu/wiki/Cheaha>

## Access (Cluster Account Request)

To get started using [Cheaha](https://docs.uabgrid.uab.edu/wiki/Cheaha), simply visit our [Open OnDemand](https://docs.uabgrid.uab.edu/wiki/Open_OnDemand) portal at [https://rc.uab.edu](https://rc.uab.edu/). This is the primary entry point for Cheaha and provides access to all cluster services directly from your web browser, including graphical desktops, Jupyter Notebooks, and even the traditional command-line.

If you don't already have an account, you will be prompted to create one the first time you log into the portal. If you are creating an account, please share some of your interests in using Cheaha as this help us understand the science interests of our users.

**Please note**: Usage of Cheaha is governed by [UAB's Acceptable Use Policy (AUP)](https://www.uab.edu/policies/content/Pages/UAB-IT-POL-0000004.aspx) for computer resources.

## Logging In

Once your account has been created, you'll receive an email containing your user ID, generally your Blazer ID. You can [log into Cheaha via your web browser](https://rc.uab.edu/) using the new web-based HPC experience.

You can also log into Cheaha via a traditional SSH client. Most UAB Windows workstations already have an SSH client installed, possibly named **SSH Secure Shell Client** or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Linux and Mac OS X systems should have an SSH client installed by default.

Usage of Cheaha is governed by [UAB's Acceptable Use Policy (AUP)](https://www.uab.edu/policies/content/Pages/UAB-IT-POL-0000004.aspx) for computer and network resources.

Check out https://uabrc.github.io/cheaha/uabgrid_getting_started/#login for more details on logging in.

### Login Credentials

| Field           | Cheaha Settings   |
| --------------- | ----------------- |
| **Remote host** | cheaha.rc.uab.edu |
| **Port**        | 22                |
| **username** | blazerid |
| **password**        | blazerid password                |

## Storage

### User Storage

Each user is allocated 5 TB of personal storage by default. This storage quota is shared between the `USER_DATA` (`/data/user/<blazerid>`) and the `HOME` (`/home/<blazerid>`) directories. More information on storage can be [found here](../data_management/storage.md).

### Project Directories

In addition to personal storage, Primary Investigators may request additional shared storage for their lab personnel. This space is given a default size of 25 TB. Each PI may have one project space. To request project storage space, the PI should email support at support@listserv.uab.edu with the name of the project as well as the Blazer IDs of the researchers to give access to. Any future requests for giving or removing access must come from the PI.

## Submitting Jobs

You can SSH into the cluster via

```bash
ssh BLAZERID@cheaha.rc.uab.edu
```

The cluster uses the Slurm queue management system (stands for Simple Linux Utility for Resource Management) for
scheduling, distributing, and managing compute "jobs". A "job" is just a general term used to describe doing a specific
task, or set of tasks (specified in script) on the compute contained within the cluster.

For a complete description and tutorial of writing and executing jobs on the cluster see Research Computing's helpful
[guide](https://docs.uabgrid.uab.edu/wiki/Slurm) on Slurm and executing compute tasks on the cluster. You can also check
out the below tutorial for a quick high level view of the cluster.

## Python on Cheaha

Anaconda is a free and open-source distribution of the Python and R programming languages for scientific computing, that
aims to simplify package management and deployment. Package versions are managed by the package management system conda.
CDGS plans on using conda on the cluster for multiple projects involving the use of python.

### Conda Shortcuts on Cheaha

* Enabling Conda Module on Cluster
  `module avail Anaconda`

* Creating new Conda Environment
  `conda create --name test_env`
  Packages can be included within the new environment with a similar command
  `conda create --name test_env PACKAGE_NAME`
* List available virtual environments available
  `conda env list`
  Virtual environment with the asterisk(\*) next to it is the one that's currently active
* Activating conda virtual environment
  `source activate test_env`
* Deactivating Virtual Environment
  `source deactivate`
* Export Conda virtual environmnet to share
  `conda env export -n test_env > environment.yml`
* Creating Conda Virtual Environment from environment.yml
  `conda env create -f environment.yml -n test_env`
* Deleting a Conda Virtual Environment
  `conda remove --name test_env --all`

For a complete tutorial and for a most up-to-date version, please use the tutorial from
[UAB Research Compute's Anaconda documenation](https://uabrc.github.io/cheaha/conda/).
