# cert-manager-psp

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cert-manager-psp`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cert-manager-psp`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cert-manager-psp
kpt live apply cert-manager-psp --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
