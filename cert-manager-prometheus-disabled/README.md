# cert-manager-prometheus-disabled

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cert-manager-prometheus-disabled`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cert-manager-prometheus-disabled`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cert-manager-prometheus-disabled
kpt live apply cert-manager-prometheus-disabled --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
