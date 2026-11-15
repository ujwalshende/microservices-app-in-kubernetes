# Deployment of Microservices Application in K8S with Best Practices
This project contains a `config.yaml` file that can be used to deploy a microservices app on a kubernetes cluster.

## Steps to deploy
1. Create a cluster on a platform like Linode.
2. Download the kubeconfig file and place it in the default location or set the KUBECONFIG environment variable to point to the location of this file
3. Create a separate namespace using `kubectl create namespace microservices` command.
4. Deploy the app to this namepace using `kubectl apply -f config.yaml -n microservices`


## Best practices used in this project

1. Pin the version of the docker images to avoid suprises when the latest tag gets updated.
2. Define liveness probe to let kubernetes know whether the app is running or it has crashed.
3. Define readiness probe to let kubernetes know that the application has started and is ready to receive traffic.
4. Define resource requests for cpu and memory.
5. Define resource limits for cpu and memory so that usage remains bounded and we don't end up using more than what we can afford.
6. Use service with type LoadBalancer instead of NodePort for external services. Exposing a node port is a bad practice. By using nodePort we expose ports on all worker nodes, which increases the attack surface and makes the cluster vulnerable.
7. Use multiple replicas to reduce service down-time. It also reduces load per pod in case of a user surge.
8. Use more than worker node to avoid having a single point of failure.
9. Using labels for the kubernetes components to reference them better.
10. Namespaces are very helpful to manage components. Its always better to split components into namespaces. It is also usefil for permission management.

## Additional best practices
1. Ensuring that applications/images are free of vulnerabilities
2. Configure containers to use non root users. If someone hacks into a container, they gain access to everything on the node. This causes a big security issue. Should be considerd especially while using third party images.
3. Update kubernetes cluster to use the latest kubernetes version. 
