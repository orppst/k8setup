Polaris Deployment
==================

This repository contains the configuration to deploy 
the Polaris proposal tool to a kubernetes cluster

The manifests below assume that components are deployed to the `orp-pst` namespace this should be manually
created as below

```shell
kubectl create namespace orp-pst
```



* [db](./db) contains postgres setup for the database functionality.
```shell
kubectl apply -k db
```
* [keycloak](./keycloak) contains keycloak setup for AAI functionality.
```shell
kubectl apply -k keycloak
```
in order to set up the admin username and password (use different values obviously!)
```shell
kubectl create secret generic keycloakadm-secret -n orp-pst --from-literal='username=adm' --from-literal='password=adm'
```

* for now the individual components of the tool are installed from the source code directories with the
```shell
quarkus build -Dquarkus.container-image.push=true --no-tests
kubectl apply -f build/kubernetes/kubernetes.yml 
```


## Minikube notes


if running this setup on minikube, then it is necessary to make sure that the default storage class is
on so that the persistent volume claims will be met

```shell
 minikube addons enable default-storageclass
```


