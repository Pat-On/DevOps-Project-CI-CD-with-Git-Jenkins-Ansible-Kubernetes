# Setup Kubernetes using eksctl

```
eksctl create cluster --name patvon  \
--region eu-west-1 \
--node-type t2.small \
```

## important file to access our node 
`/root/.kube/config`
- it has this 'power' because f hte `certificate-authority-data`


## removing the cluster - save money!

```
eksctl delete cluster patvon --region eu-west-1
```