# Create a new docker network "my_network" using bridge driver
1- sudo docker network create  --driver bridge my_network
de8ac3020a3eecf1f26093ef1d89516e217f2df42e3a00b30773661b96feff5f

2- sudo docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
de8ac3020a3e   my_network        bridge    local

# Create a new docker container using "nginx" image and connect it to the "my_network" and name it nginx_container.
1- sudo docker run --name nginx_container -p 8080:80 --network my_network nginx

2- sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                   NAMES
c8e299c57400   nginx     "/docker-entrypoint.…"   7 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   nginx_container

# Verify it on browser
1- its verified
http://localhost:8080
giving "welcome to nginx"

# Create a new docker container using "httpd" image and connect in to the"my_network" and name it httpd_container.
1- sudo docker run --name httpd_container -p 8081:80 --network my_network httpd

# verify it on browser
1- http://localhost:8081
giving "its works" message

# use the "docker network inspect" to display information about the "my_network".
1- sudo docker network inspect my_network
[
    {
        "Name": "my_network",
        "Id": "de8ac3020a3eecf1f26093ef1d89516e217f2df42e3a00b30773661b96feff5f",
        "Created": "2023-03-20T22:50:33.803989622-04:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
 
# Stop and remove the nginx_container
1- sudo docker stop nginx_container
nginx_container

2- sudo docker rm nginx_container
nginx_container

# Create a new docker container from "nginx" image and connect it with "my_network" and name it "nginx_container".
1- sudo docker run --name nginx_container2 -p 8082:80 --network my_network nginx

# verify on browser
1- http://localhost:8082
giving "Welcome to nginx!" message 

# use "docker container ls" command to display information about all running container.
1- sudo docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                   NAMES
643fb71ee635   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 2 minutes   0.0.0.0:8082->80/tcp, :::8082->80/tcp   nginx_container2

# Stop and remove all containers.
1- sudo docker stop 643fb71ee635

2- sudo docker rm 643fb71ee635
643fb71ee635

# Remove the "my_network" from network
1- sudo docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
c5b1597c5219   bridge            bridge    local
94eccef4817c   docker_gwbridge   bridge    local
b98d3a4dbcdd   host              host      local
ijkeltdk1436   ingress           overlay   swarm
de8ac3020a3e   my_network        bridge    local
c587d5a4d982   none              null      local

2- sudo docker network rm de8ac3020a3e
de8ac3020a3e

3- sudo docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
c5b1597c5219   bridge            bridge    local
94eccef4817c   docker_gwbridge   bridge    local
b98d3a4dbcdd   host              host      local
ijkeltdk1436   ingress           overlay   swarm
c587d5a4d982   none              null      local

# push the code the code base to the github 
