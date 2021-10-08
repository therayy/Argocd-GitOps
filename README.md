<br>

<p align="center">
    <img width="500px" src="imgs/openshift-gitops-banner.png">
</p>

<br>

## Installing customize ArgoCD using GitOps

- Configure Cluster requirements & reservation.
- Create a Github Organization, Fork & Clone.
- Install ArgoCD
- Getting Started with GitOps
- Deploying Services
---

### Cluster requirements & reservation.

- Server Version: 4.7 or higher
- [ROKS Red Hat OpenShift Cluster](https://techzone.ibm.com/my/reservations/create/60da20f935e6ac001f1c4086)

### Create a Github Organization, Fork & Clone.

- [Create a Github Organization with a defined name](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch)

- Fork these repositories to your ORGANIZATION & Clone them to your local repo.:
    - [multi-tenancy-gitops](https://github.com/cloud-native-toolkit/multi-tenancy-gitops)
       ``` 
       git clone https://github.com/<YOUR ORGANIZATION>/multi-tenancy-gitops.git
       ```    
    - [multi-tenancy-gitops-apps](https://github.com/cloud-native-toolkit-demos/multi-tenancy-gitops-apps)
        ```
         git clone https://github.com/<YOUR ORGANIZATION>/multi-tenancy-gitops-apps.git 
         ```
    - [multi-tenancy-gitops-services](https://github.com/cloud-native-toolkit/multi-tenancy-gitops-services)
        ``` 
        git clone https://github.com/<YOUR ORGANIZATION>/multi-tenancy-gitops-services.git
        ```
    - [multi-tenancy-gitops-infra](https://github.com/cloud-native-toolkit/multi-tenancy-gitops-infra)   
        ```
        git clone https://github.com/<YOUR ORGANIZATION>/multi-tenancy-gitops-infra.git  
        ```
### Install ArgoCD 

- To insall the Red Hat GitOps operator follow the steps:

    - cd multi-tenancy-gitops || tree . -d -L 2
    - This command is going to install Red Hat operator and the defaut ArgoCD instance
        ```
        oc apply -f setup/ocp47/ 
        ```
    - Let us now delete the default ArgoCD instance that is created earlier.
        ```
        oc delete gitopsservice cluster -n openshift-gitops || true
        ```
    - Create a custom ArgoCD instance.
        ```
        oc apply -f setup/ocp47/argocd-instance/ -n openshift-gitops
        ```
- Launch ArgoCD.
    - ArgoCD can be accessed via an OpenShift route. Using a browser, navigate to the URL returned
        ```
        oc get route -n openshift-gitops | grep openshift-gitops-cntk-server | awk '{print "https://"$2}'
        ```
    - Logging in (Sign in with the user **admin**)
        - Run the below cmd to get the Password
        ```
        oc get secret/openshift-gitops-cntk-cluster -n openshift-gitops -o json | jq -r '.data."admin.password"' | base64 -D
        ```
### Cloud Native MQ GitOps Configuration
- Run the customization script
    ```
    GIT_ORG=<Your Organization> GIT_BRANCH=master ./scripts/set-git-source.sh
    ```
    - git add, commit & push your changes by passing the $GIT_BRANCH=master.

- Update multi-tenancy-gitops-apps repository
    - git add, commit & push your changes by passing the $GIT_BRANCH=master.

### Connect ArgoCD to the GitOps repository
- Deploy Kubernetes resources with kustomization.yaml
    - Open 0-bootstrap/single-cluster/1-infra/kustomization.yaml and uncomment the below resources:
        ```
        argocd/consolelink.yaml
        argocd/consolenotification.yaml
        argocd/namespace-ibm-common-services.yaml
        argocd/namespace-ci.yaml
        argocd/namespace-dev.yaml
        argocd/namespace-staging.yaml
        argocd/namespace-prod.yaml
        argocd/namespace-sealed-secrets.yaml
        argocd/namespace-tools.yaml
        ```
    - git add, commit & push your changes to the master branch.

### Apply ArgoCD bootstrap.yaml
- Make sure that only the 1-infra is uncommented.
- Apply the bootstrap YAML to the cluster:
    ```
    oc apply -f 0-bootstrap/single-cluster/bootstrap.yaml
    ```
    