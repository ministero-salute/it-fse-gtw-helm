[![it](https://img.shields.io/badge/lang-it-green.svg)](installation-guide.md)

# How to Install the it-fse-gtw-config service

## Create the ConfigMap

Before installing the **it-fse-gtw-config-cm** service, you need to create a ConfigMap that contains the required configuration for the service. <br>
This allows the service to use custom settings or environment variables needed during installation and runtime.

To create the configMap named **it-fse-gtw-config-cm** in the Kubernetes cluster required from the service:

```bash
kubectl create configmap it-fse-gtw-config-cm --from-file=application.properties=config\application.properties
```
*Output:*
>configmap/it-fse-gtw-config-cm created

or 
Verify the ConfigMap has been created successfully by running:

```bash
kubectl get configmap it-fse-gtw-config-cm
```

## Install the Service
Once the ConfigMap has been created, you can install the it-fse-gtw-config itself.

To upgrade or install the service:

1. Download the Helm chart for the service either by using the helm fetch command or by directly retrieving the service from the repository.

2. Upgrade or Install the service:
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

## Remove the service:
To remove the service that has been installed, run the following command:

```bash
helm delete it-fse-gtw-config
```
