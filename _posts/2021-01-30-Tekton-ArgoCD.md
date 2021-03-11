---
author: jaruizes
layout: post
title: "Kubernetes - CI/CD with Tekton & Argo CD"
date: 2021-03-08 01:30
category : Kubernetes
comments: false
imagefeature: k8s/k8s-objects.png
tags:
    - microservices
    - kubernetes
    - ci/cd
---

# Kubernetes - CI/CD with Tekton & Argo CD
With this post I'm going to show how a modern and cloud native CI/CD could be implemented within a Kubernetes environment
I'm going to use two different tools:

- **Tekton**: to implement CI stages
- **Argo CD**: to implement CD stages (Gitops)

<br />


## ¿Tekton?

**Tekton** is an Open Source framework to build CI/CD pipelines directly over a Kuberentes cluster. 

**How can it do that?** Because Tekton defines a series of Kubernetes objects extending the Kubernetes API. Sorry, **what that means?** Ok, if we go to the [Kubernetes official page](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/), we can read the following definition:

> *Kubernetes objects* are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster

So, examples of Kubernetes objects are: Pod, Service, Deployment, etc...**Tekton builds its own objects to Kubernetes and deploys them into the cluster**. If you feel curious about custom objects, here [the official documentation](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) is and you can also check the Tekton Github to see how these objects are. For instance, [Pipeline](https://github.com/tektoncd/pipeline/blob/master/config/300-pipeline.yaml) or [Task](https://github.com/tektoncd/pipeline/blob/master/config/300-task.yaml)



## ¿Argo CD?

**Argo CD** is a delivery tool (CD) built for Kubernetes, based on [GitOps movement](https://www.cloudbees.com/gitops/what-is-gitops). So, what that means? Basically that Argo CD works synchronizing "Kubernetes files" between a git repository and a Kubernetes cluster. That is, if there is a change in a YAML file, Argo CD will detect that there are changes and will try to apply those changes in the cluster. 

Argo CD, like Tekton, also creates [its own Kubernetes objects](https://github.com/argoproj/argo-cd/tree/master/manifests/crds) that are installed into the Kubernetes cluster. 



## State of the art

At the moment in which this post is being written, both tools are very "young". For instance, if we check the last releases we can see:

- **Argo CD**: 1.8.7
- **Tekton**: 0.21.0

I also like to check ThoughtWorks Technology Radar and if we check them in the radar, will see:

- **Argo CD**:  **Trial status** ([Vol. 22](https://www.thoughtworks.com/radar/platforms/argo-cd))
- **Tekton**:  **Assess status** ([Vol. 23](https://www.thoughtworks.com/radar/platforms/tekton))

So, we are facing two young platforms and that may imply that there are not many examples, documentation or even maturity failures, but it's true that both tools are called to be the standard cloud native CI/CD according to the principal cloud players.

For instance, **Tekton**:

- **Google Cloud**: https://cloud.google.com/tekton?hl=es
- **Red Hat**, Openshift Pipelines based on Tekton: (https://www.openshift.com/learn/topics/pipelines)
- **IBM**: https://www.ibm.com/cloud/blog/ibm-cloud-continuous-delivery-tekton-pipelines-tools-and-resources
- **Tanzu**: https://tanzu.vmware.com/developer/guides/ci-cd/tekton-what-is/
- **Jenkins X**: pipelines based on Tekton  (https://jenkins-x.io/es/docs/concepts/jenkins-x-pipelines)

And, talking about **Argo CD**:

- **Red Hat**: https://developers.redhat.com/blog/2020/08/17/openshift-joins-the-argo-cd-community-kubecon-europe-2020/
- **IBM**: https://www.ibm.com/cloud/blog/simplify-and-automate-deployments-using-gitops-with-ibm-multicloud-manager-3-1-2



## ¿CI/CD Cloud Native?

We're talking a lot about "cloud native" associated to Tekton y Argo CD but, what do we mean by that? As I said before, both Tekton and Argo CD are installed in the Kubernetes cluster and they are based on extending Kubernetes API. Let's see it in detail:

- **Scalability**: both tools are installed in the cluster and because of that, they work creating pods to perform tasks. Pods are the way in which applications can scale horizontally...so, scalabilly are guaranteed

- **Portabillity**: both tools are based on extending Kubernetes API, creating new Kubernetes objects. These objects can be installed in every Kubernetes cluster.

- **Reusability**: the different elements within the CI/CD process use the Kubernetes objects defined by Tekton and Argo CD in the same way that you work with deployments o service objects. That means that stages, tasks or applications are YAML files that you can store in some repository and use in every cluster with Tekton and Argo CD installed. For instance, it's possible to use artifacts from [Tekton catalog](hub/catálogo asociado directamente al proyecto Tekton) or even, it's possible to use the [Openshift catalog](https://github.com/openshift/pipelines-catalog) or building a custom one. 



## Hands-on!

### What are we going to build?

We are going to build a simple CI/CD process, on Kubernetes, with these stages:

![pipeline-stages](/images/tekton-argocd/pipeline-stages.png)



In this pipeline, we can see two different parts:

- **CI part**, implemented by Tekton and ending with a stage in which a push to a repository is done.
- **CD part**, implemented by Argo CD, in which Argo CD detects that the repository has changed and perform the sync action against the Kubernetes cluster.

**Does it mean that we can not implement the whole process using Tekton?** No, it doesn't. It's possible to implement the whole process using Tekton but in this case, I want to show the **Gitops concept**.

<br />

### Requirements

To execute this PoC it's you need to have:

- A Kubernetes cluster. If you don't have one, you can create a K3D one using the script **create-local-cluster.sh** but, obviously, you need to have installed [K3D](https://k3d.io/)
- Docker
- Kubectl

<br />

### Repository structure

I've used a single repo to manage the different projects. The repository is structured in this way:

![repo_org](/images/tekton-argocd/repo_org.png)



Basically:

- **poc**: this is the main folder. Here, you can find three scripts:
  - create-local-cluster.sh: this script creates a local Kubernetes cluster based on [K3D](https://k3d.io/).
  - delete-local-cluster.sh: this script removes the local cluster
  - setup-poc.sh: this script installs and configure everything neccessary in the cluster (Tekton, Argo CD, Nexus, Sonar, etc...)
- **resources**: this the folder used to manage the two repositories (code and gitops):
  - sources-repo: source code of the service used in this poc to test the CI/CD process
  - gitops_repo: repository where Kubernetes files associated to the service to be deployed are



### Ok, how do I execute it?

#### 1) Fork

The first step is to fork the repo https://github.com/jaruizes/tekton-argocd-poc because:

- You have to modify some files to add a token
- You need your own repo to perform Gitops operations

<br />

### 2) Add Github token

It's necessary to add a Github Personal Access Token to Tekton can perform git operations, like push to gitops repo. If you need help to create this token, you can follow these instructions: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token

> ** The token needs to be allowed with "repo" grants.

Once the token is created, you have to copy it in these files (## INSERT TOKEN HERE:

- **poc/conf/argocd/git-repository.yaml**

  ```
  apiVersion: v1
  kind: Secret
  metadata:
    annotations:
      managed-by: argocd.argoproj.io
    name: repo-gitops
    namespace: argocd
  type: Opaque
  stringData:
    username: tekton
    password: ## INSERT TOKEN HERE
  ```

<br />

- **poc/conf/tekton/git-access/secret.yaml**

  ```
  apiVersion: v1
  kind: Secret
  metadata:
    name: git-auth
    namespace: tekton-poc
    annotations:
      tekton.dev/git-0: https://github.com
  type: kubernetes.io/basic-auth
  stringData:
    username: tekton
    password: ## INSERT TOKEN HERE
  ```

<br />

> ** In fact, for Argo CD, create secret with the token isn't necessary because the gitops repository in Github has public access but I think it's interesting to keep it in order to know what you need to do in case the repository be private.

<br />

### 3) Create Kubernetes cluster (optional)

This step is optional. If you already have a cluster, perfect, but if not, you can create a local one based on K3D, just executing the script **poc/create-local-cluster.sh**. This script creates the local cluster and configure the private image registry to manage Docker images.

<br />

### 4) Setup

This step is the most important because installs and configures everything necessary in the cluster:

- Installs Tekton y Argo CD, including secrets to access to Git repo
- Creates the volume and claim necessary to execute pipelines

- Deploys Tekton dashboard

- Deploys Sonarqube

- Deploys Nexus

- Creates the configmap associated to Maven settings.xml, ready to publish artifacts in Nexus (with user and password)

- Installs Tekton tasks and pipelines

  - Git-clone (from Tekton Hub)
  - Maven (from Tekton Hub)
  - Buildah (from Tekton Hub)
  - Prepare Image (custom task: poc/conf/tekton/tasks/prepare-image-task.yaml)
  - Deploy with Argo CD (custom task: poc/conf/tekton/tasks/deploy-with-argocd.yaml)

- Installs Argo CD application, configured to check changes in gitops repository (resources/gitops_repo)

> ** Be patient. The process takes some minutes.

<br />

** **This message isn't an error**. It just waiting for to Nexus admin password created when the container starts. When the Nexus container starts, at some moment, it creates a file containing the default password.

```
Configuring settings.xml (MAVEN) to work with Nexus
cat: /nexus-data/admin.password: No such file or directory
command terminated with exit code 1
```

<br />

### 5) Explore and play

Once everything is installed, you can:

- Check Tekton dashboard:

  Tekton dashboard could be exposed locally using this command:

  ```bash
  kubectl proxy --port=8080
  ```

  Then, just open this url in the browser:

  ```bash
  http://localhost:8080/api/v1/namespaces/tekton-pipelines/services/tekton-dashboard:http/proxy/#/namespaces/default/pipelines
  ```

  <br />

  In the dashboard, you need to select "tekton-poc" namespace to see the pipelines used in this PoC:
  
  ![tekton-dashboard-namespace](/images/tekton-argocd/tekton-dashboard-namespace.png)
  
  
  
  There is a pipeline created (example-ci-pipeline):
  
  ![example-pipeline](/images/tekton-argocd/example-pipeline.png)
  
  
  
  To see pipeline executions, we have to go to "PipelineRuns" options in the sidebar:
  
  ![pipeline-runs](/images/tekton-argocd/pipeline-runs.png)
  
  
  
  At this dashboard, you can check pipeline executions and trigger new ones:

![pipeline](/images/tekton-argocd/pipeline.png)



La acción de **deploy** realiza un push al repositorio de gitops y ArgoCD sincroniza el despliegue

El dashboard de ArgoCD se puede exponer mediante el comando:

```
kubectl port-forward svc/argocd-server -n argocd 9080:443
```

Y se accede al mismo en la url http://localhost:9080:

![argocd](poc/doc/img/argocd.png)

El usuario es admin y la contraseña se indica al finalizar el proceso de setup (script **setup_poc.sh** ) pero también se puede obtener con el comando:

```bash
kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```
