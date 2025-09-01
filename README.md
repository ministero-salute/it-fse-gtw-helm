# it-fse-gtw-helm

Il repository **it-fse-gtw-helm** contiene i chart Helm relativi ai servizi connessi al **Fascicolo Sanitario Elettronico (FSE)**, in particolare il **Gateway Distruito**.

## Cronologia delle versioni

| Versione Chart | Descrizione                                                                 |
|----------|------------------------------------------------------------------------------|
| v1.0.0   | Prima release ufficiale. Supporta il deployment esclusivamente su ambiente Azure. |
| v2.0.0   | Estensione delle funzionalità con supporto al deployment multi-cloud su Azure e AWS. |


## Prerequisiti

Prima di procedere con l'installazione, assicurati di avere:

1. **Cluster Kubernetes** configurato e funzionante.
2. **Helm** installato (versione 3 o superiore).
3. **Oggetti ConfigMap e Secret** necessari creati nel namespace di destinazione.
4. **Servizi cloud richiesti**:  
   - **Azure**: Event Hub, Cosmos DB e Postgres DB  
   - **AWS**: MSK, DocumentDB e Aurora DB (PostgreSQL)  
   Questi servizi sono indispensabili per il corretto funzionamento dei componenti da deployare.

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

Assicurati che tutte le configurazioni nei file `values.yaml` siano aggiornate in base al tuo ambiente di destinazione. **Predisponi Event Hub, Cosmos DB e PostGres su Azure**, poiché sono componenti fondamentali richiesti dai servizi. Consulta la documentazione ufficiale di Helm per ulteriori dettagli su come utilizzare i chart Helm.
