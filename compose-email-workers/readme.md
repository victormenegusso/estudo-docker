# Projeto de envio de emails com workers

**Estrutura do projeto:**

O projeto esta estruturado conforme a imagem:

![Alt text](arquitetura.png?raw=true "Arquitetura")

## Proxy Reverso

Utilizado para não expor todos os seviços, o unico serviço exposto é o serviço de front (nginx).
Quando o formulário é submetido, os dados vão para o nginx e o mesmo passa para o serviço app (python)

## Execução

**executar**

```bash
docker-compose up -d

# scalando o worker
docker-compose up -d --scale worker=3
```

**parar**

```bash
docker-compose down
```

**ver log**

```bash
docker-compose logs -f -t
```

## Override

Usei o arquivo 'docker-compose.override.yml' para sobreescrever uma variável de ambiente descrita no 'docker-compose.yml'
