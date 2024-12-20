# it-fse-gtw-helm

Il repository **it-fse-gtw-helm** contiene i chart Helm relativi ai servizi connessi al **Fascicolo Sanitario Elettronico (FSE)**, in particolare il **Gateway Distruito**.

## Contenuto del Repository

Questo repository include:
- Chart Helm per il deployment dei servizi del Gateway Distribuito.
- Template configurabili per semplificare il deployment su cluster Kubernetes.
- File di configurazione e risorse utili per la gestione delle applicazioni.

## Prerequisiti

Per utilizzare i chart di questo repository, è necessario:
1. Avere un cluster Kubernetes configurato e funzionante.
2. Avere installato Helm (versione 3 o superiore).
3. Avere accesso al repository e le relative autorizzazioni.

## Come Utilizzare i Chart

### 1. Aggiungere il Repository Helm

Per aggiungere il repository locale, eseguire:

```bash
helm repo add fse-gtw-helm https://ministero-salute.github.io/it-fse-gtw-helm/
helm repo update
```

### 2. Installare un Chart

Per installare un servizio specifico:

```bash
helm install <release-name> fse-gtw-helm/<chart-name> --namespace <namespace> --values <path-to-values-file>
```

### 3. Aggiornare un Chart

Per aggiornare un'installazione esistente:

```bash
helm upgrade <release-name> fse-gtw-helm/<chart-name> --namespace <namespace> --values <path-to-values-file>
```

### 4. Disinstallare un Chart

Per disinstallare un servizio:

```bash
helm uninstall <release-name> --namespace <namespace>
```

## Struttura del Repository

La struttura del repository è organizzata come segue:

```
.
├── charts/                # Directory contenente i chart Helm
├── templates/             # Template condivisi per configurazioni standard
├── values.yaml            # File dei valori predefiniti
├── README.md              # Documentazione del repository
```

