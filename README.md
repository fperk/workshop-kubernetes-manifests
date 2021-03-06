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

`kubectl logs <pod_name>`

`kubectl -n <namespace_name> exec -it <pod_name> -- /bin/sh`

`kubectl -n <namespace_name> port-forward service/<servicename> <local_port>:<service_port>`

`kubectl -n <namespace_name> port-forward <pod_name> <local_port>:<pod_port>`

We can also describe a specific resource `kubectl describe namespaces <namespace_name>`

## Kubernetes Resources

`<namespace_name> = <username>`

If you want to change the <namespace_name> to your <username> just execute this command in the manifests directory:

```
USERNAME=$(whoami) && \
find . -type f -name "*.yaml" -print0 | xargs -0 sed -i "s/<namespace_name>/$USERNAME/g" && \
find . -type f -name "ingress.yaml" -print0 | xargs -0 sed -i "s/<username>/$USERNAME/g"
```

### Namespace

#### Create Namespace

```sh
kubectl create namespace <namespace_name>
```

For example:

```sh
kubectl create namespace fpe
```

We can also create a Namespace with a kubernetes manifest:

```sh
kubectl create -f namespace.yaml
``` 

In Kubernetes you can choose between the `yaml` and `json` format.

#### Delete Namespace

> WARNING: This deletes everything under the namespace!

```sh
# kubectl delete namespaces <namespace_name>
```

### Pod

`kubectl get pods --namespace <namespace_name>` is the same as `kubectl get pods -n <namespace_name>`

```sh
kubectl create -f pod.yaml
```

`kubectl delete -f pod.yaml` or `kubectl -n <namespace_name> delete pod <pod_name>`

### ConfigMap

```sh
kubectl create -f configmap.yaml
```

`kubectl delete -f configmap.yaml` or `kubectl -n <namespace_name> delete configmap <configmap_name>`

### Secret

```sh
kubectl create secret <type> <secret_name>

kubectl create secret generic <secret_name>

kubectl -n <namespace_name> get secret <secret_name>

kubectl -n <namespace_name> describe secret <secret_name>

kubectl -n <namespace_name> get secret <secret_name> -o jsonpath='{.data}'

kubectl create -f secret.yaml

kubectl delete -f secret.yaml
```

### PVC / PV

```sh
kubectl -n <namespace_name> describe pvc <pvc_name>

kubectl create -f pvc.yaml

kubectl delete -f pvc.yaml
```

### Deployment

```sh
kubectl create -f deployment.yaml

kubectl delete -f deployment.yaml
```

### Service

```sh
kubectl -n <namespace_name> describe service <service_name>

kubectl create -f service.yaml

kubectl delete -f service.yaml
```

### Ingress

```sh
kubectl create -f ingress.yaml
```

### CronJob

```sh
kubectl create -f cronjob.yaml
```

### Statefulset

```sh
kubectl create -f statefulset.yaml

kubectl delete -f statefulset.yaml

kubectl -n <namespace_name> scale statefulsets <stateful-set-name> --replicas=<new-replicas>
```

### DaemonSet

```sh
kubectl create -f daemonset.yaml
```
