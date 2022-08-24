# Scenario
# Certified Kubernetes Administrator Practice

Application "wonderful" is running in default Namespace.

You can call the app using curl wonderful:30080 .

The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .

Set the maxSurge to 50% and the maxUnavailable to 0% . Then perform a rolling update.

Wait till the rolling update has succeeded

Imperative commands:


Update the deployment container image from httpd:alpine to nginx:alpine

```yaml
    spec:
      containers:
      - image: nginx:alpine
```

The total amount of Pods of both Deployments combined should be 10:
```yaml
		k get deploy -o wide
        	NAME           READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
		wonderful-v1   2/2     2            2           11m   httpd        httpd:alpine   app=wonderful
		wonderful-v2   8/8     8            8           99s   nginx        nginx:alpine   app=wonderful
```

