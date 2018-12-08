# Especifica a imagem base a ser utilizada pela nova imagem
FROM debian

# Especifica vários metadados para a imagem como o mantenedor. A especificação do mantenedor
# era feita usando a instrução específica, MAINTAINER que foi substituída pelo LABEL.
LABEL maintainer 'Victor Menegusso <victormenegusso@gmail.com>'

# Define argumentos que poderão ser informados ao build através do parâmetro --build-arg.
ARG BUCKET_ARG=files

# Especifica variáveis de ambiente a serem utilizadas durante o build.
ENV BUCKET_ENV=${BUCKET_ARG}