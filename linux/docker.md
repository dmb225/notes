- [Build](build)
- [Cache](cache)
- [Registry](registry)
- [Run](run)
- [Tests](tests)
- [Troubleshooting]
- [Tutorials](tutorials)


# Build
```bash
docker build -t route_frontal_runtime --network host -f jobs/runtime.Dockerfile dist
```

# Cache

```bash
FROM slatedocs/slate:latest 
RUN apt update 
RUN apt install -y npm 
RUN npm install -g swagger-to-slate 
COPY add_rights.sh /srv/slate/ 
RUN chmod +x /srv/slate/add_rights.sh 


RUN apt install -y npm failed but docker finds npm it in its cache 
Package npm is not available, but is referred to by another package. 
This may mean that the package is missing, has been obsoleted, or 
is only available from another source 

E: Package 'npm' has no installation candidate 
The command '/bin/sh -c apt install -y npm' returned a non-zero code: 100 

=>

docker build --no-cache -t inframappy/mappyslate .  
```

# Registry

## Docker push/pull vs Docker save/load 

Pour info, le temps de push du docker  bikeEngine sur Dockerhub est de 2s, contre plus d'1 minute pour un docker save. Ce sera similaire pour ce qui est du docker pull vs docker load. 

C'est la même différence que faire git push vs faire un tar cf + copie du repo: docker push/pull ne synchronisent que les 'commits' (=layer docker) qui ne sont pas présents d'un côté ou de l'autre. 

Or en docker, ce qui prend de la place, ce sont surtout les 1ères layers, qui contiennent l'image de base (Ubuntu/Debian) et les quelques 'apt install' qu'on fait. Or ceux-ci ne changent pas, ou peu, et sont partagés par plein d'images Docker différentes (donc souvent déjà dispo sur les machines). C'est une des forces de Docker, on a en réalité pas grand-chose à synchroniser pour déployer une nouvelle version. D'où le résultat.


# Run

## Get terminal 

```bash
docker run -ti --entrypoint /bin/bash slatedocs/slate:latest

docker run --mount type=bind,source=/home/x2027539@ratpsmart.local/Projects/route-frontal/route-frontal.conf,target=/conf/route-frontal.conf --publish 9090:8889 --name route-frontal route_frontal_runtime

docker run --mount type=bind,source=/home/x2027539@ratpsmart.local/Projects/route-frontal/route-frontal.conf,target=/conf/route-frontal.conf --publish 9090:8889 --name route-frontal route_frontal_runtime >>/home/x2027539@ratpsmart.local/temp/log_route_frontal/logs 2>&1
```

# Tests

## Quick python test

```bash
docker run --rm -it debian:stretchw 
apt update 
apt install python3 
apt install python3-pip 
python3 -m pip install mypy 
python3 -c "from typing_extensions import AsyncContextManager; print(repr(AsyncContextManager))" 

Python 3.5.3 (default, Apr  5 2021, 09:00:41)  
[GCC 6.3.0 20170516] on linux 
Type "help", "copyright", "credits" or "license" for more information. 
 
>>> from typing_extensions import AsyncContextManager 
```

# Troubleshooting

## Permission denied 

```bash
Fix Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied 

sudo usermod -aG docker ${USER} 
su - ${USER} 
sudo chmod 666 /var/run/docker.sock 
sudo systemctl daemon-reload  
sudo service docker restart  
```
 

# Tutorials

[Understand and implement](https://guillaumebriday.fr/comprendre-et-mettre-en-place-docker)
[Extraire d'une image toutes les informations pour la reconstruire](https://blog.stephane-robert.info/post/docker-reverse-image)







