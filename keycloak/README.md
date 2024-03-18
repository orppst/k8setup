Keycloak customization
======================

Keycloak needs to be customized in two ways to make it suitable for the proposal tool

* a realm is added that has the authorization setup 
* a theme is created so that the login screen has the same look and feel as the proposal tool

These customizations are then built into the docker image 

need to login to the repo first

```shell
docker login -u pahjbo https://kilburn.jb.man.ac.uk 
```
then 

```shell
docker build --platform linux/amd64  -t kilburn.jb.man.ac.uk/orppst/keycloak .
docker image push kilburn.jb.man.ac.uk/orppst/keycloak
```



## Theme

The theme is contained within the theme directory - see https://www.keycloak.org/docs/latest/server_development/index.html#_themes for more information on customizing



## Realm

This is the core of the setup for the orp-pst case - realms can be edited and exported with

```shell
docker run -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin -p 127.0.0.1:8080:8080 --name kcorp -it --entrypoint bash kilburn.jb.man.ac.uk/orppst/keycloak
```
which will create a container without running keycloak inside it - then start the server
```shell
/opt/keycloak/bin/kc.sh start-dev --import-realm
```

and login to the admin console to make changes to realm http://localhost:8080/admin/ 

Then when satisfied with the changes, stop the server with ctrl-C and

```shell
/opt/keycloak/bin/kc.sh export --file /tmp/orppst-realm.json --users same_file --realm orppst
```

then from another shell running on the docker host

```shell
docker cp kcorp:/tmp/orppst-realm.json ./
```


# attaching to DB on K8 cluster

need to get a port-forward
```shell
PG_CLUSTER_PRIMARY_POD=$(kubectl get pod -n orp-pst -o name \
  -l postgres-operator.crunchydata.com/cluster=keycloakdb,postgres-operator.crunchydata.com/role=master)
kubectl -n  orp-pst  port-forward "${PG_CLUSTER_PRIMARY_POD}" 5432:5432 &
```

then connect
```shell
PG_CLUSTER_USER_SECRET_NAME=keycloakdb-pguser-keycloakdb
PGPASSWORD=$(kubectl get secrets -n orp-pst "${PG_CLUSTER_USER_SECRET_NAME}" -o go-template='{{.data.password | base64decode}}')  \
PGUSER=$(kubectl get secrets -n orp-pst "${PG_CLUSTER_USER_SECRET_NAME}" -o go-template='{{.data.user | base64decode}}') \
PGDATABASE=$(kubectl get secrets -n orp-pst "${PG_CLUSTER_USER_SECRET_NAME}" -o go-template='{{.data.dbname | base64decode}}') \
psql -h localhost

```






