# Docker for absolute beginners 

**docker image** = template 

**docker container** = instance 



## basic docker command



`docker run <container-name>` = to run a container from an image

`docker ps` = list all active containers

`docker ps -a`  = list all containers

`docker stop <container-name>` = stop a container 

`docker rm <container-name> ` = remove container

`docker images` = list all images

`docker rmi <image-name> ` = remove image

`docker pull <image-name>` = download an image

say we execute `docker run ubuntu` => this will exit asap, because it is meant to be just used as a base to run other services on

`docker exec <container-name> cat /etc/hosts` = to execute a command inside a given container  

`docker run -d <container-name>` = to run a container from an image in detached mode 

## docker run

`docker run -it <container-name> bash` = attach to the terminal in an interactive mode

`docker inspect <container-name>` = see details on a container

`docker logs <container-name>` = see logson a container

### 

### port mapping

<img src="C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200727062345779.png" alt="image-20200727062345779" style="zoom:70%;" />

eg: `docker run -p 8080:8080 jenkins` - you are able to access jenkins on localhost:8080 because this port is mapped to the docker host port 

### volume mapping

<img src="C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200727062456169.png" alt="image-20200727062456169" style="zoom:70%;" />

eg:  ` docker run -p 8080:8080 -v /root/my-jenkins-data:/var/jenkins_home -u root jenkins` - you are able to access jenkins on localhost:8080 because this port is mapped to the docker host port 

`docker run -it --name admin -v /root/my-jenkins-data ubuntu` && `ls`

### env variables

`docker run -e <env-var>=<val> <container-name>` = attach to the terminal in an interactive mode

`docker inspect <container-name>` = lists all environment variables 

## docker images

![image-20200727200914160](C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200727200914160.png)

making some calls within the container :smile:

docker image = write down steps you followed to get to the above

 `history` command is useful to see all command executed in bash 

```txt
docker run -it ubuntu
apt-get update
apt-get install -y python
apt-get install python3-pip
pip3 install flask
cat > /opt/app.py
<copy pasta flask code>

FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

```dockerfile
FROM ubuntu
RUN apt-get update
RUN apt-get install -y python python3-pip
RUN pip3 install flask

COPY app.py /opt/app.py

ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```



#### CMD and entrypoints

<img src="C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200727204022916.png" alt="image-20200727204022916" />

<img src="C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200727204106306.png" alt="image-20200727204106306" style="zoom:50%;" />





## docker compose

![image-20200728070119583](C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200728070119583.png)

## docker storage

you created data_volume under the volumes and you can then mount that volume to the read-write layer

using `-v data_volume:/var/lib/mysql` this is **volume mounting**



**bind mounting** is also possible by specifying a full path we can bind to any location within the docker host   

 ![image-20200728082931680](C:\Users\henri\AppData\Roaming\Typora\typora-user-images\image-20200728082931680.png)

