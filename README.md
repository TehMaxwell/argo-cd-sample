# Argo CD Sample

A repository for playing with the Argo-CD Kubernetes deployment tools. Several sample Kubernetes manifests and helm charts are provided with different branches showing changes to manifests that can be applied using Argo CD.

#### SSH Key Generation in Windows using ssh-keygen

The following article provides some information on generation of SSH keys in Windows using the ssh-keygen utility.

https://www.purdue.edu/science/scienceit/ssh-keys-windows.html

#### ArgoCD Installation

Information on the installation of ArgoCD can be found here:

https://argo-cd.readthedocs.io/en/stable/getting_started/

#### Adding an Application in ArgoCD

The following command allows you to add an application to ArgoCD with a repository link. The application will be deployed on the cluster that the ArgoCD system is running in.

```bash
argocd app create {application_name} --repo https://github.com/argoproj/argocd-example-apps.git --path {path_to_repo_folder} --dest-namespace {kubernetes_namespace} --dest-server https://kubernetes.default.svc --directory-recurse
```

More information on application creation can be found here:

https://argo-cd.readthedocs.io/en/stable/user-guide/commands/argocd_app_create/

#### Horizontal Pod Autoscaling

More information on the Horiztonal Pod autoscaler can be found here:

https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

To autoscale an existing deployment, the following command can be used:

```bash
kubectl autoscale deployment {deployment_name} -n {namespace} --cpu-percent=50 --min=1 --max=10
```

#### Busybox Load Testing

The following command runs a busybox image and executes an HTTP request repeatedly in order to apply a load to the targetted service:

```bash
kubectl run -i --tty load-generator -n {namespace} --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://{service_name}:{service_port}; done"
```

Once running, pressing Ctrl-C will stop the loop and delete the pod that has been created. On productive clusters this may have to be changed into a deployment manifest that is applied to comply with certain pod security rules.