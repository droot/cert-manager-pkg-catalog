# cert-manager-uber

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cert-manager-uber`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cert-manager-uber`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cert-manager-uber
kpt live apply cert-manager-uber --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
