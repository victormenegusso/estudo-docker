## Comandos Básicos

lista informações sobre os containers em execução
```docker ps```

visualizar versão
```docker --version```

visualizar informações
```docker info```

lista imagens baixadas
```docker image ls```

executar uma imagem
```docker run {nome imagem}```

lista os Docker containers (running, all, all in quiet mode)
```
docker container ls
docker container ls --all
docker container ls -aq
```

parar um container
```docker container stop {CONTAINER ID}```

iniciando um service
```
    # inicia o swarm
    $ docker swarm init

    # Rodar o docker
    $ docker stack deploy -c docker-compose.yml getstartedservice
```

listando as services
```docker service ls```

status de cada replica
```docker service ps {NAME SERVICE}```

parando a service

```
    docker stack rm {NAME SERVICE}
    docker swarm leave --force
```