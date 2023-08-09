Polaris Deployment
==================

This repository contains the configuration to deploy 
the Polaris proposal tool to a kubernetes cluster

* [db](./db) contains postgres setup for the database functionality.
```shell
kubectl apply -k db
```
* [keycloak](./keycloak) contains keycloak setup for AAI functionality.
```shell
kubectl apply -k keycloak
```

for now the individual components of the tool are installed from the source code directories with the 

```shell
kubectl apply -f build/kubernetes/kubernetes.yml 
```