FROM ubuntu:16.04

# Update & openssh
RUN apt-get update \
    && apt-get install -y openssh-server 

   
# # Install sudo 
# RUN apt-get update && apt-get install -y sudo

# # Aggiungi utente genericuser ai sudoers  e mkdir 
# RUN useradd -m -s /bin/bash genericuser && \
#     mkdir -p /etc/sudoers.d && \
#     echo 'genericuser ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/genericuser && \
#     chmod 440 /etc/sudoers.d/genericuser \
#     && mkdir -p /home/genericuser/.ssh/



# COPY id_key_genericuser.pub  /home/genericuser/.ssh/authorized_keys

# # Gestire permessi e prorpretari 
# RUN chown -R genericuser:genericuser /home/genericuser \
#     && chmod 700 /home/genericuser/.ssh \
#     && chmod 600 /home/genericuser/.ssh/authorized_keys \
#     && chown -R genericuser:genericuser /home/genericuser/.ssh \
#     && chown genericuser:genericuser /home/genericuser/.ssh/authorized_keys

# # Configure SSH to allow key-based authentication
# RUN mkdir /var/run/sshd && \
#     sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config && \
#     sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config && \
#     sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
#     echo 'AllowUsers genericuser' >> /etc/ssh/sshd_config
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
