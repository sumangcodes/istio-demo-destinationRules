# istio-demo-destinationRules

Here's a concise `README.md` template for your GitHub repository, detailing the setup of microservices with Istio, including traffic control features such as granular routing, traffic splitting, and resilience testing.

```markdown
# Istio Microservices Traffic Management

This repository demonstrates how to set up microservices in Kubernetes with Istio for advanced traffic management, including granular traffic control, traffic shaping, fault injection, request routing, traffic mirroring, and Layer 7 routing. It includes two versions (`v1` and `v2`) of a microservice (`service-1`) to showcase Istio's traffic control capabilities.

## Prerequisites

- Kubernetes Cluster (e.g., Minikube, GKE, or any managed Kubernetes service)
- Istio (configured and installed on your cluster)
- kubectl CLI
- Docker

## Features

- **Granular Traffic Control**: Route traffic based on paths and hostnames.
- **Traffic Shaping and Splitting**: Split traffic between versions for A/B testing and canary deployments.
- **Fault Injection**: Simulate delays and errors to test resilience.
- **Request Routing and Rewrite Rules**: Custom routing rules and URL rewrites.
- **Traffic Mirroring**: Mirror traffic to test service versions without user impact.
- **Layer 7 Routing**: Route based on HTTP headers and URI paths.
- **Global Policy Management**: Centralized traffic management with Istio's VirtualService and DestinationRule.

## Directory Structure

```plaintext
.
├── service-1-v1-deployment.yaml       # Deployment for service-1 version v1
├── service-1-v2-deployment.yaml       # Deployment for service-1 version v2
├── service-1-v1-service.yaml          # Service for service-1 v1
├── service-1-v2-service.yaml          # Service for service-1 v2
├── service-1.yaml                     # Service to route traffic to all versions
├── service-1-gateway.yaml             # Istio Gateway to expose services to the outside
├── service-1-virtualservice.yaml      # Istio VirtualService for traffic routing rules
└── service-1-destinationrule.yaml     # Istio DestinationRule for version-specific policies
```

## Setup Instructions

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/istio-microservices-traffic-management.git
   cd istio-microservices-traffic-management
   ```

2. **Deploy Services and Deployments**:
   ```bash
   kubectl apply -f service-1-v1-service.yaml
   kubectl apply -f service-1-v2-service.yaml
   kubectl apply -f service-1.yaml
   kubectl apply -f service-1-v1-deployment.yaml
   kubectl apply -f service-1-v2-deployment.yaml
   ```

3. **Configure Istio Gateway and Routing**:
   ```bash
   kubectl apply -f service-1-gateway.yaml
   kubectl apply -f service-1-virtualservice.yaml
   kubectl apply -f service-1-destinationrule.yaml
   ```

4. **Verify Setup**:
   Retrieve the Istio Ingress Gateway IP:
   ```bash
   kubectl get svc istio-ingressgateway -n istio-system
   ```
   Access the service:
   ```bash
   curl http://<IngressGatewayIP>/hello
   ```

## Example Traffic Control Scenarios

1. **Path-based Routing**: Routes `/hello` to `service-1` (configurable in `VirtualService`).
2. **Traffic Splitting**: Split traffic between versions (`v1`, `v2`) in `DestinationRule`.
3. **Fault Injection**: Test resilience by injecting delays or errors (modify `VirtualService`).
4. **Traffic Mirroring**: Mirror requests to another version for testing purposes.

## Customization

- **Modify Routes**: Update `service-1-virtualservice.yaml` to add or change routing paths.
- **Adjust Traffic Split**: Edit `service-1-destinationrule.yaml` to control traffic distribution across versions.
- **Inject Faults**: Customize fault injection rules within `VirtualService` to simulate network issues.

## Clean Up

To remove all resources, run:
```bash
kubectl delete -f .
```
