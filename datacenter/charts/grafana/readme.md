# Grafana

Configure the grafana helm repo

    helm repo add grafana https://grafana.github.io/helm-charts

Update the contents

    helm repo update

See what grafana has available

    helm search repo grafana/grafana --versions

Pick a suitable version, and download the chart files

    helm pull grafana/grafana --untar --version 6.52.4 


Pull up the default values file from the chart for prod and dev

    cp grafana/values.yaml ./values-<namespace>.yaml


Reference the correct values file in Your ArgoCD Application chart via {{ .Release.Namespace }}

```
source:
  ...
  helm:
    valueFiles: 
      - ../values-{{ .Release.Namespace }}.yaml
```