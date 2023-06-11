# Basic commands:

kubectl create deployment  demo-nginx --image=nginx --replicas=2 --port=80
- kubectl deployment regapp --image=valaxy/regapp --replicas=2 --port=8080
kubectl get all
kubectl get pod


kubectl expose deployment demo-nginx --port=80 --type=LoadBalancer
- kubectl expose deployment regapp --port=8080 --type=LoadBalancer
kubectl get services -o wide


Small recap of the process:
```
                                        POD
Deploy ----> Replica set------------>            <------------- SVC (SERVICE) 
            init in background          POD                     in our example LB
```


Output:
```
[root@ip-172-31-7-181 ~]# kubectl get all
NAME                              READY   STATUS    RESTARTS   AGE
pod/demo-nginx-56c89b8bfd-bwzzz   1/1     Running   0          6m23s
pod/demo-nginx-56c89b8bfd-vllqm   1/1     Running   0          6m23s

NAME                 TYPE           CLUSTER-IP     EXTERNAL-IP                                                               PORT(S)        AGE
service/demo-nginx   LoadBalancer   10.100.29.33   a8d34dce8df5e4aebbb86f0afdbe3fde-1500350500.eu-west-1.elb.amazonaws.com   80:30921/TCP   3m8s
service/kubernetes   ClusterIP      10.100.0.1     <none>                                                                    443/TCP        108m

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/demo-nginx   2/2     2            2           6m23s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/demo-nginx-56c89b8bfd   2         2         2       6m23s
```