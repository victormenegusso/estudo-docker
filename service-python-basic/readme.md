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


## Problemas que tive:

Quando fui rodar o comando: ```sudo docker swarm init``` ocorreu o seguinte erro:
```Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on interface wlp8s0 (2804:d55:180e:8300:ade1:77be:e8e7:3c85 and 2804:d55:180e:8300:a6a:4137:ba82:961d) - specify one with --advertise-addr```

Para solucionar eu especifiquei o endereço
```sudo docker swarm init --advertise-addr 2804:d55:180e:8300:ade1:77be:e8e7:3c85```