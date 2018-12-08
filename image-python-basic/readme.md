# Container python

## Arquivos

    - Dockerfile -> indica como criar a imagem
    - requirements.txt -> indica as bibliotecas de python que serão instaladas no comando `RUN pip install --trusted-host pypi.python.org -r requirements.txt`
    - app.py -> aplicativo em python que vai rodar no container

## Executando

```
    # cria a imagem docker com o nome 'friendlyhello'
    $ docker build -t friendlyhello .

    # executa a imagem ( o -p 4000:80 mapeia a porta 80 do container para porta 4000  do host)
    $ docker run -p 4000:80 friendlyhello

    # executa em 'detached mode'
    docker run -d -p 4000:80 friendlyhello

```

## Registrando a imagem ( na conta do docker )

```
    # logar na conta
    $ docker login

    # registra a tag 'docker tag {NOME IMAGEM} {user}/{REP}:{TAG}' ( semelhante a uma branch do git )
    $ docker tag friendlyhello victormenegusso/container-python-basic:part1

    #publica a imagem 'docker push username/repository:tag'
    $ docker push victormenegusso/container-python-basic:part1

    # Pull and run the image from the remote repository ( se não esta na maquina o docker baixa automaticamente)
    docker run -p 4000:80 victormenegusso/container-python-basic:part1

``` 