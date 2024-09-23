
## Notes concerning PAGoDA version 3 

il faut créer un service account dans le namespace du serveur (ici argo-workflows) et un secret avec un token (un automatisme qui s'est perdu avec les dernières versions de kubernetes) avec un nom spécifique (NONSERVICEACCOUNT.service-account-token).
Une fois ce service account crée, il faudra créer des RoleBindings entre ce ServiceAccount du Namespace "argo-workflows" et les ClusterRole view et edit de créer lors de l'installation d'argo-workflows.
Dans notre cas, les services accounts créés sont liés aux groupes keycloak pagoda-admin et pagoda-user.

Seuls les SA créés dans le namespace hébergeant les serveurs sont pris en compte.

Pour les utilisateurs :

URL: https://argo-workflows.pagoda.liris.cnrs.fr/
Version 3.5.10

### NAMESPACES

They are three namespaces managed or known by the [Argo Server (AS)](https://argo-workflows.readthedocs.io/en/latest/argo-server/):

- `argo-workflows` : used by the Argo Server (AS) internals
- `argo-dev` : old namespace previously associated with PAGoDA version 2 (platform). 
  This is attributed to EBO  
- `ud-evolution`: namespace attributed to JPU.

Note: namespace access restrictions are handled through Rancher level authorizations (within the `argoworkflows-dev` project). Only the PAGoDA platform admin can modify such accesses.

### ACCESS
Pour lancer les workflows avec la cli d'argo, cela se passe via le serveur de argo (on récupère les credentials dans l'interface utilisateur)
Pour Hera, l'interaction se fait directement avec le kubeconfig donné par Rancher (https://rancher3.pagoda.liris.cnrs.fr/)

### Logs storage.

ArgoWorkflows logs are archived through an S3 bucket.
