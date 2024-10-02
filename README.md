
# Task 1: Kubernetes Deployment

DevOps Engineer Assessment from Caplinq

## Guide for configuration

### Configure dotnet on local/Ubuntu server
```
sudo apt-get update
sudo apt-get install -y dotnet-sdk-8.0
sudo apt-get install -y aspnetcore-runtime-8.0
sudo apt-get install -y dotnet-runtime-8.0
```

To run dotnet test

*make sure to run this inside the directory where .sln file is located*

```
dotnet test Caplinq.DevOps.sln
```

For Building

```
dotnet build
```

### K8s Deployment Setup/Naming

Namespace: dotnet

Deployment:  dotnet-web-deployment

Service: dotnet-web-service (with Load Balancer)

### How to Access Kubernetes Cluster
Get deployments

```
kubectl get pods -n dotnet
```

Access deployments

```
kubectl exec -it -n dotnet <deployment_name> -- bash
```

View services

```
kubectl get services -n dotnet
```


## Deployment

PR to main branch github actions will automatically run

See .github/workflows/main.yml to view CI/CD Pipeline