Database setup for Proposal Tool
==================================

This assumes that the https://quarkus.io/guides/deploying-to-kubernetes#service_binding 
functionality is being used and that the postgres operator https://access.crunchydata.com/documentation/postgres-operator/latest/quickstart
has been installed into the k8 cluster.

via helm https://access.crunchydata.com/documentation/postgres-operator/latest/installation/helm

```shell
helm install pgo oci://registry.developers.crunchydata.com/crunchydata/pgo
```





p.s. do not confuse postgres operator with 
https://postgres-operator.readthedocs.io/en/latest/quickstart/