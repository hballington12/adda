# Getting started...

## Compiling an Exectuable File

This part of the tutorial is based on the [compiling](https://github.com/adda-team/adda/wiki/CompilingADDA) section of the [ADDA wiki](https://github.com/adda-team/adda/wiki).

To get started with ADDA on the UHHPC cluster, we need to compile the ADDA source code. To do this, we will need to first add the ADDA source code on to the cluster. One possible location for doing this is in your `\home` directory. At the time of this post, the storage quota for your home directory is 50 GB. The ADDA source code takes up approximately 100 MB of space so it's acceptable to put these in your home directory, for now. To clone the ADDA source files, we will use PuTTY, which is used for establishing a secure connection between our device and one of the head nodes on the cluster.

1. First, open PuTTY and log on to the cluster with your username and password.

2. The ADDA code is developed in C, Fortan, and C++. Therefore, we should ensure that a relevant module is loaded on the head node. For example, in PuTTY, use the command: 

```
module load gcc-6.4
```

3. Next, we will use the git module to add the ADDA source code into our `\home` directory. The git module is already installed on the cluster and the source code can be added using the `clone` command. In PuTTY, use the command: 

```
git clone https://github.com/adda-team/adda.git
```

4. According to the [ADDA documentation](https://github.com/adda-team/adda/wiki/CompilingADDA), we must position ourselves in the `\src` directory, if we want to compile the ADDA code. Therefore, in PuTTY, use the command:

```
cd adda/src
```

5. We will now use [GNU Make](https://www.gnu.org/software/make/) to make an executable file on the cluster. The ADDA code has various versions, such as MPI and OpenCL, which are designed to take advantage of particular computer architectures. For now, we will use the sequential version, which is standard. We will now compile the source code into an executable file. In PuTTY, use the command:
```
make seq
```
This should create some `.o` files, as well as an exectuable file called `adda` in the `/home/<user>/adda/src/seq` directory. The `adda` executable file is a compiled version of all the ADDA source code, which can be understood by the cluster to run ADDA computations. In the next section, we will look at how to submit a job on the cluster using the `adda` executable file.

## Submitting an ADDA Job on the Cluster

Now that we've created an executable ADDA file for the cluster, we need to set up a directory to execute the job from. For this, we will use WinSCP to create a directory and some files but you can use any other means that you are comfortable with. 
1. First, open WinSCP and log on to the cluster with your username and password.
2. Make a new directory (shortcut F7) in your home folder. Name it `clusterTest` (case-sensitive!). 
3. Within the `clusterTest` directory, make a new file and name it `adda.sh`. This is our ADDA shell file. It will contain information about our job requirements and the settings that we want to run ADDA with. 
4. Open the shell file and paste the following:

```
    #!/bin/sh
    #PBS -l walltime=0:10:00
    #PBS -l nodes=1:ppn=1
    #PBS -k oe
    #PBS -o /adda/clusterTest
    #PBS -e /adda/clusterTest
    echo ------------------------------------------------------
    echo -n 'Job is running on node '; cat $PBS_NODEFILE
    echo ------------------------------------------------------
    echo PBS: qsub is running on $PBS_O_HOST
    echo PBS: originating queue is $PBS_O_QUEUE
    echo PBS: executing queue is $PBS_QUEUE
    echo PBS: working directory is $PBS_O_WORKDIR
    echo PBS: execution mode is $PBS_ENVIRONMENT
    echo PBS: job identifier is $PBS_JOBID
    echo PBS: job name is $PBS_JOBNAME
    echo PBS: node file is $PBS_NODEFILE
    echo PBS: current home directory is $PBS_O_HOME
    echo PBS: PATH = $PBS_O_PATH
    echo ------------------------------------------------------

    ulimit -s unlimited
    cd /home/<user>/clusterTest
    /home/<user>/adda/src/seq/adda
```
5. Now that the shell file has been made, we are almost ready to submit the job to the cluster. In PuTTY, navigate to the location of the shell file using:
```
cd; cd/clusterTest
```
6. Now we can submit the job. In PuTTY, use:
```
qsub adda.sh
``` 

If successful, you should see output parameters from the job in the `clusterTest` directory. Note that some arguments may require you to add some extra files to the working directory. For example, the `-store_scat_grid` requires that the `scat_params.dat` file is added to the current directory (thanks to Rob for pointing this out).
  
  
[Previous page](./README.md)

#### [Home](./README.md) 
