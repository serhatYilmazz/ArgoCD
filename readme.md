Install Ambassador
Blue/Green deployments can work on any vanilla Kubernetes cluster. But for Canary deployments you need a smart service layer that can gradually shift traffic to the canary pods while still keeping the rest of the traffic to the old/stable pods.

Argo Rollouts supports several service meshes and gateways for this purpose.

In this lesson we will use the popular Ambassador API Gateway for Kubernetes to split live traffic between the canary and old/stable version.

We installed Argo CD for you and you can login in the UI tab.

Click the "New app" button on the top left and fill the following details:

application name : ambassador
project: default
SYNC POLICY: automatic
AUTO-CREATE Namespace: enabled
repository URL: https://github.com/codefresh-contrib/gitops-certification-examples
path: ./ambassador-chart
Cluster: https://kubernetes.default.svc (this is the same cluster where ArgoCD is installed)
Namespace: ambassador
Leave all the other values empty or with default selections. Finally click the Create button. The Ambassador Gateway will be installed on the cluster.

Notice that we are not using the default namespace, but a brand new one. It is imperative that you select the "auto-create namespace" option.

auto-create

If you don't select this option, ArgoCD will not find the namespace and deployment will fail. Delete the application and create it again if you have a deployment issue.

You can also manually do if you forgot it in the UI:

kubectl create namespace ambassador
Try syncing again the application.

Again, you can see that GitOps is not only useful for your own applications but also for other supporting applications as well.

Wait some time until the gateway is fully synced and the deployment is marked as Healthy.

Once you are ready to proceed, press Check.