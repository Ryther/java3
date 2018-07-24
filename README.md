
# JDK3 docker container
--------------------------------
### Container Docker per la compilazione di software che usa JDK3

|OS|CREATION COMMAND|
|:-:|:--------------|
|Windows|`docker run -tdi --name=jdk3 --net="host" --privileged=true -v jdk3_workdir:/home/developer ryther/jdk3:latest`
|Linux|`sudo docker run -tdi --name=jdk3 --net="host" --privileged=true -v jdk3_workdir:/home/developer ryther/jdk3:latest`

---------------------------------

Una volta creato il container, per eseguirlo nuovamente utilizzare il comando:  
>`docker start jdk3`

----------------------

> Written with [StackEdit](https://stackedit.io