# Manifest files


Link:
- https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/#pods-created-via-http

pod.yml
```
apiVersion: v1
kind: Pod
metadata:
  name: demo-pod
  labels:
    app: demo-app
spec:
  containers:
    - name: demo-nginx
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP
```