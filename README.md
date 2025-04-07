Polaris Deployment
==================

This repository contains the configuration to deploy 
the Polaris proposal tool to a kubernetes cluster

The manifests below assume that components are deployed to the `orp-pst` namespace this should be manually
created as below

```shell
kubectl create namespace orp-pst
```

The database k8s operator that is used is [crunchydata]\(https://access.crunchydata.com/documentation/postgres-operator/latest)

* [db](./db) contains postgres setup for the database functionality.
```shell
kubectl apply -k db
```
* [keycloak](./keycloak) contains keycloak setup for AAI functionality.
  in order to set up the admin username and password (use different values obviously!)
```shell
kubectl create secret generic keycloakadm-secret -n orp-pst --from-literal='username=adm' --from-literal='password=adm'
```
then create
```shell
kubectl apply -k keycloak
```

* need to set up storage
```shell
kubectl apply -k storage
```

* for now the individual components of the tool are installed from the source code directories with the
```shell
quarkus build -Dquarkus.container-image.push=true --no-tests
kubectl apply -f build/kubernetes/kubernetes.yml 
```

*N.B. for any image pushes it is necessary to login to the repository first*

if building on ARM Mac then cannot build and push directly in one go - need to build with the correct arch.
```shell
quarkus build -Dquarkus.docker.buildx.platform=linux/amd64 --no-tests
docker push kilburn.jb.man.ac.uk/orppst/pst-gui:0.6
```
```shell
docker push kilburn.jb.man.ac.uk/orppst/pst-api-service:0.6
```


```shell
docker login -u pahjbo https://kilburn.jb.man.ac.uk   
```

## Minikube notes


if running this setup on minikube, then it is necessary to make sure that the default storage class is
on so that the persistent volume claims will be met

```shell
 minikube addons enable default-storageclass
```


