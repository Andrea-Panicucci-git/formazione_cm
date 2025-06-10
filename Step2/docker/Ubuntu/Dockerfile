FROM ubuntu:16.04

# Update & openssh
RUN apt-get update \
    && apt-get install -y openssh-server 

   
# Install sudo 
RUN apt-get update && apt-get install -y sudo

# Aggiungi utente genericuser ai sudoers  e mkdir 
RUN useradd -m -s /bin/bash vagrant && \
    mkdir -p /etc/sudoers.d && \
    echo 'vagrant ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/vagrant && \
    chmod 440 /etc/sudoers.d/vagrant \
    && mkdir -p /home/vagrant/.ssh/



COPY key/id_rsa.pub  /home/vagrant/.ssh/authorized_keys

# Gestire permessi e prorpretari 
RUN chown -R vagrant:vagrant /home/vagrant \
    && chmod 700 /home/vagrant/.ssh \
    && chmod 600 /home/vagrant/.ssh/authorized_keys \
    && chown -R vagrant:vagrant /home/vagrant/.ssh \
    && chown vagrant:vagrant /home/vagrant/.ssh/authorized_keys

# Configure SSH to allow key-based authentication
RUN mkdir /var/run/sshd && \
    sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config && \
    sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
    echo 'AllowUsers vagrant' >> /etc/ssh/sshd_config
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
