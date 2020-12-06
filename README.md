# Build Python 3.9 from source on Linux (Ubuntu and Debian)
Procedure has been tested on `Ubuntu 20.04 LTS` and `Debian GNU/Linux 10 (Raspberry Pi)`.  
An alternative installation will be made meaning the Python 3 version that comes with the Linux distribution will not be broken.
This is important because a lot of Linux packages depend on the Python 3 version that comes with the distro.  
Python 3 that comes with the Linux distro: `/usr/bin/python3`  
Newly installed alternative Python 3 version: `/usr/local/bin/python3.9`  
The Python package manager `pip` and `setuptools` will be part of this installation.


## References
[GitHub cpython project](https://github.com/python/cpython/)  
[Build CPython on Linux](https://cpython-core-tutorial.readthedocs.io/en/latest/build_cpython_linux.html#)  
[Python Source Releases](https://www.python.org/downloads/source/)  
[How to Install Python 3.8 on Ubuntu, Debian and LinuxMint](https://tecadmin.net/install-python-3-8-ubuntu/)

## Prerequisites
Make sure you are connected with an OS user with sudo rights.  
Update and upgrade all system packages:
```
$ sudo apt update
$ sudo apt full-upgrade -y
```
Install the Linux development libraries to compile Python source code:
```
$ sudo apt install build-essential checkinstall -y
$ sudo apt install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev -y
```
Make sure wget is installed (missing on some Linux distros):
```
$ sudo apt install wget -y
```

## Download source files and build/install Python 3.9
In this example `Python 3.9.0` sourcecode files will be used but the procedure can also be tested on other Python versions.   
Download and extract source code files:
```
$ wget https://www.python.org/ftp/python/3.9.0/Python-3.9.0.tgz
$ tar -xzf Python-3.9.0.tgz
```
Change working directory:
```
$ cd Python-3.9.0
```
Prepare the build with optimization features:
```
$ ./configure --enable-optimizations
```
Finally perform the actual build (make command needs to be executed with sudo rights):
> We will use `make altinstall` to prevent replacing the default Python 3 binaries that come with the Linux distro.
```
$ sudo make altinstall
```
Go back to directory where initial file was downloaded, remove downloaded file and directory containing the extracted files (with sudo because some files are owned by root):
```
$ cd ..
$ rm Python-3.9.0.tgz
$ sudo rm -rf Python-3.9.0
```

## Check installation and usage
Newly installed alternative version can be used with command `python3.9`, the version from the Linux distro can still be used with command `python3`.  
Check Python 3 location for Linux distro and alternative version:
```
$ which python3
/usr/bin/python3
$ which python3.9
/usr/local/bin/python3.9
```
Check Python 3 version for Linux distro and alternative version:
```
$ python3 -V
Python 3.7.3
$ python3.9 -V
Python 3.9.0
```
Show Python packages that come with the newly installed version:
```
$ python3.9 -m pip list
Package    Version
---------- -------
pip        20.2.3
setuptools 49.2.1
```

## Create virtual environment(s)
It is always recommended to create virtual environments per project which will allow you to install different Python packages.   
Create a new Python environment called `myenv`:
```
$ python3.9 -m venv myenv
```
Activate the environment:
```
$ source myenv/bin/activate
```
From now on `python` can be used as command:
```
$ which python
/home/wim/myenv/bin/python
$ python -V
Python 3.9.0
```
Update `pip` and `setuptools` to the latest version:
```
$ python -m pip install --upgrade pip setuptools
$ pip list
```
Other Python packages can easily be installed now via `pip` in the virtual environment (example `requests` package):
```
$ pip install requests
$ pip list
```
