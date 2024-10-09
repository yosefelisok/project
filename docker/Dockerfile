# Dockerfile для тестового окружения
FROM ubuntu:24.04

# Установка OpenSSH Server
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    curl \
    && apt-get clean

# Создание папки для SSH
RUN mkdir /var/run/sshd

# Настройка пользователя и пароля
RUN useradd -rm -d /home/devops -s /bin/bash -g root -G sudo -u 1000 devops && \
    echo 'devops:password' | chpasswd

# Настройка SSH
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
    echo "UseDNS no" >> /etc/ssh/sshd_config

EXPOSE 22 80

CMD ["/usr/sbin/sshd", "-D"]

