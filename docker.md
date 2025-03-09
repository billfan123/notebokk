docker容器登录的方法：
// 获取当前运行的docker 容器
docker ps
C:\Users\59901> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED       STATUS       PORTS     NAMES
918a56750ea5   ubuntu    "bash"    11 days ago   Up 11 days             pensive_shamir
// 通过docker exec命令
docker exec -it 918a56750ea5 /bin/bash
