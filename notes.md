# cert-manager-pkg-catalog

Catalog currently have following off-the-shelf abstract packages for cert-manager:

- cert-manager-basic
- cert-manager-psp: This package is created by cloning `cert-manager-basic` and applying PSP specific changes on top. So this is essentially `cert-manager-basic + psp`.


## Notes

bundles directory contain the kubernetes manifests generated using `helm`.

Steps followed to generate the static manifests for each variant:

```sh

cd bundles/

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks > cert-manager-v.1.8.2-basic.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set global.podSecurityPolicy.enabled=true > cert-manager-v.1.8.2-psp.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set prometheus.servicemonitor.enabled=true > cert-manager-v.1.8.2-prometheus-sm.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set prometheus.servicemonitor.enabled=true --set global.podSecurityPolicy.enabled=true > cert-manager-v.1.8.2-uber.yaml

```

Steps followed to generate kpt package for one of the variants `cert-manager-basic`:

```sh

mkdir cert-manager-basic

kpt pkg init cert-manager-basic
kubectl-slice -f bundles/cert-manager-v.1.8.2-basic.yaml --template '{{.kind|lower}}/{{.metadata.name|dottodash}}.yaml' -o cert-manager-basic
...
39 files generated.
```

