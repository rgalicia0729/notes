# Kubernetes

View kubernetes api version

    $ kubectl api-versions

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



