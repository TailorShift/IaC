# ArgoCD initialisation
Before argocd can manage and deploy applications, an agrocd custom resource needs to be created manually:

Create the argo cd instance and git repository reference

    oc -n atos-developmant apply ../charts/argocd/argocd.yaml
    oc -n atos-developmant apply ../charts/argocd/argocd-repo-iac.yaml

Edit the secret and put in the ssh private key for your github/gitlab

    oc -n atos-developmant edit secret argocd-repo-iac

