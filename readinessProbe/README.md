# Scenario 1
## Certified Kubernetes Administrator Practice 

Create a Deployment named space-alien-welcome-message-generator of image httpd:alpine with one replica.

It should've a ReadinessProbe which executes the command stat /tmp/ready . This means once the file exists the Pod should be ready.
The initialDelaySeconds should be 10 and periodSeconds should be 5 .

Create the Deployment and observe that the Pod won't get ready.

## Imperative commands:

```yaml
  alias kubectl="k"
  k create deployment space-alien-welcome-message-generator --image=httpd:alpine --replicas=1 --dry-run=client -o YAML > deployment.yml
```

Update the YAML and add the following snippet for readinessProbe under 'container spec' and not deployment spec.
```yaml
        readinessProbe:
         exec:
          command:
          - stat 
          - /tmp/ready
         initialDelaySeconds: 10
         periodSeconds: 5
```

Once updated create your deployment 
```yaml
  k create -f deployment.yml
  k get deploy (To check the deployment is 'not ready' as per scenario instructions)
```

# Scenario 2

Make the Deployment ready.
Exec into the Pod and create file /tmp/ready .
Observe that the Pod is ready.

## Imperative commands:

```yaml
   k get pods (grab the name of the pod to use in 2nd command)
   k exec pods <pod name> -- touch /tmp/ready
   k get deploy (Deployment should be ready after creating the file)
```
