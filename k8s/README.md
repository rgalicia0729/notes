# Kubernetes

View kubernetes api version

    $ kubectl api-versions

View api resources

    $ kubectl api-resources

## Pods

Generate yml file to create a pod "create-pod.yaml"

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
```
Apply a manifest

    $ kubectl apply -f <manifest name>

Remove resources from a manifest

    $ kubectl delete -f <manifest name>

Get the list of pods

    $ kubectl get pods | po

Show more information about a pod

    $ kubectl get pods -o wide

View a pod description

    $ kubectl describe pod <pod name>

Remove a pod

    $ kubectl delete pod <pod name>

Get the yaml from a pod

    $ kubectl get pod <pod name> -o yaml

Por forward pod

    $ kubectl port-forward <pod name> 8080:<pod port>

Interactive mode of a pod

    $ kubectl exec -it <pod name> -- sh

View the logs of a pod

    $ kubectl logs <pod name>

    $ kubectl logs <pod name> -f

Run two containers in one pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: two-containers-pod
spec:
  containers:
    - name: container1
      image: python:3.6-alpine
      command:
        [
          "sh",
          "-c",
          "echo container1 > index.html && python -m http.server 8080",
        ]
    - name: container2
      image: python:3.6-alpine
      command:
        [
          "sh",
          "-c",
          "echo container2 > index.html && python -m http.server 8080",
        ]
```
Select a container from a pod running two containers

    $ kubectl logs <pod name> -c <container name>

Filter pods by labels

    $ kubectl get pods -l <tag=value>

Add a label to a pod that is running

    $ kubectl label pod <pod-name> <tag=value>

## ReplicaSets

```yaml
apiVersion: apps/v1
Kind: ReplicaSet
metadata:
  name: test-replicaset
  labels:
    app: test
spec:
  replicas: 3
  selector:
    matchLabels:
      app: pod-test
  template:
    metadata:
      labels:
        app: pod-test
    spec:
      containers:
        - name: container-test
          image: nginx:alpine
```
Get the list of replica set

    $ kubectl get replicaset | rs

Get the yaml from a replica set

    $ kubectl get rs <replica set name> -o yaml

## Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-test
  annotations:
    kubernetes.io/change-cause: "Change port to 80"
  labels:
    app: front
spec:
  replicas: 3
  selector:
    matchLabels:
      app: front
  template:
    metadata:
      labels:
        app: front
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80

```
Show the labels of a deployment

    $ kubectl get deployment --show-labels

View the status of a deployment

    $ kubectl rollout status deployment <deployment name>

View rollout history

    $ kubectl rollout history deployment <deployment name>

View review status

    $ kubectl rollout history deployment <deployment name> --revision=<revision number>

change review

    $ kubectl rollout undo deployment <deployment name> --to-revision=<revision number>

## Services

```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-test
  labels:
    app: app-web
spec:
  selector:
    app: app-web
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 80
```

## Namespaces

See the namespaces

    $ kubectl get namespaces

Create a namespace

    $ kubectl create namespace <namespace name>

Create a namespaces through a yaml

```yaml
apiVersion: v1
kind: Namespaces
metadata:
  name: develop
  label:
    name: develop
```

See namespace labels

    $ kubectl get namespaces --show-labels

Describe a namespace

    $ kubectl describe namespace <namespace name>

Delete a namespace

    $ kubectl delete namespace <namespace name>