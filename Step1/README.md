# Setup di un Docker Registry con Ansible

Questo playbook Ansible configura un **Docker Registry privato locale** su `localhost`, esponendolo sulla porta 5000.

---

## Cosa fa il playbook

- Avvia un container Docker con l’immagine ufficiale `registry:2`.
- Espone il registry sulla porta **5000** della macchina locale.
- Imposta il container per il riavvio automatico (`restart_policy: always`).

---

## Prerequisiti

- Docker installato sulla macchina locale.
- Ansible installato.
- Collection `community.docker` installata:

```bash
ansible-galaxy collection install community.docker
```
## Come usare

- Salva il playbook in un file, ad esempio docker-registry.yml.
- Esegui il playbook:

```bash
ansible-playbook docker-registry.yml
```

### Come funziona il task principale
```
- name: Avvia un container Docker registry
  community.docker.docker_container:
    name: registry
    image: registry:2
    state: started
    restart_policy: always
    published_ports:
      - 5000:5000
```
- Crea e avvia un container chiamato registry.
- Usa l’immagine ufficiale Docker Registry versione 2.
- Espone la porta 5000 del container sulla porta 5000 della macchina locale.
- Il container si riavvierà automaticamente in caso di arresto o riavvio del sistema.

### Verifica

Dopo l’esecuzione, puoi testare il registry con:
```
curl http://localhost:5000/v2/_catalog
```

Dovresti ricevere una risposta JSON che indica i repository presenti (inizialmente vuoti):
```
{"repositories":[]}
```