FROM quay.io/keycloak/keycloak:21.0.1 as builder

WORKDIR /opt/keycloak

COPY orppst-realm.json /opt/keycloak/data/import/
RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:21.0.1
COPY --from=builder /opt/keycloak/ /opt/keycloak/
COPY theme /opt/keycloak/themes

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]