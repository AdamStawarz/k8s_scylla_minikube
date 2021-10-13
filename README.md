# Automating Scylla deployments with Kubernetes

This example demonstrates a simple example of deploying a Scylla cluster on Minicube


## Demo

- Install minikube/kubectl

- First, create the `Service` aggegating Scylla `Pods`:
  ```bash
  $ kubectl create -f scylla-service.yaml
  ```
  
- Create the `ConfigMap`, for the readiness-checking file:
  ```bash
  $ kubectl create -f scylla-configmap.yaml
  ```
  
- Finally, we're ready to instantiate our Scylla cluster with three nodes:
  ```bash
  $ kubectl create -f scylla-statefulset.yaml
  ```
  
We can query the resources we've created with commands like `kubectl get statefulsets` or `kubectl describe storageclass scylla`.

To query the state of the `Pods`, execute `kubectl get pods`. Once all `Pods` are ready, we can use `nodetool` to observe the state of the Scylla cluster:

```bash
$ kubectl exec scylla-0 -- nodetool status
```


Finally, we can increase the size of our cluster:

```bash
$ kubectl edit statefulset scylla
```

# References

- [Scalable multi-node Cassandra deployment on Kubernetes Cluster](https://github.com/IBM/Scalable-Cassandra-deployment-on-Kubernetes/blob/master/README.md)
- [Google Cloud Platform Quickstart for Linux](https://cloud.google.com/sdk/docs/quickstart-linux)
- [Running Kubernetes on Google Compute Engine](https://kubernetes.io/docs/getting-started-guides/gce/)
- [Example: Deploying Cassandra with Stateful Sets](https://kubernetes.io/docs/tutorials/stateful-application/cassandra/)
- [Strategies for Running Stateful Workloads in Kubernetes](https://thenewstack.io/strategies-running-stateful-applications-kubernetes-pet-sets/)
