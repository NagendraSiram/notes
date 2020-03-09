# Tools

##### Java Memory Analysis

- Eclipse Memory Analyzer - Heap Dumps (.hprof)
- JVisual VM
- GC Viewer
- IBM

##### Intellj Pluggins
- Plant Uml
- Sonarlint


# Java Commands

To run a main program that is bundled in a jar file

> %JAVA_HOME%\bin\java –jar application.jar

To run a main program that is bundled in a jar file which has other dependency jars present in dependency directory

> %JAVA_HOME%\bin\java -cp application.jar;./dependency/* com.company.apps.MainApplication

> %JAVA_HOME%\bin\java –cp ".;application.jar;config.properties;" com.company.apps.MainApplication

> %JAVA_HOME%\bin\java -cp ".;mysql-connector-java-5.0.8-bin.jar" TestDriver

_Note: For Unix use : instead of ; _

**DEBUG**

> java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005 -jar application.jar

# Git Commands

**Migrating Git**
> git clone —bare ssh://something.com/com/home/project.git

> git push —mirror https://github.com/project.git

**Amend the message**
```
git commit --amend -m "new message"
```
**Amend the files**
```
git commit --amend
```
**Logs**
```
gl
git log --stat
git reflog
```

**Remove untracked directories and files**
```
git clean -df
```
**To revert all local changes in case you haven’t actually committed** 
```
git reset --hard HEAD 
```

**Undoing bad commits (when you haven't pushed any changes to repo)**
```
git reset --soft number (previous committed files will be in staging area)
git reset number (previous committed files will be in un-tracked section) 
git reset --hard number (previous committed files are completely removed)
```
**Revert bad commits  (which other users already pulled committed changes)**  
```
 git revert number (reverts only the commit number specified) 
```
**Cherry pick commits from other branch**
```
git cherrypick number
```
**Tag a release**
```
git tag -a release-xx -m 'for version xx'

git push origin --tags

git tag -a release-xx 640bf0 -m 'for version xx' (Tag older commit)

git tag -d release-xx (delete a tag)
```
**Git Stash Commands**
 ```
git stash list [<options>]
git stash show [<stash>]
git stash drop [-q|--quiet] [<stash>]
git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
git stash branch <branchname> [<stash>]
git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
         [-u|--include-untracked] [-a|--all] [<message>]]
git stash clear
git stash create [<message>]
git stash store [-m|--message <message>] [-q|--quiet] <commit>  
```


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
