# Redes

## tipos
- None Network -> container fica sem rede
- Bridge Network (*padrão*) -> ponte entre as interfaces de rede do container e da máquina host
- Host Network -> acesso direto a interface do host
- Overlay Network (*swarm*) -> para clusters

obs: *pode ser criadas novas redes*

## Comandos

listar os tipos:
```bash
docker network ls
```

## Exemplos

executando um container sem definir a rede e checando a sua configuração:

```bash
docker container run --rm alpine ash -c "ifconfig"

#saída demonstrando que contem rede
#eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
#          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
#          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
#          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:0
#          RX bytes:200 (200.0 B)  TX bytes:0 (0.0 B)

#lo        Link encap:Local Loopback
#          inet addr:127.0.0.1  Mask:255.0.0.0
#          UP LOOPBACK RUNNING  MTU:65536  Metric:1
#          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:1000
#          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

### None Network

`--net none`

O mesmo container do exemplo acima mas sem rede:


```bash
docker container run --rm --net none alpine ash -c "ifconfig"

# saída apenas a interface padrão (lo) sem acesso a rede
#lo        Link encap:Local Loopback
#          inet addr:127.0.0.1  Mask:255.0.0.0
#          UP LOOPBACK RUNNING  MTU:65536  Metric:1
#          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:1000
#          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

### Bridge Network

visualizar os dados da rede bridge

```bash
docker network inspect bridge

# saída
# ...
#            "Config": [
#                {
#                    "Subnet": "172.17.0.0/16",
#                   "Gateway": "172.17.0.1"
#               }
#            ]
# ...
```
todos os containers(bridge) vão estar dentro desta subrede.

#### Exemplo criando dois container que se comunicam via ping

```bash

# criando o container1
docker container run -d --name container1 alpine sleep 1000

# executando comando para ver a interface de rede do container1 ( modo interativo )
docker container exec -it container1 ifconfig

# saída ( nota que o container esta na subnet bridge)
#eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
#          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
#          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
#          RX packets:59 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:0
#          RX bytes:7943 (7.7 KiB)  TX bytes:0 (0.0 B)

#lo        Link encap:Local Loopback
#          inet addr:127.0.0.1  Mask:255.0.0.0
#          UP LOOPBACK RUNNING  MTU:65536  Metric:1
#          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:1000
#          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

# mesmos passos para o container 2
docker container run -d --name container2 alpine sleep 1000
docker container exec -it container2 ifconfig

# saída
#eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:03
#          inet addr:172.17.0.3  Bcast:172.17.255.255  Mask:255.255.0.0
#          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
#          RX packets:42 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:0
#          RX bytes:5550 (5.4 KiB)  TX bytes:0 (0.0 B)

#lo        Link encap:Local Loopback
#          inet addr:127.0.0.1  Mask:255.0.0.0
#          UP LOOPBACK RUNNING  MTU:65536  Metric:1
#         RX packets:0 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:1000
#          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)


# container 1 pingando container 2
docker container exec -it container1 ping 172.17.0.3

# container 1 pingando o google
docker container exec -it container1 ping www.google.com

```

### Bridge Network ( criando uma nova rede )

Demostrar que containers em redes diferentes não possuem acesso um com outro.

```bash
# criando a nova rede com o drive de bridge
docker network create --driver bridge rede_bridge_nova

# inspecionando nova rede
docker network inspect rede_bridge_nova

# saída ( uma subrede diferente da bridge )
# ...
#            "Config": [
#                {
#                   "Subnet": "172.19.0.0/16",
#                   "Gateway": "172.19.0.1"
#               }
#            ]
# ...

# criando o 3º container 
docker container run -d --name container3 --net rede_bridge_nova alpine sleep 1000

# ver as interface
docker container exec -it container3 ifconfig

# saída
#eth0      Link encap:Ethernet  HWaddr 02:42:AC:13:00:02
#          inet addr:172.19.0.2  Bcast:172.19.255.255  Mask:255.255.0.0
#          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
#          RX packets:76 errors:0 dropped:0 overruns:0 frame:0

# container 3 tentando pingar o container 2
docker container exec -it container3 ping 172.17.0.3

# saída ( não consegue )

# fazer o container3 tambem ter acesso a rede bridge ( padrão )
docker network connect bridge container3

# ver as interface ( com a nova bridge )
docker container exec -it container3 ifconfig

# saída 
#eth0      Link encap:Ethernet  HWaddr 02:42:AC:13:00:02
#          inet addr:172.19.0.2  Bcast:172.19.255.255  Mask:255.255.0.0
# ....
#eth1      Link encap:Ethernet  HWaddr 02:42:AC:11:00:04
#          inet addr:172.17.0.4  Bcast:172.17.255.255  Mask:255.255.0.0
# .... 


# container 3 pingar o container 2
docker container exec -it container3 ping 172.17.0.3

# saída (consegue pingar)


# removendo a conectividade com a rede bridge
docker network disconnect bridge container3

```

### Host Network

```bash
docker container run -d --name container4 --net host alpine sleep 1000

# ver as interface
docker container exec -it container3 ifconfig

# saída -> as mesmas interfaces que o host possui
```