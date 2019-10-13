https://app.pluralsight.com/library/courses/getting-started-kubernetes/table-of-contents

# What is k8s.

Born in Goodle

# Architecture

## Big picture

### Master
- kubi-apiserver
- cluster store (uses etcd - distributed, consistent key-value storage)
- kube-controller-manager (node, enpoint, namespace - wathces the changes)
- kube-scheduler (watch apiserver for new pods)

### Nodes
- Kubelet (k8s agent: watch apiserver, insantiate pods. :10255 /spec /healthz /pods)
- container engine
- kube-proxy (all container in pods has the same IP)

### Desired Model and desired state

### Pods.
Wrapper around container. (pod with few containers is advanced case with maincar and sidecar container).

### Services.

Load balance pods with the same labels.

## Installing 
On AWS.

1) Route 53 rule of outbound server to k8s
2) Local installation of kubectl:
```
brew install kubectl
brew install kops
```
3) Follow the guide:
https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html

4) On sandbox environment
`okta-aws pay_sandbox sts get-caller-identity` saves credentials from sandbox to test profile.
and then 
```
aws eks update-kubeconfig --name ledger-test3 --profile pay_sandbox
```
Then check
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/.

and also we need token to login:
https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html#awscli-install-osx-path

kubectl get pods -l app=wallet


## Pods
Pod is atomic unit of virtualization.

kubectl create -f pod.yml
kubectl get pods --all-namespaces
kubectl get pods

## Services

kubectl get service
kubectl get ep

http://kubernetesbyexample.com/

## Deployments
kubectl get rs

kubectl apply -f filename.yml --record=true
```
kubectl get deployment
kubectl rollout status deployment deployment_name
kubectl rollout history deployment deployment_name
```
--record flag to save history

