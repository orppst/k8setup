FROM quay.io/keycloak/keycloak:23.0.6 as builder

WORKDIR /opt/keycloak
COPY theme /opt/keycloak/themes

COPY orppst-realm.json /opt/keycloak/data/import/
RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:23.0.6
COPY --from=builder /opt/keycloak/ /opt/keycloak/

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]