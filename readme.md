# Estudo docker

Repositório para armazenar exemplos / textos sobre o docker

## INIT

https://docs.docker.com/get-started/
https://docs.docker.com/get-started/part2/#share-your-image

## Conceitos Básicos

    Containers compartilham o kernel da maquina host


### Images e containers
    
    Imagem é um pacote que contem tudo oque sua aplicação precisa para executar, o conteiner é o local onde sua imagem executa.

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

