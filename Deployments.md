Q1:
in Yaml:
spec:
replicas: 5 # edited to 5 from 1

Q2.
kubectl rollout status deployment/webapp

Q3.
kubectl get replicasets -l app=webapp

Q4.
kubectl get replicasets -l app=webapp -o yaml > webapp-replicaset.yaml
kubectl get pods -l app=webapp -o yaml > webapp-pods.yaml

Q5.
kubectl delete deployment webapp

Q6.
add to the Yaml:
spec:
      containers:
      - image: nginx:1.17.1
        name: nginx
        ports:
        - containerPort: 80 #added

Q7.
kubectl set image deployment/webapp nginx=nginx:1.17.4
kubectl rollout status deployment/webapp

Q8.
kubectl rollout history deployment/webapp

Q9.
kubectl rollout undo deployment/webapp #undo
kubectl rollout status deployment/webapp #check undo status
kubectl describe deployment/webapp | grep "Image:" | awk '{print $2}' #shows only the image and the version without the extra information

Q10.
barakuva@cloudshell:~$ kubectl get pods
NAME                      READY   STATUS         RESTARTS   AGE
webapp-58db9dc58f-zdrpl   0/1     ErrImagePull   0          9s
webapp-76bffbdf95-4j9j9   1/1     Running        0          3m40s
kubectl rollout undo deployment/webapp
kubectl rollout status deployment/webapp #ok

Q11.
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: webapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: webapp
  minReplicas: 10
  maxReplicas: 20
  metrics:
    - type: Resource
      resource:
        name: cpu
        targetAverageUtilization: 85

Q12.
kubectl delete deployment webapp
kubectl delete hpa webapp-hpa

Q14.
apiVersion: batch/v1
kind: Job
metadata:
  name: hello-job
spec:
  completions: 10
  template:
    spec:
      containers:
      - name: hello-job
        image: busybox
        command: ["echo", "Hello, I am from the job"]
        resources: {}
      restartPolicy: Never

        


