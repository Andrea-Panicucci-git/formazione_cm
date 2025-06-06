FROM alpine:3.18

# Installare bash, sudo, openssh e altri tool
RUN apk update && apk add --no-cache \
    bash \
    sudo \
    openssh

# Creare utente genericuser con bash
# RUN adduser -D -s /bin/bash genericuser && \
#     echo "genericuser ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/genericuser && \
#     chmod 440 /etc/sudoers.d/genericuser

# # Configurare SSH: creare directory e copiare chiave pubblica
# RUN mkdir -p /home/genericuser/.ssh && chown genericuser:genericuser /home/genericuser/.ssh

# COPY id_key_genericuser.pub /home/genericuser/.ssh/authorized_keys

# RUN chown genericuser:genericuser /home/genericuser/.ssh/authorized_keys && \
#     chmod 700 /home/genericuser/.ssh && \
#     chmod 600 /home/genericuser/.ssh/authorized_keys

# # Configurare sshd
# RUN mkdir -p /run/sshd && \
#     sed -i 's/#PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config && \
#     sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config && \
#     sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
#     echo 'AllowUsers genericuser' >> /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]