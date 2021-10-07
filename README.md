## Installing customize ArgoCD using GitOps

- Cluster requirements & reservation.
- Create a Github Organization, Fork & Clone.
- Install ArgoCD
- Customize ArgoCD
- Login in to the ArgoCD UI

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

    - cd multi-tenancy-gitops
    ```
    oc apply -f setup/ocp47/
    
    ```
