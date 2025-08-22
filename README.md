# SimpleQtProject

This project contains the simplest Qt based application and uses as the building system **qmake**.
It's used to demonstrate building process in the docker container for different platforms. 

Folder _docker_ contains several Docker-files, each provides an environment for the following systems:
* Ubuntu 24.04
* Ubuntu 18.04 LTS
* Windows

For the Windows the cross compilation is used, which is facilitated by project [MXE](https://mxe.cc/).

In order to run build for the all listed platforms it's enough to run command `make` in the folder _docker_.
It will build docker images if required and then invoke each container to compile the project for the specified environment.

Just to build manually docker image, for example for Windows environment, use the following command:
```
docker build -t simple-qt-build --file windows.docker .
```

In order to run the building of the project in the created container, for example for Windows, utilize the following:
```
docker run  --mount type=bind,source=$(pwd)/result/,target=/app/res --mount type=bind,source=$(pwd)/../,target=/app/src simple-qt-build
```

When this command is finished, the folder _docker/result_ will contain building results, for example _SimpleQtProject.exe_ in the Windows case. To run it under Linux consider applying **wine**:
```
wine SimpleQtProject.exe
```