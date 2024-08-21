# Star Wars API Helm Charts

This repository houses the Helm chart configurations for deploying the assorted Star Wars API wrappers (Python, Go, and Node.js) to a Kubernetes cluster.

## Prerequisites

- Kubernetes Cluster
    - Running version of K3s (as this has only beentested on a k3s cluster henceh the nodePort bits)
- Helm installed and configured

### Review the Repositories for the Various Containers in Use

| Container | Repository Link |
|-----------|-----------------|
| Python    | [Python Container](https://github.com/bmorri13/python_multistage_starwars_api_wrapper) |
| Go        | [Go Container](https://github.com/bmorri13/go_multistage_starwars_api_wrapper) |
| Node      | [Node Container](https://github.com/bmorri13/node_multistage_starwars_api_wrapper) |

> ⚠️ **Note:** As of the latest update, these images are based on the (Chainguard base images)[https://edu.chainguard.dev/chainguard/chainguard-images/] and deployed to (DockerHub Container Registry)[https://hub.docker.com/repositories/bmo75]




### File Structure
```bash
starwars_api_helm_charts/
├── go_starwars_api_helm/
│ ├── Chart.yaml
│ ├── values.yaml
│ └── templates/
│   ├── namespace.yaml
│   ├── deployment.yaml
│   └── service.yaml
├── node_starwars_api_helm/
│ ├── Chart.yaml
│ ├── values.yaml
│ └── templates/
│   ├── namespace.yaml
│   ├── deployment.yaml
│   └── service.yaml
├── python_starwars_api_helm/
│ ├── Chart.yaml
│ ├── values.yaml
│ └── templates/
│   ├── namespace.yaml
│   ├── deployment.yaml
│   └── service.yaml
```


## Usage

### Installing the Charts

To deploy the API wrappers using Helm, run the following commands:

```bash
helm install python-starwars-api ./python_starwars_api_helm --create-namespace
helm install go-starwars-api ./go_starwars_api_helm --create-namespace
helm install node-starwars-api ./node_starwars_api_helm --create-namespace
```

- These commands will create the required namespaces and deploy the API wrappers in their respective namespaces (python-starwars-api, go-starwars-api, and node-starwars-api).

### Monitoring the Deployments
- You can monitor the deployment status of each API wrapper by watching the pods:

```bash
kubectl get pods -n python-starwars-api --watch
kubectl get pods -n go-starwars-api --watch
kubectl get pods -n node-starwars-api --watch
```

### Listing the Installed Helm Releases
- To see a list of all the Helm releases currently installed:

```bash
helm list
```

### Upgrading the Charts
- If you need to upgrade the API wrappers after making changes to the Helm charts or the Docker images:

```bash
helm upgrade python-starwars-api ./python_starwars_api_helm
helm upgrade go-starwars-api ./go_starwars_api_helm
helm upgrade node-starwars-api ./node_starwars_api_helm
```


### Uninstalling the Charts
- To uninstall the API wrappers and clean up the resources, use the following commands:

```bash
helm uninstall python-starwars-api
helm uninstall go-starwars-api
helm uninstall node-starwars-api
```

- These commands will remove the deployed resources from the Kubernetes cluster but will leave the namespaces intact.
