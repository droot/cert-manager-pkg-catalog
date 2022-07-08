# cert-manager-vanilla

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cert-manager-vanilla`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cert-manager-vanilla`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cert-manager-vanilla
kpt live apply cert-manager-vanilla --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/