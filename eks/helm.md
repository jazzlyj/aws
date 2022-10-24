# Helm
Helm is a package manager and application management tool for Kubernetes that packages multiple Kubernetes resources into a single logical deployment unit called a Chart.

Helm helps you to:

* Achieve a simple (one command) and repeatable deployment
* Manage application dependency, using specific versions of other application and services
* Manage multiple deployment configurations: test, staging, production and others
* Execute post/pre deployment jobs during application deployment
* Update/rollback and test application deployments

reference:
https://www.eksworkshop.com/beginner/060_helm/helm_intro/


## Install the command line tools

```
curl -sSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

verify the version
```
helm version --short
```

## Configure first Chart repository. 
Chart repositories are similar to APT or yum repositories. Download the stable repository to have something to start with:

```
helm repo add stable https://charts.helm.sh/stable
```

## List the charts you can install:

```
helm search repo stable
```

## Configure Bash completion for the helm command:

```
helm completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
source <(helm completion bash)
```


# Install Jenkins

* Add repo
```
helm repo add jenkins https://charts.jenkins.io
```

* Install
```
helm install jenkins jenkins/jenkins --set rbac.create=true,controller.servicePort=80,controller.serviceType=LoadBalancer
```


* Uninstall
```
helm uninstall jenkins
```


