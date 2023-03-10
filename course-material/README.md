# GPU Programming with OpenACC

4-5 December, 2017, at CSC - IT Center for Science.

## Table of content

1. [Schedule](#schedule)
1. [Material](#lecture-material)
1. [Instructions for running OpenACC exercises](#instructions-for-running-openacc-exercises)
1. [Exercises](#exercises)

## Schedule

| Day 1         |                              |
| ------------- | ----------------------------
| 9:00  - 10:00 | Introduction to accelerators
| 10:00 - 10:15 | Break
| 10:15 - 11:15 | Introduction to OpenACC
| 11:15 - 12:00 | Exercises
| 12:00 - 12:45 | Lunch
| 12:45 - 13:15 | Exercises
| 13:15 - 14:15 | OpenACC data management
| 14:15 - 14:30 | Break
| 14:30 - 16:00 | Exercises & wrap up of day 1

| Day 2         |                              |
| ------------- | ----------------------------
| 9:00  - 10:15 | Profiling and performance optimization
| 10:15 - 10:30 | Break
| 10:30 - 12:00 | Exercises
| 12:00 - 12:45 | Lunch
| 12:45 - 14:00 | Advanced topics
| 14:00 - 14:15 | Break
| 14:15 - 16:00 | Exercises & wrap up of day 2

## Lecture material

The [slides](https://events.prace-ri.eu/event/670/material/slides/) for the lectures of this course can be downloaded from the course [homepage](https://events.prace-ri.eu/event/670/) on the PRACE website.

Other external material

- [openacc.org](http://www.openacc.org)
- [openacc 2.5 specifications](http://www.openacc.org/sites/default/files/OpenACC_2pt5.pdf)
- [NVIDIA Accelerated Commputing](https://developer.nvidia.com/accelerated-computing)
- [NVIDIA OpenACC resources](https://developer.nvidia.com/openacc)
- [PGI compiler suite](http://www.pgroup.com/) Free of charge OpenACC compiler (community edition)

## Instructions for running OpenACC exercises

All exercises can be done using the local classroom workstations. You may also use the [Taito-GPU](https://research.csc.fi/taito-gpu) partition of Taito cluster.

### Downloading the exercises

To get the exercises you can clone the repository

```shell
git clone https://github.com/csc-training/openacc.git
```

This command will create a folder called `openacc` where all the materials are located. If the repository is updated during the course you can update your local copy of it with a `git pull` command.

You can find the exercises in two different folders within this repository. Folder [openacc/exercises](/exercises/) has a set of exercises prepared by CSC,while the exercises in [openacc/nvidia-labs](/nvidia-labs/) are courtesy of Nvidia.

### Compiling with PGI compiler

PGI compiler commands  are

- `pgcc` for C
- `pgfortran` for fortran
- `pgc++` for C++

OpenACC compilation can be enabled with option `-acc`. Note that without this flag, a non-accelerated version will be compiled. In addition to the acc flag, you have to specify the type of the accelerator with `-ta=nvidia,kepler` flag. If you run these exercises on some other system, you have to modify the type of the accelerator accordingly. You can check the type of the acclerator and recommended flags with command `pgaccelinfo`. If you want to get detailed information on OpenACC code generation, you can use option `-Minfo=accel`.

### Running on local desktop computers

Classroom workstations have Quadro K600 GPUs and both CUDA SDK and PGI compiler installations. The PGI compiler is not in the PATH by default, but you can initialize the environment using command `source ~/pgi/pgi_activate`.

### Running on Taito-GPU

You can log into [Taito-GPU](https://research.csc.fi/taito-gpu) front-end node using ssh command `ssh -Y trngXXX@taito-gpu.csc.fi` where `XXX` is the number of your training account. You can also use your own CSC account if you have one.

Before compiling the exercises you have to load the correct environment module `pgi/17.10` as well as reload the git module to access this repository

```shell
module load pgi/17.10
module load git
```

Serial jobs can be run interactively with srun command, for example

```shell
srun -n1 -pgpu --gres=gpu:k40:1 ./my_program
```

#### Reservation

This course has a resource reservation that can be used for the exercises. You can run your job within the reservation with `--reservation` flag, such as

```shell
srun --reservation=openacc_mon -n1 -pgpu --gres=gpu:k40:1 ./my_program
```

Names of the reservations for Monday and Tuesday are `openacc_mon` and `openacc_tue` respectively.
