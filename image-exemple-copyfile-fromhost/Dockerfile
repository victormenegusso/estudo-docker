FROM nginx:1.13

LABEL maintainer 'Victor Menegusso <victormenegusso@gmail.com>'

# Executa ações/comandos durante o build dentro da imagem.
RUN echo '<h1>Sem conteúdo</h1>' > /usr/share/nginx/html/conteudo.html

# Copia arquivos e diretórios para dentro da imagem.
COPY *.html /usr/share/nginx/html/