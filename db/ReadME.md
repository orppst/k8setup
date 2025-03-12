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

N.B 
* actually install the db instances from directory above.
* cannot progress above postgres 14 because of the new permissions on public schema not being automatically supported by quarkus...

p.s. do not confuse postgres operator with 
https://postgres-operator.readthedocs.io/en/latest/quickstart/ https://github.com/zalando/postgres-operator
