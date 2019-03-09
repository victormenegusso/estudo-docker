# Comunicação entre dois Services de compose files diferentes

## intro
Contexto, dois projetos (compose-container-a e compose-container-n) cada um com o seu 'docker-compose.yml' e eles precisam se comunicar entre si.

Quando iniciamos os container via compose, a rede é visivel apenas pelos services do arquivo de compose: https://docs.docker.com/compose/networking/

Para dois projetos se conversarem, eles precisam estar na mesma rede.
Para isso, criamos uma rede 'network_tests_comunication'

E no compose de cada projeto colocamos que vamos utilizar uma rede externa
https://docs.docker.com/compose/networking/#use-a-pre-existing-network
```Dockerfile
....
networks:
  network_tests_comunication:
    external: true
....
```



## Criando a Rede
```bash
docker network create network_tests_comunication
```

## Executando os containers
```bash
cd compose-container-a
sudo docker-compose up -d 

cd compose-container-b
sudo docker-compose up -d 
```

## Executando os comandos de ping
```bash
#command -> container A pingando container B
docker container exec -it compose-container-a_container-a_1 ping container-b

#log
PING container-b (172.26.0.3): 56 data bytes
64 bytes from 172.26.0.3: seq=0 ttl=64 time=0.095 ms
64 bytes from 172.26.0.3: seq=1 ttl=64 time=0.264 ms
64 bytes from 172.26.0.3: seq=2 ttl=64 time=0.172 ms
64 bytes from 172.26.0.3: seq=3 ttl=64 time=0.143 ms
64 bytes from 172.26.0.3: seq=4 ttl=64 time=0.405 ms
64 bytes from 172.26.0.3: seq=5 ttl=64 time=0.152 ms
64 bytes from 172.26.0.3: seq=6 ttl=64 time=0.100 ms

```

```bash
#command -> container B pingando container A
docker container exec -it compose-container-b_container-b_1 ping container-a

#log
PING container-a (172.26.0.2): 56 data bytes
64 bytes from 172.26.0.2: seq=0 ttl=64 time=0.155 ms
64 bytes from 172.26.0.2: seq=1 ttl=64 time=0.146 ms
64 bytes from 172.26.0.2: seq=2 ttl=64 time=0.116 ms
64 bytes from 172.26.0.2: seq=3 ttl=64 time=0.210 ms
64 bytes from 172.26.0.2: seq=4 ttl=64 time=0.274 ms

```


