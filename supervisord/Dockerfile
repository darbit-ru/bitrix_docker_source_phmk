FROM ubuntu:20.04

RUN apt-get update \
    && apt-get install -y supervisor

# Установка необходимых пакетов для Docker CLI
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Добавляем GPG ключ для Docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Добавляем Docker репозиторий
RUN echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

# Установка Docker CLI
RUN apt-get update && apt-get install -y docker-ce-cli

COPY ./conf/supervisor/messanger.conf /etc/supervisor/conf.d/messanger.conf
COPY ./conf/supervisor/worker.conf /etc/supervisor/conf.d/worker.conf
# COPY ./conf/supervisor/supervisord.conf /etc/supervisor/supervisord.conf

CMD ["supervisord", "-n"]
