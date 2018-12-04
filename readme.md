# Estudo docker

Repositório para armazenar exemplos / textos sobre o docker

## INIT

https://docs.docker.com/get-started/
https://docs.docker.com/get-started/part2/#share-your-image

## Conceitos Básicos

    Engine de administração de containers.
    Containers compartilham o kernel da maquina host.
    Utiliza os serviços do LXC (Linux Containers)
    Possui vários níveis de isolamento ( cpu, memória, rede...)

### Containers vs MV

    Possui várias vantagens de uma maquina virtual
    Consome menos recursos
    Velocidade de boot maior

### Images e containers
    
    Imagem é um pacote que contem tudo oque sua aplicação precisa para executar, o conteiner é o local onde sua imagem executa.

    Container 
        tem o seu proprio sistema de arquivos.
    
    Imagem
        Modelo de sistema de arquivos usado para criar o container
        Composta por 1 ou mais layers (camadas) [representa 1 ou mais mudanças no sistema de arquivos]
        Cada layer é resentado como uma sub imagem ( facilita no reuso, caso eu tenha mais imagens basiadas em uma imagem X, a imagem X não fica duplicada)
        Somente a ultima layer pode ser alterada

### Services

    https://docs.docker.com/get-started/part3/#introduction 

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


## Problemas que tive:

### permissão
Todo momento tinha que colocar sudo ( para não precisar estar como root ), para solucinar:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

### services
Quando fui rodar o comando: ```sudo docker swarm init``` ocorreu o seguinte erro:
```Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on interface wlp8s0 (2804:d55:180e:8300:ade1:77be:e8e7:3c85 and 2804:d55:180e:8300:a6a:4137:ba82:961d) - specify one with --advertise-addr```

Para solucionar eu especifiquei o endereço
```sudo docker swarm init --advertise-addr 2804:d55:180e:8300:ade1:77be:e8e7:3c85```