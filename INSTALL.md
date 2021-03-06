### Installation instruction

Install java (jdk >= 1.7 or jre >= 1.7) and the latest git on your system. For Debian/Ubuntu based Linux, `$ sudo apt-get install git openjdk-8-jre`. For Fedora/Red-Hat based Linux,`$ sudo yum install git java-1.8.0-openjdk`. If you don't have super-user privileges on your system, locally install them and add them to `$PATH`.

Install Anaconda Python3 (or Miniconda3) on your system. If you already have it, skip this. Get the latest Miniconda3 installer at <a href="http://conda.pydata.org/miniconda.html" target=_blank>http://conda.pydata.org/miniconda.html</a> and install it. The following command is for Anaconda Python3 on 64bit Linux system.
```
$ wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
$ bash Miniconda3-latest-Linux-x86_64.sh
```
Choose `yes` for the final question. If you choose `no`, you need to manually add Miniconda3 to your `$HOME/.bashrc`.
```
Do you wish the installer to prepend the Miniconda2 install location
to PATH in your /your/home/.bashrc ? [yes|no]
[no] >>> yes
```
Remove any other Anaconda Python from your `$PATH`. Check your loaded modules with `module list` and unload any Anaconda Python modules. Open a new terminal after installation.

Install BigDataScript v0.999l on your system.
```
$ git clone https://github.com/pcingola/BigDataScript
$ cd BigDataScript
$ git checkout tags/v0.9999
$ cp distro/bds_Linux.tgz $HOME
$ cd $HOME
$ tar zxvf bds_Linux.tgz
```
Add `export PATH=$PATH:$HOME/.bds` to your bash initialization script (`$HOME/.bashrc` or `$HOME/.bash_profile`). If java memory occurs, add `export _JAVA_OPTIONS="-Xms256M -Xmx512M -XX:ParallelGCThreads=1"` too.

Get the latest version of the pipeline.
```
$ git clone https://github.com/kundajelab/TF_chipseq_pipeline
```
Install software dependencies automatically. It will create two conda environments (aquas_chipseq and aquas_chipseq_py3) in Miniconda3.
```
$ ./install_dependencies.sh
```
If you don't use `install_dependencies.sh`, manually replace BDS's default `bds.config` with a correct one:
```
$ cp bds.config ./utils/bds_scr $HOME/.bds
```
If `install_dependencies.sh` fails, run `./uninstall_dependencies.sh`, fix problems and then try `./install_dependencies.sh` again.


### How to install dependencies and share them on a cluster

If you have super-user privileges on your system, it is recommended to install Miniconda3 on `/opt/miniconda3/` and share conda environment with others.
```
$ sudo su
$ ./install_dependencies.sh
$ chmod 755 -R /opt/miniconda3/  # if you get some annoying permission issues.
```
In order to make Miniconda3 accessible for all users, create an intialization script `/etc/profile.d/conda_init.sh`.
```
$ echo '#!/bin/bash' > /etc/profile.d/conda_init.sh
$ echo 'export PATH=$PATH:/opt/miniconda3/bin' >> /etc/profile.d/conda_init.sh
```
