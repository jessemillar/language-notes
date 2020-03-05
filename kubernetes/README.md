# Kubernetes

## ` kubectl`

### [apply vs create](https://stackoverflow.com/questions/47369351/kubectl-apply-vs-kubectl-create)

`kubectl create` is what we call Imperative Management. On this approach you tell the Kubernetes API what you want to create, replace or delete, not how you want your K8s cluster world to look like.

`kubectl apply` is part of the Declarative Management approach, where changes that you may have applied to a live object (i.e. through scale) are maintained even if you apply other changes to the object.
