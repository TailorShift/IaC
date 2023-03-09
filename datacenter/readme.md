# Datacenter IaC architecture

The datacenter is managed with OpenShift GitOps (ArgoCD).

We set up two main "apps":
* `operators` containing all resources for OpenShift operators we use
*  `apps` containing the app of apps declaration of all self-developer services

We do not use ApplicationSets because 
* we do not want to deploy the same setup to multiple clusters
* the app of apps pattern is widely used and documented
* the author has good knowledge of the app of apps pattern