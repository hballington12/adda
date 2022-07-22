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




[Previous page](./README.md)

#### [Home](./README.md) 
