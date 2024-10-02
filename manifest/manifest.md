# Manifest files setup

*follow this guide in sequence*

To make deployment setup cleaner, deployments are contained inside a namespace

`dotnetapinamespace.yaml`

This line specifies the name of our namespace
```
metadata:
  name: dotnet
```

To create one inside the cluster run

```
kubernetes apply -f dotnetapinamespace.yaml
```

To setup deployments, a pods to where our dockerfile will be running is found inside

`dotnetapi.yaml`

The following lines are essential to configure, this sets up how many replicas of our deployment will be made and where to get the docker image.

```
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web-api-deployment
  template:
    metadata:
      labels:
        app: web-api-deployment
      namespace: dotnet
    spec:
      containers:
      - name: web-api-deployment
        image: dekkusu/devops-things:caplinq
        imagePullPolicy: Always
        ports:
        - containerPort: 80
```

In this case, 2 replicas are set (important to have more than 1 to make sure downtime is reduced in case of sudden errors or updates).

As for the dockerfile, it is pointing to the docker repository where the github action pushes the docker image created.

To deploy deployments run

```
kubernetes apply -f dotnetapi.yaml
```


For the services, this where the networking is configured (becomes more important when DB is added to not mess up the whole deployment)

`dotnetapiservice.yaml`

To deploy services run

```
kubernetes apply -f dotnetapiservice.yaml
```
