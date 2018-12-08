# Exemplo de build de imagem com argumentos

Exemplo de imagem que pode receber como parametro um argumento chamado `BUCKET_ARG`

**Build sem arg**
```bash

docker image build -t ex-build-arg .
docker container run ex-build-arg bash -c 'echo $BUCKET_ENV' 

# Saída esperada:
files
```

**Build com arg**
```bash

docker image build --build-arg BUCKET_ARG=myapp -t ex-build-arg .
docker container run ex-build-arg bash -c 'echo $BUCKET_ENV' 

# Saída esperada:
myapp
```