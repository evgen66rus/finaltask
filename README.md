# How to launch this environment

### Create configmap
`kubectl create -f env-configmap.yaml`

### Create redis statefull set
`kubectl create -f redis-pod.yaml`

### Create redis service
`kubectl create -f redis-service.yaml`

### Create redis cluster
`kubectl exec -it redis-cluster-0 -- redis-cli --cluster create \
$(kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}{":6379"}{"\t"}' \
| awk '{print $1 " " $2 " " $3 " " $4 " " $5 " " $6}')`

