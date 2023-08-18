Keycloak customization
======================

Keycloak needs to be customized in two ways to make it suitable for the proposal tool

* a realm is added that has the authorization setup 
* a theme is created so that the login screen has the same look and feel as the proposal tool

These customizations are then built into the docker image

```shell
docker build -t mykeycloak .
```



## Theme

The theme is contained within the theme directory - see https://www.keycloak.org/docs/latest/server_development/index.html#_themes for more information on customizing



## Realm

This is the core of the setup for the orp-pst case - realms can be edited and exported with

```shell
docker run -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin -p 127.0.0.1:8080:8080 --name kcorp -it --entrypoint bash mykeycloak
```
which will create a container without running keycloak inside it - then start the container

```shell
/opt/keycloak/bin/kc.sh start-dev
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






