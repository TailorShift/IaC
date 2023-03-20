# Datacenter IaC architecture

The datacenter is managed with OpenShift GitOps (ArgoCD).

We set up two main "apps":

*  `apps-of-apps` containing the app of apps declaration.
*  `apps` containing the argocd applications. All custom applications to be deployed, need an `Application` kind resource here. Automatically deployed by ARGO CD App ../app-of-apps/apps-aoa.yaml

We do not use ApplicationSets because 
* we do not want to deploy the same setup to multiple clusters
* the app of apps pattern is widely used and documented
* the author has good knowledge of the app of apps pattern