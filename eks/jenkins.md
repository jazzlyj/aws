# Jenkins via Helm Chart
https://github.com/jenkinsci/helm-charts/blob/main/charts/jenkins/README.md

```
helm repo add jenkins https://charts.jenkins.io
helm repo update
helm search repo jenkins




helm show values jenkins/jenkins | less

```


## Install
* Pick a name to use for the release name


```
helm install jenkins jenkins/jenkins --set rbac.create=true,controller.servicePort=80,controller.serviceType=LoadBalancer



### std out
NAME: jenkins
LAST DEPLOYED: Mon Oct 24 05:34:48 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get your 'admin' user password by running:
  kubectl exec --namespace default -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
2. Get the Jenkins URL to visit by running these commands in the same shell:
  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        You can watch the status of by running 'kubectl get svc --namespace default -w jenkins'
  export SERVICE_IP=$(kubectl get svc --namespace default jenkins --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
  echo http://$SERVICE_IP:80/login

3. Login with the password from step 1 and the username: admin
4. Configure security realm and authorization strategy
5. Use Jenkins Configuration as Code by specifying configScripts in your values.yaml file, see documentation: http:///configuration-as-code and examples: https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos

For more information on running Jenkins on Kubernetes, visit:
https://cloud.google.com/solutions/jenkins-on-container-engine

For more information about Jenkins Configuration as Code, visit:
https://jenkins.io/projects/jcasc/


NOTE: Consider using a custom image with pre-installed plugins
eksworkshop:~/environment $ 




```

### Get password
```
kubectl exec --namespace default -it svc/jenkins-test -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
```





```

```
```

```
```

```
```

```
```

```

