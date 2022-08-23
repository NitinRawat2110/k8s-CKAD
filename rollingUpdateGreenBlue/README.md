# Scenario
# Certified Kubernetes Administrator Practice

Application "wonderful" is running in default Namespace.

You can call the app using curl wonderful:30080 .

The application YAML is available at /wonderful/init.yaml .

The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .

The switch should happen instantly. Meaning that from the moment of rollout, all new requests should hit the new image.

Create a new Deployment wonderful-v2 which uses image nginx:alpine with 4 replicas. It's Pods should have labels app: wonderful and version: v2

Once all new Pods are running, change the selector label of Service wonderful to version: v2

Finally scale down Deployment wonderful-v1 to 0 replicas

# Imperative commands:

Update the deployment container image from [httpd:alpine](httpd:alpine) to [nginx:alpine](nginx:alpine) with 4 replicas and labels app: wonderful and version: v2

  Check the [wonderful-v2](wonderful-v2) YAML [here](https://github.com/NitinRawat2110/k8s-CKAD/blob/main/rollingUpdateGreenBlue/wonderful-v2.yml)
  
  Create the wonderful-v2 deployment 
```yaml
  k create -f wonderful-v2.yml
```

Change the selector label of Service wonderful to version: v2. Check the [service](service) YAML [here](https://github.com/NitinRawat2110/k8s-CKAD/blob/main/rollingUpdateGreenBlue/wonderful-v1.yml)

```yaml
  k edit svc wonderful
```
  
Finally scale down Deployment wonderful-v1 to 0 replicas

```yaml
  k scale deployment/wonderful-v1 --current-replicas=4 --replicas=0
  
  OR
  
  k scale deploy wonderful-v1 --replicas 0
```
