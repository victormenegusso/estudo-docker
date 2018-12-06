# Comandos

## Comandos Básicos

visualizar versão:

```bash
docker --version
```

visualizar informações:

```bash
docker info
```

### listagem
lista informações sobre os containers em execução:
```bash
docker ps
```

lista imagens baixadas:
```bash
docker image ls
```

lista os Docker containers (running, all, all in quiet mode):

```bash
docker container ls
docker container ls --all
docker container ls -aq
```

### Execução -> comando 'run'
executar uma imagem:
```bash
docker run {nome imagem}
```
obs: o comando run sempre cria um novo container e é um grupo de comandos basicos:

```bash
# Download automático das imagens não encontradas:
docker pull

# Criação do container
docker create

# Execução do container
docker start

# Uso do modo interativo
docker exec
```

executar uma imagem ( excuindo o container logo em seguida):
```bash
docker run -rm {nome imagem}
```

executar container em modo interativo
```bash
docker container run -it
docker container start -ai
docker container exec -t

#exemplo
docker container run -it debian bash
```

Dar nome a um container

```bash
docker container run --name {NOME} {nome imagem}

# exemplo
docker container run --name mydeb -it debian bash
```

### Execução -> comando 'start'

diferente do run que chega baixar, criar e executar o container, start só executa 

```bash
docker container start {name container}

#exemplo
docker container start -ai mydeb
```

### Parar um container

parar um container:
```bash
docker container stop {CONTAINER ID}
```

### Mapeamento de porta

O mapeamento de portar entre o container e a máquina host é feito atraves da flag `-p {PORTA HOST}:{PORTA CONTAINER}` 
```bash
#exemplo
docker container run -p 8080:80 nginx
```

## Comandos para Services

iniciando um service:
```bash
# inicia o swarm
$ docker swarm init

# Rodar o docker
$ docker stack deploy -c docker-compose.yml getstartedservice
```

listando as services:
```bash
docker service ls
```

status de cada replica:
```bash
docker service ps {NAME SERVICE}
```

parando a service:

```bash
    docker stack rm {NAME SERVICE}
    docker swarm leave --force
```