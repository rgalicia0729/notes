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

    $ kubectl get pods

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
