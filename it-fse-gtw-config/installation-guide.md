[![en](https://img.shields.io/badge/lang-en-red.svg)](installation-guide.en.md)

# Come Installare il servizio it-fse-gtw-config

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
