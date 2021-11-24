# Red Hat Advanced Cluster Management and OpenShift GitOps

An effective way to manage OpenShift Gitops instances with RHACM.

## Why this approach is worth considering
This repo is designed to enhance GitOps approach leveraged by OpenShift GitOps
in a multi-cluster environment with business continuity process managed by RHACM.

## How to use this repository
This is a boilerplate repository to quickly set up the initial resources. \
It provides:
  * Folder-based structure model
  * RHACM objects
  * OpenShift GitOps example objects

To start using this repo you can fork it and adapt it to your environment.

## Repository structure model
This is a GitOps folder-based structure model.

* [_rhacm-manifests_](rhacm-manifests): contains Red Hat Advanced Cluster Management manifests.
* [_gitops-manifests_](gitops-manifests): contains Argo CD resources, such as AppProjects, Applications and ApplicationSets.

### Why folder-based strategy and not branched-based
The folder-based approach has the following main advantages:
* The main branch is the Single Point of Truth for data
* Follows Git standard workflows
* Increase collaboration and the whole team enablement
* Avoids _independent_ branches proliferation
* Reduces time during troubleshooting

## Prerequisites
To use this repo you need to have in your enviroment:
* RHACM MultiClusterHub installed on an OpenShift Cluster.
* At least one OpenShift Cluster on which to install OpenShift Gitops operator.

## How to deploy resources on RHACM Hub
* Login into RHACM Hub cluster.
* Deploy this repository on RHACM:
  ```
  clone repository because is not the main branch
  navigate to root folder 
  oc apply -k rhacm-gitops/rhacm-manifests/overlays/prod/
  ```

  This will create the following resources:
  * Channel
  * PlacementRules
  * Subscription for Argo CD resources (i.e. AppProjects, Applications, ApplicationSets)
  * ArgoCD Application
  * Channel namespace
  * Policy for: 
    * OpenShift GitOps Operator installation, needed cluster role binding and namespace openshift-gitops creation;
    * HTPasswd Identity Provider configuration; 
    * Cluster Admin role binding configuration;
    * Kubeadmin user deletion;  

