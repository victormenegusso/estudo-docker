# notas

## build imagem

- no docker file, toda linha(comando) gera um novo layer, logo comandos que possam mudar com frequencia, deixamos nas ultimas linhas, pois durante o build se os layers anteriores não forem modificados, os mesmos não precisam ser "re-compilados"

- quando é necessario executar varios scripts no `RUN`: 
```bash
RUN useradd www && \
  mkdir /app && \
  mkdir /log && \
  chown www /log
```