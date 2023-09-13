## Q1. 
```
kubectl get pods --show-labels #Get pods with label information
```
## Q2.
```
YAML code:
```
```
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-prod1
  labels:
    app: nginx
    env: prod
spec:
  containers:
    - name: nginx
      image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-prod2
  labels:
    app: nginx
    env: prod
spec:
  containers:
    - name: nginx
      image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-dev1
  labels:
    app: nginx
    env: dev
spec:
  containers:
    - name: nginx
      image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-dev2
  labels:
    app: nginx
    env: dev
spec:
  containers:
    - name: nginx
      image: nginx

---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-dev3
  labels:
    app: nginx
    env: dev
spec:
  containers:
    - name: nginx
      image: nginx
```
-----------------------------
```
kubectl get pods -l env=dev
kubectl get pods --selector env=dev -o json | jq -r '.items[] | "Pod: \(.metadata.name) Labels: \(.metadata.labels)"' > Podlist
#Command above output to PodList  the pods with env=dev  with the label names.
kubectl get pods -l env=prod
kubectl get pods --selector env=prod -o json | jq -r '.items[] | "Pod: \(.metadata.name) Labels: \(.metadata.labels)"' > Podlist
#Command above output to PodList  the pods with env=prod  with the label names.
```
## Q8.
```
kubectl get pod -l env
```
## Q9.
```
kubectl get pods -l 'env in (dev,prod)'
```
## Q10.
```
kubectl get pods -l 'env in (dev,prod)' -o custom-columns="NAME:.metadata.name,ENV:.metadata.labels.env" > Podlist
#Command above output to PodList the pods with env=prod and env=dev with the label names.
```
## Q11.
```
kubectl label pods -l env=dev env=uae
```
## Q12.
```
kubectl label pods -l env env-
```
## Q13.
```
kubectl label pods nginx-dev1 app=nginx #do this for all pods
```
## Q14.
```
kubectl get nodes -o custom-columns=NAME:.metadata.name,LABELS:.metadata.labels
```
## Q15.
```
kubectl label nodes minikube nodeName=nginxnode
```
## Q16:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    run: nginx
spec:
  nodeSelector:
    nodeName: nginxnode
  containers:
  - name: nginx
    image: nginx
  dnsPolicy: ClusterFirst
  restartPolicy: Never
```
## Q17:
```
Node:             minikube/192.168.49.2
```
## Q18:
```
works
```


