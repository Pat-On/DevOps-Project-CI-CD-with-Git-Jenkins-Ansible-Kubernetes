# Using Labels and Selectors

- basically it is mapping in this case from the LB to the backend service
  
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

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  ports:
    - name: nginx-port
      protocol: TCP
      port: 80
      targetPort: 80
  selector:
    app: demo-app
  type: LoadBalancer

```

## command to run this files

- `kubectl apply -f <file_name>`

to look deeper:
- kubectl describe <name_of_the_existing_resource>

