# cert-manager-pkg-catalog

This repository contains several variants of cert-manager packages.

This repository is *suppose* to represent official kpt packages released by Cert Manager project.

## Few words about the content organization

bundles directory contain the kubernetes manifests generated using `helm`.

Steps followed to generate the static manifests for each variant:

```sh

cd bundles/

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks > cert-manager-v.1.8.2-vanilla.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set prometheus.enabled=false > cert-manager-v.1.8.2-prometheus-disabled.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set podSecurityPolicy.enabled=true > cert-manager-v.1.8.2-psp.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set prometheus.servicemonitor.enabled=true > cert-manager-v.1.8.2-prometheus-sm.yaml

helm template cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version 1.8.2 --include-crds --no-hooks --set prometheus.servicemonitor.enabled=true --set podSecurityPolicy.enabled=true > cert-manager-v.1.8.2-uber.yaml

```

Steps followed to generate kpt package for one of the variants `cert-manager-vanilla`:

```sh

mkdir cert-manager-vanilla

kpt pkg init cert-manager-vanilla
kubectl-slice -f bundles/cert-manager-v.1.8.2-vanilla.yaml --template '{{.kind|lower}}/{{.metadata.name|dottodash}}.yaml' -o cert-manager-vanilla
Wrote cert-manager-vanilla/serviceaccount/cert-manager-cainjector.yaml -- 484 bytes.
Wrote cert-manager-vanilla/serviceaccount/cert-manager.yaml -- 466 bytes.
Wrote cert-manager-vanilla/serviceaccount/cert-manager-webhook.yaml -- 469 bytes.
Wrote cert-manager-vanilla/configmap/cert-manager-webhook.yaml -- 309 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-cainjector.yaml -- 1149 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-issuers.yaml -- 866 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-clusterissuers.yaml -- 901 bytes.
Wrote cert-manager-vanilla/lusterrole/cert-manager-controller-certificates.yaml -- 1506 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-orders.yaml -- 1417 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-challenges.yaml -- 2455 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-ingress-shim.yaml -- 1541 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-view.yaml -- 850 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-edit.yaml -- 960 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-approve:cert-manager-io.yaml -- 729 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-controller-certificatesigningrequests.yaml -- 1205 bytes.
Wrote cert-manager-vanilla/clusterrole/cert-manager-webhook:subjectaccessreviews.yaml -- 543 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-cainjector.yaml -- 639 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-issuers.yaml -- 637 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-clusterissuers.yaml -- 651 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-certificates.yaml -- 647 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-orders.yaml -- 635 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-challenges.yaml -- 643 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-ingress-shim.yaml -- 647 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-approve:cert-manager-io.yaml -- 671 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-controller-certificatesigningrequests.yaml -- 677 bytes.
Wrote cert-manager-vanilla/clusterrolebinding/cert-manager-webhook:subjectaccessreviews.yaml -- 667 bytes.
Wrote cert-manager-vanilla/role/cert-manager-cainjector:leaderelection.yaml -- 1116 bytes.
Wrote cert-manager-vanilla/role/cert-manager:leaderelection.yaml -- 693 bytes.
Wrote cert-manager-vanilla/role/cert-manager-webhook:dynamic-serving.yaml -- 733 bytes.
Wrote cert-manager-vanilla/rolebinding/cert-manager-cainjector:leaderelection.yaml -- 784 bytes.
Wrote cert-manager-vanilla/rolebinding/cert-manager:leaderelection.yaml -- 761 bytes.
Wrote cert-manager-vanilla/rolebinding/cert-manager-webhook:dynamic-serving.yaml -- 671 bytes.
Wrote cert-manager-vanilla/service/cert-manager.yaml -- 688 bytes.
Wrote cert-manager-vanilla/service/cert-manager-webhook.yaml -- 661 bytes.
Wrote cert-manager-vanilla/deployment/cert-manager-cainjector.yaml -- 1580 bytes.
Wrote cert-manager-vanilla/deployment/cert-manager.yaml -- 1860 bytes.
Wrote cert-manager-vanilla/deployment/cert-manager-webhook.yaml -- 2464 bytes.
Wrote cert-manager-vanilla/mutatingwebhookconfiguration/cert-manager-webhook.yaml -- 1342 bytes.
Wrote cert-manager-vanilla/validatingwebhookconfiguration/cert-manager-webhook.yaml -- 1530 bytes.
39 files generated.c
```

## Packages

Catalog currently have following variants:

- cert-manager-vanilla
- cert-manager-psp
- cert-manager-prometheus-disabled
- cert-manager-uber
- cert-manager-prometheus-sm
