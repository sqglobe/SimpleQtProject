# SimpleQtProject

Проект содержит простой пример графического приложения **Qt**, в качестве системы сборки используется **qmake**.

Папка **docker** содержит **docker**-файл, который описывает систему кросс-платформенной сборки приложения для **Windows**.
Для этого используется среда [mxe](https://mxe.cc/).

Чтобы собрать контейнер, необходимо выполнить в папке **docker** команду:

```
docker build -t simple-qt-build --file windows.docker .
```

Перед запуском сборки в полученном контейнере, необходимо создать дирректорию **docker/result**. Запускается сборки из 
папки **docker** командой:

```
docker run  --mount type=bind,source=$(pwd)/result/,target=/app/res --mount type=bind,source=$(pwd)/../,target=/app/src simple-qt-build
```

После завершения, в дирректории **docker/result** будет находится исполняемый файл **SimpleQtProject.exe**.
