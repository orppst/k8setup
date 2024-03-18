Database setup for Proposal Tool
==================================

This assumes that the https://quarkus.io/guides/deploying-to-kubernetes#service_binding 
functionality is being used and that the postgres operator https://access.crunchydata.com/documentation/postgres-operator/latest/quickstart
has been installed into the k8 cluster.

via helm https://access.crunchydata.com/documentation/postgres-operator/latest/installation/helm

```shell
helm install -n pgo pgo oci://registry.developers.crunchydata.com/crunchydata/pgo
```

it is possible to run a PGAdmin instance too for the db https://access.crunchydata.com/documentation/postgres-operator/latest/architecture/postgrescluster-scoped-pgadmin-4



p.s. do not confuse postgres operator with 
https://postgres-operator.readthedocs.io/en/latest/quickstart/