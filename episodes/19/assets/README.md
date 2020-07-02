# Guide

### CROSSPLANE

1. Install Crossplane

```
kubectl create namespace crossplane-system

helm repo add crossplane-alpha https://charts.crossplane.io/alpha

helm install crossplane --namespace crossplane-system crossplane-alpha/crossplane
```

2. Install `provider-gcp` and `provider-aws`

```
kubectl apply -f provider-gcp.yaml
kubectl apply -f provider-aws.yaml
```

3. Create `ClusterRole`s

```
kubectl apply -f roles/
```

4. Create `InfrastructureDefinition`s

```
kubectl apply -f definitions/
```

5. Create `Composition`s

```
kubectl apply -f compositions/
```

6. Create EKS Cluster

```
kubectl apply -f cluster-1.yaml
```

6. Create GKE Cluster

```
kubectl apply -f cluster-2.yaml
```

7. Get `kubeconfig`

```
kubectl get secret gke-conn -o=jsonpath={.data.kubeconfig} | base64 --decode > gke.kube
kubectl get secret eks-conn -o=jsonpath={.data.kubeconfig} | base64 --decode > eks.kube
```

8. Use `kubeconfig`

```
kubectl get nodes --kubeconfig=gke.kube
kubectl get nodes --kubeconfig=eks.kube
```

# FALCO/SYSDIG
### Falco 
1. Install Falco (in this case using helm): https://github.com/falcosecurity/charts/tree/master/falco
```
helm install falco falcosecurity/falco --set ebpf.enabled=true
```
2. Tail the falco pods logs (in one terminal)
```
kubectl logs -l app=falco -f
```
3. attack a POD! (In another)
```
kubectl exec -it *podname* bash
cd /bin
touch fakeexe
```

4. Uninstall Falco (in this case using helm): 
```
helm uninstall falco
```

### Sysdig
6. Lets Install Sysdig (Sign up for a free trial here): https://sysdig.com/company/free-trial/


