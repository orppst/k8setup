FROM quay.io/keycloak/keycloak:25.0.0 as builder

WORKDIR /opt/keycloak
COPY theme /opt/keycloak/themes

COPY /providers/keycloak-orcid.jar /opt/keycloak/providers/
COPY orppst-realm.json /opt/keycloak/data/import/
RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:25.0.0
COPY --from=builder /opt/keycloak/ /opt/keycloak/

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]