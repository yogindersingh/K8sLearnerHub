# K8sLearnerHub

A hands-on learning repository for Kubernetes, built around a Spring Boot 3 application (Java 17) used as a sample workload.

## Project Structure

```
K8sLearnerHub/
├── src/main/resources/
│   ├── commands/
│   │   └── kubernetescommands.txt   # Kubectl command reference
│   └── examples/
│       └── nginxDeployment.yaml     # nginx Deployment + NodePort Service + HPA
├── src/main/java/com/learning/kubernetes/
│   └── KubernetesApplication.java   # Spring Boot entry point
└── pom.xml                          # Maven build (Spring Boot 3.2.2, Java 17)
```

## Sample App

The Spring Boot app (`spring-boot-starter-web`) serves as a lightweight container workload to practise deploying, scaling, and exposing services in a cluster.

**Build**
```bash
./mvnw clean package
```

## Kubernetes Command Reference

See [`src/main/resources/commands/kubernetescommands.txt`](src/main/resources/commands/kubernetescommands.txt) for a categorised list of kubectl commands covering:

| Category | Commands |
|---|---|
| Cluster info | `kubectl version`, `kubectl get nodes`, `kubectl get events` |
| Pods | `kubectl run`, `kubectl get pods`, `kubectl delete pod`, `kubectl logs` |
| Deployments | `kubectl create deployment`, `kubectl scale`, `kubectl delete deployment`, `kubectl describe` |
| Services | `kubectl expose` (ClusterIP / NodePort / LoadBalancer), `kubectl get service` |
| Namespaces | `kubectl get namespaces` |
| YAML / API | `kubectl api-resources`, `kubectl api-versions`, `kubectl explain`, `kubectl diff` |
| Dry-run | `--dry-run=client -o yaml` for Deployments, Jobs, Services |

## Example YAML

[`src/main/resources/examples/nginxDeployment.yaml`](src/main/resources/examples/nginxDeployment.yaml) demonstrates three resources in a single file:

- **Deployment** — runs nginx with 1 replica
- **Service (NodePort)** — exposes port 80 externally on node port 30000
- **HorizontalPodAutoscaler** — scales 1–5 replicas at 70% CPU utilisation

Apply it to a running cluster:
```bash
kubectl apply -f src/main/resources/examples/nginxDeployment.yaml
```

## Service Types

| Type | Scope |
|---|---|
| ClusterIP | Internal cluster traffic only (default) |
| NodePort | External access via a high port (30000–32767) |
| LoadBalancer | External access via a cloud load balancer |
| Ingress | HTTP/HTTPS routing with host/path rules |
