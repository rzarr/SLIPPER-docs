---
title: Docker4SLIPPER

---

# Docker4SLIPPER



From version 3.1 on, the software provides also a Docker image for all the updated branches. The software has been successfully installed on Ubuntu, SL7 and some versions of MacOs. However, the Docker image provides a platform-indipendent environment to run the code without issues and with the needed ROOT (6.24) and Python (2 and 3) versions already installed.


# Docker image (working on Linux and MacOS)

The repository were all the images are hosted can be found at [this link](https://hub.docker.com/repository/docker/zarrella/slipper-docker). All images are built from a base version of Ubuntu, which is the OS where the code was tested the most and are continuously updated through GitLab Pipelines. The only requirement to use the image is a working [Docker](https://docs.docker.com/get-docker/) installation. The repository provides an executable that takes care of pulling the "latest" tag of the SLIPPER base image and build the "local" version. To get the images, run:



```cpp
>> ./path/to/slipper/docker/install_docker.sh
```

**N.B.: This step is mandatory since the "latest" tag of the slipper-docker image DOES NOT contain an installation of the software. It is only used as base image for faster build of the "local" version, which is the ONLY ONE that has a functioning SLIPPER installation. After this step is completed, the "latest" image can be removed.**

The SLIPPER version built inside the "local" docker image is by default the one of the "master" branch. If a different branch is needed, it can be set in the installation step via the command: 

```cpp
>> ./path/to/slipper/docker/install_docker.sh <branch-name>
```

where <branch-name> is the name of the SLIPPER repositiory branch you want to install. Otherwise, when running the docker, one can change the repository branch and recompile the software.

**N.B.: if the change of branch happens from inside the docker image, keep in mind that this step is only temporary and must be performed every time the docker is run. If the branch is chosen at the installation step, the choice is permanent.**

After the installation is finished, a docker container can be started launching the "run_docker.sh" executable found in the "docker" folder of the repository. This executable launches a container of the "local" tag of the slipper-docker image.

The executable also mounts the **current** local directory in the "/home/footer/data" path inside the container. This feature can be exploited to process data inside the container and make them available in the local host folder. So, to process the data, step into the folder containing all the binary files and launch:



```cpp
>> cd path/to/binary/files/folder
>> ./path/to/slipper/run_docker.sh
>> ...
```

To make the processed files available in the local host folder, save them in the shared folder ("data" inside the container).

**WARNING!! All the changes made to the shared folder from the container WILL be propagated to the local folder in the host system!**


# Running docker containers by hand (<a href="https://tenor.com/view/donald-trump-responsibility-i-dont-take-any-responsibility-at-all-no-responsibility-usa-president-gif-16623875">CLICK HERE BEFORE READING</a>)

After pulling the "latest" image and building the "local" version, it is possible to run a container using the command:



```cpp
>> docker run -it zarrella/slipper-docker:local
```

The "-it" option tells docker to run the container in interactive mode, meaning that it will open a shell with the poperly set environment and the already compiled software. From this shell, it is possible to run SLIPPER immediately.

In Docker, it is also possible to share a local folder with the container. To do so, step into the folder containing the input binary data and launch:



```cpp
>> docker run -it -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

This will mount the local current folder inside the container in "data". At this point, the binary input files can be processed from inside the container and the output can be saved in the "data" folder to make it accessible from outside docker.

With the current docker image, it is also possible to use the ROOT TBrowser from inside the container to check the contents of processed files. To activate this functionality, the DISPLAY variable needs to be passed to docker. This can be done with the following command on Linux:



```cpp
>> docker run -it --net=host -e DISPLAY=$DISPLAY -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

and MacOs:



```cpp
>> docker run -it --net=host -e DISPLAY=host.docker.internal:0.0 -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

For Windows users, the first step is to install an operating system that actually works :) 

-------------------------------

Updated on 2025-02-26 at 13:36:50 +0000
