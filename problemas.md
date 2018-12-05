# Problemas que tive:

## permissão
Todo momento tinha que colocar sudo ( para não precisar estar como root ), para solucinar:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

## services
Quando fui rodar o comando: ```sudo docker swarm init``` ocorreu o seguinte erro:
```Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on interface wlp8s0 (2804:d55:180e:8300:ade1:77be:e8e7:3c85 and 2804:d55:180e:8300:a6a:4137:ba82:961d) - specify one with --advertise-addr```

Para solucionar eu especifiquei o endereço
```sudo docker swarm init --advertise-addr 2804:d55:180e:8300:ade1:77be:e8e7:3c85```