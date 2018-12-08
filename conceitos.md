# Conceitos Básicos

    Engine de administração de containers.
    Containers compartilham o kernel da maquina host.
    Utiliza os serviços do LXC (Linux Containers)
    Possui vários níveis de isolamento ( cpu, memória, rede...)

## Containers vs MV

    Possui várias vantagens de uma maquina virtual
    Consome menos recursos
    Velocidade de boot maior

## Images e containers
    
    Imagem é um pacote que contem tudo oque sua aplicação precisa para executar, o conteiner é o local onde sua imagem executa.

    Container 
        tem o seu proprio sistema de arquivos.
    
    Imagem
        Modelo de sistema de arquivos usado para criar o container
        Composta por 1 ou mais layers (camadas) [representa 1 ou mais mudanças no sistema de arquivos]
        Cada layer é resentado como uma sub imagem ( facilita no reuso, caso eu tenha mais imagens basiadas em uma imagem X, a imagem X não fica duplicada)
        Somente a ultima layer pode ser alterada

    

## Services

    https://docs.docker.com/get-started/part3/#introduction 

## Coordenado Multiplos containers 

Docker Compose -> arquivo que descreve varias imagens, e atraves dele podemos executar um ambiente completo, com imagens de banco de dados, imagens com a aplicação, etc.
