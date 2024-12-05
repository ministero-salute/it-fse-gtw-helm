[![en](https://img.shields.io/badge/lang-en-red.svg)](README.en.md)


# Fascicolo Sanitario 2.0

# Servizi da Installare

Di seguito la lista dei servizi da installare:

- [*it-fse-gtw-config*](https://github.com/ministero-salute/it-fse-gtw-config)
- [*it-fse-gtw-rules-manager*](https://github.com/ministero-salute/it-fse-gtw-rules-manager)
- [*it-fse-gtw-dispatcher*](https://github.com/ministero-salute/it-fse-gtw-dispatcher)
- [*it-fse-gtw-validator*](https://github.com/ministero-salute/it-fse-gtw-validator)
- [*it-fse-gtw-fhir-mapping-engine*](https://github.com/ministero-salute/it-fse-gtw-fhir-mapping-engine)
- [*it-fse-gtw-indexer*](https://github.com/ministero-salute/it-fse-gtw-indexer)
- [*it-fse-gtw-ini-client*](https://github.com/ministero-salute/it-fse-gtw-ini-client)
- [*it-fse-gtw-garbage*](https://github.com/ministero-salute/it-fse-gtw-garbage)
- [*it-fse-gtw-status-check*](https://github.com/ministero-salute/it-fse-gtw-status-check)
- [*it-fse-gtw-status-manager*](https://github.com/ministero-salute/it-fse-gtw-status-manager)

# Steps per Installare il Gateway Distribuito

## Definire il Secret nel Cluster

```bash
kubectl create secret docker-registry name-secret-registry --docker-server=registry-to-use --docker-username=userPull --docker-password=userPassword
```
Questo comando crea un secret in Kubernetes chiamato `name-secret-registry`, che contiene le credenziali per l'accesso al Docker registry.<br>
Il secret memorizza il **docker-server**, **docker-username** e **docker-password**, informazioni necessarie a Kubernetes per autenticarsi e scaricare le immagini Docker dal registry specificato.<br>

### Analisi del Comando:
- **kubectl**: La  command line utilizzata per interagire con un cluster Kubernetes.
- **create secret docker-registry**: Crea un secret che memorizza le credenziali per l'accesso a un Docker registry.
- **name-secret-registry**: Questo è il nome del secret che viene creato. In questo caso, il secret si chiama `name-secret-registry`.
- **--docker-server=registry-to-use**: Specifica l'URL del Docker registry con cui autenticarsi (ad esempio, Docker Hub, un registry privato, ecc.). Sostituisci `registry-to-use` con l'URL effettivo del registry (ad esempio, `https://index.docker.io/v1/` o l'URL di un registry privato).
- **--docker-username=userPull**: Il nome utente utilizzato per l'autenticazione con il Docker registry. Sostituisci `userPull` con il nome utente effettivo per accedere al registry.
- **--docker-password=userPassword**: La password associata al nome utente Docker specificato (`userPull`). Sostituisci `userPassword` con la password effettiva o con un token di accesso.

**Esempio di utilizzo:**<br>
__Il secret azregdevops verrà utilizzato durante la fase di installazione, ma puoi sostituire questo valore con quello che hai scelto durante la fase di creazione del secret__
```bash
kubectl create secret docker-registry azregdevops --docker-server=registry-to-use --docker-username=userPull --docker-password=userPassword
```

## Helm Repository Management

I seguenti comandi possono essere utilizzati per cercare e recuperare una versione specifica di uno dei servizi menzionati sopra:

```bash
helm repo add fse https://ministero-salute.github.io/it-fse-gtw-helm
helm repo update fse
helm search repo fse/it-fse-gtw-rules-manager --versions
```

| Name                        | Chart Version | App Version | Description                              |
|-----------------------------|---------------|-------------|------------------------------------------|
| fse/it-fse-gtw-rules-manager | 0.1.0         | xxx       | servizio del Fascicolo Sanitario Elettronico 2.0 |
| ...                         | ...           | ...         | ...                                      |

Il comando ```helm search``` può essere utilizzato per recuperare l'ultima versione di ciascun servizio.

<br>

È importante aggiornare il repository prima di eseguire la ricerca con il seguente comando:
```bash
helm fetch repo fse/it-fse-gtw-rules-manager --versions
```

```bash
helm repo update fse
```

**Per scaricare una versione specifica:**
```bash
helm fetch <nome-repo>/<nome-chart> --version <versione-chart> 
```

Esempio di utilizzo:<br>
**Per scaricare la versione 0.1.0 elencata dal comando di ricerca per il servizio it-fse-gtw-rules-manager:**

```bash
helm fetch fse/it-fse-gtw-rules-manager --version 0.1.0
```

Questo comando scarica il pacchetto che potrà essere utilizzato successivamente nella fase di installazione.


---
## Guida all'installazione del servizio:

1. [*it-fse-gtw-config*](it-fse-gtw-config/installation-guide.md)<br>
2. [*it-fse-gtw-rules-manager*](it-fse-gtw-rules-manager/installation-guide.md)<br>
3. [*it-fse-gtw-dispatcher*](it-fse-gtw-dispatcher/installation-guide.md)<br>
4. [*it-fse-gtw-validator*](it-fse-gtw-validator/installation-guide.md)<br>
5. [*it-fse-gtw-fhir-mapping-engine*](it-fse-gtw-fhir-mapping-engine/installation-guide.md)<br>
6. [*it-fse-gtw-indexer*](it-fse-gtw-indexer/installation-guide.md)<br>
7. [*it-fse-gtw-ini-client*](it-fse-gtw-ini-client/installation-guide.md)<br>
8. [*it-fse-gtw-garbage*](it-fse-gtw-garbage/installation-guide.md)<br>
9. [*it-fse-gtw-status-check*](it-fse-gtw-status-check/installation-guide.md)<br>
10. [*it-fse-gtw-status-manager*](it-fse-gtw-status-manager/installation-guide.md)<br>
---

## Verifica le Risorse create

### Pods

```bash
kubectl get pods
```
Esempio di output:

| NAME                                      | READY | STATUS  | RESTARTS | AGE |
|-------------------------------------------|-------|---------|----------|-----|
| it-fse-gtw-status-manager-845ccdf5dc-7jw7t | 0/1   | Running | 1        | 24s |

### ConfigMaps

```bash
kubectl get cm
```

Esempio di output:

| NAME                              | DATA | AGE |
|-----------------------------------|------|-----|
|it-fse-gtw-config-cm               | 1    | 10m |
|it-fse-gtw-dispatcher-cm           | 2    | 10m |
|it-fse-gtw-fhir-mapping-engine-cm  | 1    | 10m |
|it-fse-gtw-garbage-cm              | 1    | 10m |
|it-fse-gtw-indexer-cm              | 2    | 10m |
|it-fse-gtw-ini-client-cm           | 4    | 10m |
|it-fse-gtw-rules-manager-cm        | 2    | 10m |
|it-fse-gtw-status-check-cm         | 1    | 10m |
|it-fse-gtw-status-manager-cm       | 2    | 10m |
|it-fse-gtw-validator-cm            | 2    | 10m |


### Kubernetes Secrets

```bash
kubectl get secrets
```

Esempio di output:

| NAME                     | TYPE                                | DATA | AGE  |
|--------------------------|-------------------------------------|------|------|
| azregdevops               | kubernetes.io/dockerconfigjson     | 1    | 14d  |
| kafka-secret              | Opaque                              | 16   | 111m |
| mongo-secret              | Opaque                              | 18   | 111m |
| pswcertclient-secret      | Opaque                              | 2    | 111m |
| ********************      | ********************                | ***  | *** |
```
