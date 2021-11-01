# Kubernetes Workshop

## Access to the cluster

We have to reach `kula-001` (Bastion host) to access the cluster:

```sh
$ ssh -i <ssh_private_key_path> <username>@kula-001.workshop.exanio.net
```

From there on we can communicate with the Cluster by exporting the `KUBECONFIG` variable to our `env`ironment:

```sh
$ export KUBECONFIG=/opt/kubeconfig
$ kubectl get nodes
```

## Kubernetes Basics

`kubectl get <resource>` is the same like `kubectl get <resource_abbrevation>`

`kubectl get namespace` is the same like `kubectl get ns`

`kubectl get service` is the same like `kubectl get svc`

`kubectl describe <resources>` ie. `kubectl get namespaces`

`kubectl get pod -o wide`

We can also describe a specific resource `kubectl describe namespaces <namespace_name>`

## Kubernetes Resources

### Namespace

#### Create Namespace

`kubectl create namespace <username>`

For example:

`kubectl create namespace fpe`

We can also create a Namespace with a kubernetes manifest:

`kubectl create -f namespace.yaml` (this can also be a json file)

#### Delete Namespace

`Warning: This deletes everything under the namespace!`

`kubectl delete namespaces <insert-some-namespace-name>`

### Pod

`kubectl get pods --namespace <username>` is the same as `kubectl get pods -n <username>`

`kubectl create -f pod.yaml`

`kubectl delete -f pod.yaml` or `kubectl delete pod <pod_name>`

### ConfigMap

`kubectl create -f configmap.yaml`

`kubectl delete -f configmap.yaml` or `kubectl delete configmap <configmap_name>`

### Secret

`kubectl create secret <type> <secret_name>`

`kubectl create secret generic <secret_name>`

`kubectl get secret <secret_name>`

`kubectl create -f secret.yaml`

`kubectl delete -f secret.yaml`

### PVC / PV

`kubectl describe pvc <pvc_name>`

`kubectl create -f pvc.yaml`

`kubectl delete -f pvc.yaml`

### Service

`kubectl describe service <service_name>`

`kubectl create -f service.yaml`

`kubectl delete -f service.yaml`

### Deployment

`kubectl create -f deployment.yaml`

`kubectl delete -f deployment.yaml`

### Statefulset

scale

### DaemonSet

### Ingress

`kubectl create -f ingress.yaml`

`kubectl delete -f ingress.yaml`