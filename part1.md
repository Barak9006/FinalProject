## Deploy a pod named nginx-pod using the nginx:alpine image.
```
kubectl run nginx-pod-barak --image nginx:alpine
```
-------------------------------------------------------------
## Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.
```
kubectl run messaging --image redis:alpine --labels tier=msg
```
-----------------------------------------------------------
## Create a namespace named apx-x998-yourname
```
kubectl create namespace apx-x998-barak
```
---------------------------------------------
## Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname
```
kubectl get nodes -o json > ./tmp/nodes-barak
```
----------------------------------------
## Create a service messaging-service to expose the messaging application within the
cluster on port 6379.
```
kubectl expose pod messaging --type ClusterIP --port 6379 --name messaging-service
```
```
And with Yaml:(created with vi)
/apiVersion: v1
kind: Service
metadata:
  name: messaging-service
spec:
  selector:
    app: messaging
  ports:
    - protocol: TCP
      port: 6379
      targetPort: 6379
  type: ClusterIP
/
```
-------------------------------------------------------
## Create a deployment named hr-web-app using the image kodekloud/webapp-color
```
kubectl create deployment hr-web-app --image kodekloud/webapp-color --replicas 2
```
---------------------------------------------------------------------------------------
## Create a static pod named static-busybox on the master node that uses the busybox
image and the command sleep 1000
```
I did json file and moved it to Manifests folder.
```
```
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "static-busybox",
    "namespace": "default"
  },
  "spec": {
    "containers": [
      {
        "name": "busybox-container",
        "image": "busybox",
        "command": ["sleep", "1000"]
      }
    ],
    "restartPolicy": "Never"  //static 
  }
}
```
-------------------------------------------------------------------------------
## Create a POD in the finance-yourname namespace named temp-bus with the image
redis:alpine
```
kubectl create namespace finance-barak
kubectl run temp-bus --image redis:alpine --namespace finance-barak
```
--------------------------------------------------------------------------------------
## Create a Persistent Volume with the given specification
```
yaml:
```
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: /pv/data-analytics #created automatically
```
----------------------------------------------------------------
## Q11:Create a Pod called redis-storage-yourname with image: redis:alpine with a Volume
of type emptyDir that lasts for the life of the Pod.
```
yaml:
```
```
apiVersion: v1
kind: Pod
metadata:
  name: redis-storage-barak
spec:
  containers:
  - name: redis-container
    image: redis:alpine
    volumeMounts:
    - name: redis-storage
      mountPath: /data/redis
  volumes:
  - name: redis-storage
    emptyDir: {}
```
-------------------------------------------------------
## Q12: 12. Create this pod and attached it a persistent volume called pv-1
a. Make sure the PV mountPath is hostbase : /data
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: use-pv
  name: use-pvspec-yourname
spec:
  containers:
  - image: nginx
    name: use-pv
    resources: {}
    volumeMounts:
    - name: pv-1
      mountPath: /data
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
  - name: pv-1
```
------------------------------
## Q13:
```
kubectl create deployment nginx-deploy --image nginx:1.16 --replicas 1 --record
kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record=true
```
------------------------------------------------
## Q14:
```
kubectl run nginx-resolver --image nginx
kubectl expose pod nginx-resolver --name nginx-resolver-service --port 80
kubectl run busybox --image busybox:1.28 -it -- /bin/sh
```
```
doing nslookup command to record results
```
----------------------------------------
## Q15:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-critical
spec:
  containers:
    - name: nginx
      image: nginx
  restartPolicy: Always
```
--------------------
##Q16:
```
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  containers:
    - name: alpha
      image: nginx
      env:
        - name: alpha
          
    - name: beta
      image: busybox
      command: ["sleep", "4800"]
      env:
        - name: beta
```
---------------------------------------
--------------------------------------






 

