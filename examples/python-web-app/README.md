# To run a Django app on container

Just clone the below repository

```
```

**Move to the below folder path**

```
cd /home/ubuntu/DockerZeroToHero/examples/python-web-app
docker build .
docker images
```

**To run a container**

```
docker run -it <imageid>
```

![image](https://github.com/kohlidevops/DockerZeroToHero/assets/100069489/14f2eeb1-bebe-4b60-8c03-98b315e05161)

Container is running with port 8000. but i cant able to access the application from outside. Because port mapping is missing.

**To run a container with port mapping**

```
docker run -p <EC2Port>:<ContainerPort> -it <imageid>
docker run -p 9000:8000 -it <imageid>
```

![image](https://github.com/kohlidevops/DockerZeroToHero/assets/100069489/aa6c29e3-9946-4538-ab4a-880ea3e25a09)

**Now I can able to access the application from outside**

![image](https://github.com/kohlidevops/DockerZeroToHero/assets/100069489/d772e0a5-1128-40c2-b79c-f203e142ba60)

