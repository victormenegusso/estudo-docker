# Exemplo de Service

Este service utiliza o container criado/publicado 'container-python-basic'
O arquivo 'docker-compose.yml' indica para o docker como configurar/rodar/escalar o servico ( container: container-python-basic)

## Executando

```
    # inicia o swarm
    $ docker swarm init

    # Rodar o docker
    $ docker stack deploy -c docker-compose.yml getstartedservice

    # listando as services
    $ docker service ls

    # status de cada replica
    $ docker service ps getstartedservice_web

```

## parando

```
    docker stack rm getstartedservice
    docker swarm leave --force
```