# Scenario
# Certified Kubernetes Administrator Practice

Application "wonderful" is running in default Namespace.

You can call the app using curl wonderful:30080 .

The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .

Set the maxSurge to 50% and the maxUnavailable to 0% . Then perform a rolling update.

Wait till the rolling update has succeeded

Imperative commands:

```yaml
  alias kubectl="k"
  k edit deploy wonderful-v1
```

Update the deployment container image from httpd:alpine to nginx:alpine

```yaml
    spec:
      containers:
      - image: nginx:alpine
```

Update the deployment and add the following snippet for updating the rollout strategy:
```yaml
  strategy:
    rollingUpdate:
      maxSurge: 50%
      maxUnavailable: 0%
    type: RollingUpdate
```


