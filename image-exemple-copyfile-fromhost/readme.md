# Instruções para povoamento da imagem
Exemplo de build de imagem, que copia o arquivo `index.html` para dentro da imagem

```bash
docker image build -t ex-build-copy .
docker container run -p 80:80 ex-build-copy 
```