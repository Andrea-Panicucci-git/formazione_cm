# Esercizio Step 3 - Build, Push & Run Containers con Registry Locale

Questo esercizio ha lo scopo di automatizzare la **costruzione**, **pubblicazione** e **esecuzione** di immagini Docker personalizzate (`Ubuntu` e `Alpine`) tramite **Ansible**, utilizzando un **Docker Registry privato locale** (`localhost:5000`).

---

## Prerequisiti

- Docker installato e funzionante
- Ansible installato
- Ruolo `community.docker` installato:

  ```bash
  ansible-galaxy collection install community.docker
  ```
---

## Cosa fa il Playbook

1. Rileva l’engine container:

Verifica se è presente docker o podman.

2. Costruisce le immagini:
```bash
my_ubuntu_ssh da ./path/to/Ubuntu
my_alpine_ssh da ./path/to/Alpine
```
3. Effettua il push al registry locale:
```bash
localhost:5000/my_ubuntu_ssh:latest
localhost:5000/my_alpine_ssh:latest
```
4. Esegue i container pubblicati:
```bash 
Ubuntu: esposto sulla porta 8080
Alpine: esposto sulla porta 8081
```
## Verifica



### Visualizza le immagini nel registry:

```bash
curl http://localhost:5000/v2/_catalog
 Visualizza i tag di una immagine:
curl http://localhost:5000/v2/my_ubuntu_ssh/tags/list
```
### Verifica i container attivi:
```bash 
docker ps 
```

## Pulizia (opzionale)
```bash 

docker stop registry
docker rm registry
docker rmi localhost:5000/my_ubuntu_ssh localhost:5000/my_alpine_ssh
docker container rm -f my_ubuntu_ssh my_alpine_ssh
```