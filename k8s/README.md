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

## AWS EKS

1. Install aws cli (AWS Documentation)

2. Create a user in IAM.

3. Configure aws CLI with user credentials

    $ aws configure

4. Validate which user is configured in aws CLI

    $ aws sts get-caller-identity

5. Install eksctl

    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

    $ brew tap weaveworks/tap

    $ brew install weaveworks/tap/eksctl

    $ eksctl version

6. Install Kubectl MacOS Apple-silicon M1

    $ curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.22.6/2022-03-09/bin/darwin/amd64/kubectl

    $ chmod +x ./kubectl

    $ sudo cp ./kubectl /usr/local/bin/kubectl

    $ sudo chown root: /usr/local/bin/kubectl

    $ export PATH=$HOME/bin:$PATH

    $ echo 'export PATH=$PATH:$HOME/bin' >> ~/.zshrc

    $ kubectl version --short --client

7. Create a cluster with eksctl in aws

    $ eksctl create cluster \ 
      --name <cluster name> \ 
      --region <region> \ 
      --zones <zone a>,<zone b> \
      --without-nodegroup

8. Configure kubeconfig to connect to the cluster

    $ aws eks \
      --region <region> update-kubeconfig \
      --name <cluster name>

9. View cluster information

    $ kubectl cluster-info

10. Creating a managed node group

    eksctl create nodegroup \
      --cluster <cluster name> \
      --region <region> \
      --name <workers name> \
      --node-type t2.small \
      --nodes 1 \
      --nodes-min 1 \
      --nodes-max 3 \
      --ssh-access \
      --asg-access

11. Implemente una AWS Load Balancer Controller en un clúster de Amazon EKS.

    $ eksctl utils associate-iam-oidc-provider \
      --region <region> \
      --cluster <cluster name> \
      --approve

    $ aws iam create-policy \
      --policy-name AWSLoadBalancerControllerIAMPolicy \
      --policy-document https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.2/docs/install/iam_policy.json

    $ eksctl create iamserviceaccount \
      --cluster <cluster name> \
      --region <region> \
      --namespace kube-system \
      --name alb-ingress-controller \
      --attach-policy-arn <arn:aws:iam::856536748046:policy/AWSLoadBalancerControllerIAMPolicy> \
      --override-existing-serviceaccounts \
      --approve

    $ kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-alb-ingress-controller/v1.1.4/docs/examples/rbac-role.yaml
    
    $ kubectl apply \
    --validate false \
    -f https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml

    $ kubectl apply -f https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.2/v2_4_2_full.yaml

    $ kubectl get deployment -n kube-system aws-load-balancer-controller

12. Create ingress controller App

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  namespace: game-2048
  name: ingress-2048
  labels:
    app: ingress-2048
  annotations:
    kubernetes.io/ingress.class: alb
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
spec:
  rules:
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: service-2048
                port:
                  number: 80
```

Get the ingress created

    $ kubectl get ingress -n <namespace>

