# Service - Manifest File

Link: https://kubernetes.io/docs/concepts/services-networking/service/

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
  type: LoadBalancer
```


Usage of labels to target the specific pod
```
                Selector:          Labels:
                app: demo-app      app: demo-app
External -------> Service ------>  POD
    PC


