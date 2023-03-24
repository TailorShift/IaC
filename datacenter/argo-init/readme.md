# ArgoCD initialisation
Before argocd can manage and deploy applications, an agrocd custom resource needs to be created manually:

* Choose your environment
    ```
    NS=atos-development
    NS=atos-production
    ```

* Create the argo cd instance and git repository reference
    ```
    oc -n $NS apply -f ../charts/argocd/templates/argocd.yaml
    oc -n $NS apply -f ../charts/argocd/templates/argocd-repo-iac.yaml
    ```

* Edit the secret and put in the ssh private key for your github/gitlab
    ```
    oc -n $NS edit secret argocd-repo-iac
    ```

* Create the app of apps, dploying other apps
    ```
    # for development
    oc -n $NS apply -f ../app-of-apps/apps-aoa-dev.yaml

    # or for production
    oc -n $NS apply -f ../app-of-apps/apps-aoa-prod.yaml
    ```

* In Argocd manually sync the app "apps-aoa"