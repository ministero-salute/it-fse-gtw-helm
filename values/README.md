# README - Cartella `values`

La cartella `values` raccoglie i file di configurazione di esempio (`values.yaml`) per ogni microservizio installato tramite i chart Helm del progetto **it-fse-gtw-helm**.

## Scopo

Per ogni versione rilasciata dei chart Helm, sono disponibili in questa cartella i file di esempio dei valori (`values.yaml`) utilizzati per la configurazione dei microservizi. Questi file permettono di personalizzare il comportamento e le risorse di ciascun servizio durante l’installazione su Kubernetes.

## Struttura della Cartella

La struttura tipica è la seguente:

```
values/
  ├── <versione-chart>/
  │     ├── <microservizio-1>-values.yaml
  │     ├── <microservizio-2>-values.yaml
  │     └── ...
  ├── <versione-chart-successiva>/
  │     ├── <microservizio-1>-values.yaml
  │     ├── <microservizio-2>-values.yaml
  │     └── ...
  └── ...
```

### Supporto Multi-Cloud (da versione 2.0.0)

A partire dalla versione **2.0.0** dei chart Helm, è stato introdotto il supporto per il multi-cloud.  
Per ogni versione >= 2.0.0, troverai due sottocartelle dedicate agli ambienti cloud principali:

```
values/2.0.0/
  ├── azure/
  │     ├── it-fse-gtw-config-values.yaml
  │     ├── it-fse-gtw-dispatcher-values.yaml
  │     └── ...
  ├── aws/
  │     ├── it-fse-gtw-config-values.yaml
  │     ├── it-fse-gtw-dispatcher-values.yaml
  │     └── ...
```

- La sottocartella `azure` contiene i file di values di esempio per l’installazione su ambiente Azure.
- La sottocartella `aws` contiene i file di values di esempio per l’installazione su ambiente AWS.

## Utilizzo

- Per installare o aggiornare un microservizio tramite Helm, copia il file di esempio relativo alla versione, al microservizio e all’ambiente desiderato (`azure` o `aws`).
- Modifica i parametri secondo le tue esigenze (es. risorse, variabili d’ambiente, configurazioni specifiche).
- Utilizza il file come input per il comando `helm install` o `helm upgrade`.

## Esempio

Per la versione `2.0.0` del chart, troverai:

```
values/2.0.0/
  ├── azure/
  │     ├── it-fse-gtw-config-values.yaml
  │     ├── it-fse-gtw-dispatcher-values.yaml
  │     └── ...
  ├── aws/
  │     ├── it-fse-gtw-config-values.yaml
  │     ├── it-fse-gtw-dispatcher-values.yaml
  │     └── ...
```

## Note

- I file di esempio non contengono credenziali o dati sensibili.
- Personalizza sempre i valori prima di utilizzarli in ambienti di produzione.

---