# Renovate Helm Releases

Creates [Renovate](https://github.com/renovatebot/renovate) annotations in [Flux2](https://github.com/fluxcd/flux2) Helm Releases

## Workflow example usage

```yaml
uses: k8s-at-home/renovate-helm-releases@v1
with:
  cluster-path: './cluster'
```

## Renovate configuration example

The following is needed in order for Renovate to pick up Helm repositories in Helm Releases

```jsonc
  "regexManagers": [
    // regexManager to read and process helm repositories
    {
      // tell renovatebot to parse only helm releases
      "fileMatch": ["cluster/.+helm-release\\.yaml$"],
      // tell renovatebot to match the following pattern in helm release files
      "matchStrings": [
        "registryUrl=(?<registryUrl>.*?)\n *chart: (?<depName>.*?)\n *version: (?<currentValue>.*)\n"
      ],
      // tell renovatebot to search helm repositories
      "datasourceTemplate": "helm"
    },
```
