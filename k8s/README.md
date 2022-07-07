# Kubernetes

View api resources

    $ kubectl api-resources

Generate yml file to create a pod "create-pod.yaml"

```yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
```

    $ kubectl apply -f create-pod.yml

Get the list of pods

    $ kubectl get pods

View a pod description

    $ kubectl describe pod <pod name>

Remove a pod

    $ kubectl delete pod <pod name>

Get the yaml from a pod

    $ kubectl get pod <pod name> -o yaml



