## Q1.
```
barakuva@cloudshell:~$ cat config.txt
key1=value1
key2=value2
```
## Q2.
```
kubectl create configmap keyvalcfgmap --from-file=config.txt
barakuva@cloudshell:~$ kubectl describe configmap keyvalcfgmap
Name:         keyvalcfgmap
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
config.txt:
----
key1=value1
key2=value2


BinaryData
====

Events:  <none>
```
## Q3.
```
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml \
  --overrides='
  {
    "spec": {
      "containers": [
        {
          "name": "nginx",
          "image": "nginx",
          "envFrom": [
            {
              "configMapRef": {
                "name": "keyvalcfgmap"
              }
            }
          ]
        }
      ]
    }
  }' > nginx-pod.yml
barakuva@cloudshell:~$ kubectl exec -it nginx -- /bin/sh
# echo $key1

# echo $key2  

# exit
```

kubectl delete pod nginx
