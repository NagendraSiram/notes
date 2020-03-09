# Docker Commands
```bash
docker ps
docker ps -a (all stopped jobs)

docker run —name my-name -d -h "${hostname}” -p 80:80 my-app (name - running image name, d - detached, h - host, p - port mapping)
docker start my-app
docker stop my-app

docker images
docker rm image-id (remove history of running container)
docker rmi image-id (remove/delete downloaded image)
```
**Build & Tag**
```
docker build -t user/repo-name:v2 . (here . means it includes all the files in the image from the current directory)
docker tag image-id myresgistryhost:1212/fedora/httpd:v1

docker pull user/repo-name@sha256:cbbf2f9a99b47fc460d422812b6a5adff7dfee951d8fa2e4a98caa0382cfbdbf
docker push user/repo-name
```

**Delete all containers**
```
docker rm $(docker ps -a -q)
```

**Delete all images**
```
docker rmi $(docker images -q)
```
**Logon to docker container**
```
docker exec -it <image-id> /bin/bash
```
**Login to docker registery**
```
docker login
docker push
docker logout
```

# Docker Swarm Commands

**Init Swarm**
> docker swarm init —listen-addr 172.31.21.161:2377 —secret SAFC [172.31.21.161 is current m/c ip, SAFC password to join the swarm]

**Join Nodes**
> docker swarm join —secret SAFC 
              —ca-hash SHA256:837474 
                 172.31.21.161:2377 (main master 1 ip)
              —listen-adde 172.31.21.162:2377 (master 2

**Promote Node as Manager**
> docker node promote <id> 

**List Nodes**
> docker node ls 

**Create Service & Replicas**
```
docker service create --name <servicename> -P 8080:8080 --replicas 5 <imagename>
docker service ls
docker service tasks <servicename>
docker service inspect <servicename> - configuration
docker service rm <servicename>
docker service-scale <servicename>=7
            or
docker service update --replicas 7 <servicename>
docker node tasks <nodeid>
docker node tasks self
```

**Docker Compose (used to covert YML to DAB)**
```
docker-compose build
docker-compose bundle
```
**DAB (distributed application bundle)**
```
docker stack deploy <dabfilename>
docker stack tasks <dabfilename>
docker stack rm  <dabfilename>
```
