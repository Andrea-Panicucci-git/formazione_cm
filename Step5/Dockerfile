FROM jenkins/jenkins:lts-jdk17

USER root

# Installa Docker CLI (senza daemon)
RUN apt-get update && apt-get install -y docker.io

USER jenkins
