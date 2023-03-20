# ArgoCD initialisation
Before argocd can manage and deploy applications, an agrocd custom resource needs to be created manually:

* Create the argo cd instance and git repository reference
    ```
    oc -n atos-development apply -f ../charts/argocd/argocd.yaml
    oc -n atos-development apply -f ../charts/argocd/argocd-repo-iac.yaml
    ```

* Edit the secret and put in the ssh private key for your github/gitlab
    ```
    oc -n atos-development edit secret argocd-repo-iac
    ```

* Create the app of apps, dploying other apps
    ```
    oc -n atos-development apply -f ../app-of-apps/apps-aoa.yaml
    ```

* In Argocd manually sync the app "apps-aoa"