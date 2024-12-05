[![en](https://img.shields.io/badge/lang-en-red.svg)](installation-guide.en.md)

# Come Installare il Servizio it-fse-gtw-config

## Creazione della ConfigMap

Prima di installare il servizio **it-fse-gtw-config-cm**, è necessario creare un ConfigMap che contenga la configurazione richiesta per il servizio. <br>
Questo permette al servizio di utilizzare impostazioni personalizzate o variabili d'ambiente necessarie durante l'installazione e l'esecuzione.

Per creare la ConfigMap chiamata **it-fse-gtw-config-cm** nel cluster Kubernetes richiesto dal servizio è necessario eseguire il seguente comando: <br>

```bash
kubectl create configmap it-fse-gtw-config-cm --from-file=application.properties=config\application.properties
```
*Output:*
>configmap/it-fse-gtw-config-cm created


Oppure verifica che la ConfigMap sia stato creata correttamente eseguendo:

```bash
kubectl get configmap it-fse-gtw-config-cm
```

## Installazione del Servizio
Una volta creato la ConfigMap, puoi procedere con l'installazione del servizio **it-fse-gtw-config**

Per aggiornare o installare il servizio:

1. Scarica il chart Helm per il servizio utilizzando il comando helm fetch oppure recuperando direttamente il servizio dal repository.

2. Aggiorna o installa il servizio:
```bash
helm upgrade --install it-fse-gtw-config it-fse-gtw-config-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```

*Output:*
>Release "it-fse-gtw-rules-manager" does not exist. Installing it now.
>NAME it-fse-gtw-config
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

## Rimozione del Servizio:
Per rimuovere il servizio appena installato, esegui il seguente comando:

```bash
helm delete it-fse-gtw-config
```

---





















### Rules Manager

To create the configMap named **it-fse-gtw-rules-manager-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-rules-manager-cm --from-file=application.properties=path/al/file/application.properties --from-file=truststore.jks=path/al/file/truststore.jks
```
*Output:*
>configmap/it-fse-gtw-rules-manager-cm created

To upgrade or install the service:
```bash
helm upgrade --install it-fse-gtw-rules-manager it-fse-gtw-rules-manager-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-rules-manager" does not exist. Installing it now.
>NAME it-fse-gtw-rules-manager  
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None  

*To delete:*

```bash
helm delete it-fse-gtw-rules-manager
```

### Dispatcher

To create the configMap named **it-fse-gtw-dispatcher-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-dispatcher-cm --from-file=application.properties=config\application.properties --from-file=truststore.jks=config\truststore.jks
```
*Output:*
>configmap/it-fse-gtw-dispatcher created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-dispatcher it-fse-gtw-dispatcher-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-dispatcher" does not exist. Installing it now.
>NAME it-fse-gtw-dispatcher
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-dispatcher
```

### Validator

To create the configMap named **it-fse-gtw-validator-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-validator-cm --from-file=application.properties=config\application.properties --from-file=truststore.jks=config\truststore.jks
```
*Output:*
>configmap/it-fse-gtw-validator-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-validator it-fse-gtw-validator-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-validator" does not exist. Installing it now.
>NAME it-fse-gtw-validator
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-validator
```


### FHIR

To create the configMap named **it-fse-gtw-fhir-mapping-engine-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-fhir-mapping-engine-cm --from-file=application.properties=config\application.properties
```
*Output:*
>configmap/it-fse-gtw-fhir-mapping-engine-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-fhir-mapping-engine it-fse-gtw-fhir-mapping-engine-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-fhir-mapping-engine" does not exist. Installing it now.
>NAME it-fse-gtw-fhir-mapping-engine
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-fhir-mapping-engine
```


### Indexer

To create the configMap named **it-fse-gtw-indexer-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-indexer-cm --from-file=application.properties=config\application.properties --from-file=truststore.jks=config\truststore.jks
```
*Output:*
>configmap/it-fse-gtw-indexer-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-indexer it-fse-gtw-indexer-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-indexer" does not exist. Installing it now.
>NAME it-fse-gtw-indexer
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-indexer
```

### Ini-client

To create the configMap named **it-fse-gtw-ini-client-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-ini-client-cm --from-file=application.properties=config\application.properties --from-file=truststore.jks=config\truststore.jks --from-file=S1GTW-INI.jks=config\S1GTW-INI.jks --from-file=A1GTW-INI.jks=config\A1GTW-INI.jks
```
*Output:*
>configmap/it-fse-gtw-ini-client-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-ini-client it-fse-gtw-ini-client-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-ini-client" does not exist. Installing it now.
>NAME it-fse-gtw-ini-client
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-ini-client
```


### Garbage

To create the configMap named **it-fse-gtw-garbage-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-garbage-cm --from-file=application.properties=config\application.properties
```
*Output:*
>configmap/it-fse-gtw-garbage-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-garbage it-fse-gtw-garbage-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release "it-fse-gtw-garbage" does not exist. Installing it now.
>NAME: it-fse-gtw-garbage
>LAST DEPLOYED: Fri Nov 29 12:38:41 2024
>NAMESPACE: default
>STATUS: deployed
>REVISION: 1
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-garbage
```

### Status-check

To create the configMap named **it-fse-gtw-status-check-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-status-check-cm --from-file=application.properties=config\application.properties
```
*Output:*
>configmap/it-fse-gtw-status-check-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-status-check it-fse-gtw-status-check-0.1.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release  "it-fse-gtw-status-check" does not exist. Installing it now.
>NAME it-fse-gtw-dispatcher
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None

*To delete:*

```bash
helm delete it-fse-gtw-status-check
```


### Status-manager

To create the configMap named **it-fse-gtw-status-manager-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-status-manager-cm --from-file=application.properties=config\application.properties --from-file=truststore.jks=config\truststore.jks
```
*Output:*
>configmap/it-fse-gtw-status-manager-cm created

To upgrade or install the service:

```bash
helm upgrade --install it-fse-gtw-status-manager it-fse-gtw-status-manager-1.2.0.tgz --set "imagePullSecrets[0].name=azregdevops"
```
*Output:*
>Release  "it-fse-gtw-status-manager" does not exist. Installing it now.
>NAME it-fse-gtw-status-manager
>LAST DEPLOYED: Fri Nov 29 11:05:42 2024  
>NAMESPACE: default  
>STATUS: deployed  
>REVISION: 1  
>TEST SUITE: None


*To delete:*

```bash
helm delete it-fse-gtw-status-manager
```
