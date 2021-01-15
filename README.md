# Docker
# To list all runing container
    docker container ls (new way) = docker ps (old way)
# To Show all containers (default shows just running)
    docker container ls -a

# To remove container
    doccker container rm {conainer ID}
# To run stop container
    docker container start {container ID}
# To stop container
    docker container stop {container ID}
# To run container with detached (-d) {run container in background}
    docker container run -d ubuntu sleep 30
# To run container and go inside to container (-it i=interactive, t=tty) 
    docker container run -it ubuntu /bin/bash
# To exit container but container keeps run, use => (ctrl + p + q), not => (ctrl+d) 
# To Delete all containers at once
    docker container rm $(docker container ls -aq)
# To show all information of container
    docker dontainer inspact {container ID}

# Port Maping and Forwarding
    docker container run -d -p 3600:80 nginx --name {define container name}

# Shell access to ontainer
    docker containerr exec -it {conainer ID} /bin/bash
# To change runing container name
    docker container rename {container ID} {new name}
# To restart container 
    docker container restart {container ID}
# To attach runing container
    docker container attach {container ID}
    it will attach runing container to terminal
# To kill
    docker container kill {container ID}
# Wait 
    docker container wait {container ID}
    it will wait to stop container and show exit status of contaier
# pause 
    docker container pause {container ID}
    it will stop all services and can not access it
    docker container unpause {container ID}
# create 
    it will create container only while run command pull img and then create container
    then will command that you passed run container.
    docker container create ubuntu sleep 60
# Diff
    docker container diff {container ID}
    Inspect changes to files or directories on a container’s filesystem
# Export Container
    docker container export >my_ubuntu.tar
    docker container export >{any name you like}.tar
                    or
    docker container export -o my_ubuntu.tar
# Import or create img from .tar file
    docker image import my_ubuntu.tar {img name}
    to container newly imported img use "docker container run -it {img name} /bin/bash"
# creating img form runing container
    docker container commit --author "Taha Khan" -m "this is test commit" {container ID} {new image name}
    docker image ls (new imge should be in list)

# Docker File
    FROM ubuntu:16.04 (this name of base img)
    "docker image build -t myubuntu:1 ." => this will create img from docker file "." means docker file is in current working directory.
    "docker image ls " you img should be there. 

# Persist Data
    data persist in docker has two main methods 
    1)volume
    2)bind mount
    3)tempfs mount
# To list all volums
    docker volume ls

# To create volume 
    docker create volume {volume name}
# To remove volume
    docker volume rm {volume name}
    can not delete any volume if its container is present either runing condition or exited.
# To remove all unused volums
    docker volume prune 
# Bind mount
    in bind mount we can mount folder from host mechine into container.
    "docker container run -it -v /host_bind_folder:/temp/test ubuntu:14.04 bash"
    here we share /host_bind_folder with ubbuntu mechine, 
    host mechine path should be full path.other wise it will create volume
    to binding current folder
    "docker container run -it -v $(pwd):/temp/test ubuntu:14.04 bash"
                        OR
    "docker container run -it --mount type=bind,source=$(pwd),target=/temp/test/ ubuntu:14.04 absh"
# Docker Networking
    "docker network ls"
    to list networks, 
    by default every container use bridge network
# To inspact networks
    "docker network inspact bridge"

    "docker network create -d bridge test", it will create new network "test" with bridge driver
    "docker network ls" will list down newly created network.
    "ifconfig" on host mechine will show one more netwok having br in starting of name
    br means it is bridge network.
    "docker container run -it --network test ubuntu:14.04 bash" it will run container with specified network.
    "ifconfig" can see eth0, then "ifconfig" on host will show veth network
    once container stop "veth" on host mechine will not be present.
    

     

