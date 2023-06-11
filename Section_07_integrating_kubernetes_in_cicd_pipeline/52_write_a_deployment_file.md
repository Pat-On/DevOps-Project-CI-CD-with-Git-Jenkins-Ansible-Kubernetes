# Deployment File

```
apiVersion: apps/v1 
kind: Deployment        # Deployment name and Deployment label
metadata:
  name: devops-regapp
  labels: 
     app: regapp        # have to match selectors for example in the service

spec:
  replicas: 2                   # create 2 pods from the pod template
  selector:
    matchLabels:
      app: regapp

  template:
    metadata:                   # pod definition
      labels:
        app: regapp
    spec:
      containers:               # template to create a pod
      - name: regapp            # container definition
        image: patvon/regapp
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
  strategy:                     # make sure only one pod updated at a time 
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```


Service file:
```
apiVersion: v1
kind: Service
metadata:
  name: devops-service
  labels:
    app: regapp 
spec:
  selector:                 # To which deployment it can send traffic
    app: regapp 

  ports:
    - port: 8080
      targetPort: 8080

  type: LoadBalancer
```