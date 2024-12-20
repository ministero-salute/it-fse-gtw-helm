# it-fse-gtw-helm

Il repository **it-fse-gtw-helm** contiene i chart Helm relativi ai servizi connessi al **Fascicolo Sanitario Elettronico (FSE)**, in particolare il **Gateway Distruito**.

## Prerequisiti

Prima di procedere con l'installazione, assicurati di avere:

1. **Cluster Kubernetes** configurato e funzionante.
2. **Helm** installato (versione 3 o superiore).
3. **Oggetti ConfigMap e Secret** necessari creati nel namespace di destinazione.
4. **Event Hub e Cosmos DB ** su Azure, poiché sono essenziali per il corretto funzionamento dei servizi da deployare.

## Creazione delle ConfigMap richieste

È necessario creare tre ConfigMap per configurare i servizi:

1. **`datastore-address`**

   Contiene le informazioni relative agli indirizzi del datastore:
   ```bash
   kubectl create configmap datastore-address \
     --from-literal=kafka-address="<kafka-address>" \
     --from-literal=db-suffix="<db-suffix>" \
     --from-literal=db-uri-srv="<db-uri-srv>" \
     --from-literal=db-address="<db-address>" \
     -n <namespace-di-destinazione>
   ```

2. **`network-address`**

   Contiene l'indirizzo dei servizi di rete:
   ```bash
   kubectl create configmap network-address \
     --from-literal=service-address="<service-address>" \
     -n <namespace-di-destinazione>
   ```

3. **`client-keystore-cm`**

   Include un file `client.pfx` per l'autenticazione del client:
   ```bash
   kubectl create configmap client-keystore-cm \
     --from-file=client.pfx=path\al\file\client.pfx \
     -n <namespace-di-destinazione>
   ```

   Il file `client.pfx` è essenziale per permettere la comunicazione sicura con **Event Hub**, un servizio di messaggistica gestito su Azure. Assicurati che l'Event Hub sia correttamente configurato nel tuo ambiente Azure.

## Creazione dei Secret richiesti

1. **`secrets-store-creds`**

   Contiene le credenziali per accedere ai servizi protetti:
   ```bash
   kubectl create secret generic secrets-store-creds \
     --from-literal clientid="<valore-clientid>" \
     --from-literal clientsecret="<valore-clientsecret>" \
     -n <namespace-di-destinazione>
   ```

2. **Secret per il Docker Registry**

   È necessario un Secret per autenticarsi al Docker Registry:
   ```bash
   kubectl create secret docker-registry docker-registry-creds \
     --docker-username=<nome-utente> \
     --docker-password=<password> \
     --docker-email=<email> \
     -n <namespace-di-destinazione>
   ```

## Aggiungere il Repository Helm

Aggiungi il repository Helm del progetto ed esegui l'aggiornamento:
```bash
helm repo add fse-gtw-helm https://ministero-salute.github.io/it-fse-gtw-helm/
helm repo update
```

## Installazione di un Chart

Per installare un chart nel cluster Kubernetes:
```bash
helm install <nome-release> fse-gtw-helm/<nome-chart> \
  --namespace <namespace> \
  --values <percorso-file-valori>
```

### Configurazione tramite variabili `--set`

In alternativa, è possibile configurare i valori direttamente durante l'installazione utilizzando il parametro `--set`. Esempio:
```bash
helm install <nome-release> fse-gtw-helm/<nome-chart> \
  --set "imagePullSecrets[0].name=<nome-secret>" \
  --set secrets.keyvaultName="<keyvault-name>" \
  --set secrets.tenantId="<tenant-id>" \
  --set secrets.secretKeyVaultName="<secret-keyvault-name>" \
  -n <namespace>
```

Sostituisci i segnaposto `<...>` con i valori appropriati per il tuo ambiente.

## Aggiornamento di un Chart

Per aggiornare un'installazione esistente:
```bash
helm upgrade <nome-release> fse-gtw-helm/<nome-chart> \
  --namespace <namespace> \
  --values <percorso-file-valori>
```

## Disinstallazione di un Chart

Per disinstallare un chart:
```bash
helm uninstall <nome-release> --namespace <namespace>
```

## Nota Finale

Assicurati che tutte le configurazioni nei file `values.yaml` siano aggiornate in base al tuo ambiente di destinazione. **Predisponi Event Hub e Cosmos DB su Azure**, poiché sono componenti fondamentali richiesti dai servizi. Consulta la documentazione ufficiale di Helm per ulteriori dettagli su come utilizzare i chart Helm.
