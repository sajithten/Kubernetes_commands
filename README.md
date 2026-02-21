# Kubernetes Quick Reference (Interview + Real Use)

---

# 1. PODS

## Use Case

* Smallest deployable unit
* Run single container (or tightly coupled containers)
* Debugging, testing, temporary workloads

## Commands

```
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash
kubectl delete pod <pod-name>
```

## YAML (Basic)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
```

---

# 2. DEPLOYMENTS

## Use Case

* Manage stateless apps
* Rolling updates, rollback
* Maintain desired state

## Commands

```
kubectl get deployments
kubectl describe deployment <name>
kubectl rollout status deployment <name>
kubectl rollout undo deployment <name>
kubectl scale deployment <name> --replicas=3
```

## YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
```

---

# 3. REPLICASET

## Use Case

* Ensure fixed number of pods
* Usually managed by Deployment

## Commands

```
kubectl get rs
kubectl describe rs <name>
```

---

# 4. HPA (Horizontal Pod Autoscaler)

## Use Case

* Auto scale pods based on CPU/Memory

## Commands

```
kubectl get hpa
kubectl autoscale deployment <name> --cpu-percent=50 --min=1 --max=5
```

## YAML

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-example
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deploy
  minReplicas: 1
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

---

# 5. VPA (Vertical Pod Autoscaler)

## Use Case

* Adjust CPU/memory requests automatically

## Commands

```
kubectl get vpa
```

## Note

* Requires VPA controller installation
* Not used with HPA in most production setups

---

# 6. SERVICES

## Types + Use Case

* ClusterIP → Internal communication
* NodePort → Expose via node IP
* LoadBalancer → External access (cloud)
* Headless → Direct pod access

## Commands

```
kubectl get svc
kubectl describe svc <name>
```

## YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP
```

---

# 7. INGRESS

## Use Case

* HTTP/HTTPS routing
* Path-based routing
* Single entry point

## Commands

```
kubectl get ingress
kubectl describe ingress <name>
```

---

# 8. CONFIGMAP

## Use Case

* Store non-sensitive config

## Commands

```
kubectl get configmap
kubectl create configmap my-config --from-literal=key=value
```

---

# 9. SECRETS

## Use Case

* Store sensitive data (passwords, tokens)

## Commands

```
kubectl get secrets
kubectl create secret generic my-secret --from-literal=password=1234
```

---

# 10. PV (Persistent Volume)

## Use Case

* Cluster-level storage

## Commands

```
kubectl get pv
```

---

# 11. PVC (Persistent Volume Claim)

## Use Case

* Request storage from PV

## Commands

```
kubectl get pvc
```

## YAML

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-demo
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

# 12. NAMESPACE

## Use Case

* Logical separation (dev, qa, prod)

## Commands

```
kubectl get ns
kubectl create ns dev
kubectl config set-context --current --namespace=dev
```

---

# 13. DAEMONSET

## Use Case

* Run one pod per node
* Monitoring agents (Prometheus, Fluentd)

## Commands

```
kubectl get daemonset
```

---

# 14. STATEFULSET

## Use Case

* Stateful apps (DB, Kafka)
* Stable identity + storage

## Commands

```
kubectl get statefulset
```

---

# 15. JOB / CRONJOB

## Use Case

* Job → One-time execution
* CronJob → Scheduled jobs

## Commands

```
kubectl get jobs
kubectl get cronjobs
```

---

# TROUBLESHOOTING COMMANDS (CRITICAL)

## Pod Issues

```
kubectl describe pod <pod>
kubectl logs <pod>
kubectl logs <pod> -c <container>
kubectl get events
```

## Debugging

```
kubectl exec -it <pod> -- /bin/sh
kubectl top pod
kubectl top node
```

## Networking Issues

```
kubectl get svc
kubectl get endpoints
kubectl port-forward pod/<pod> 8080:80
```

## Deployment Issues

```
kubectl rollout status deployment <name>
kubectl rollout history deployment <name>
```

## Node Issues

```
kubectl get nodes
kubectl describe node <node>
```

## Force Delete

```
kubectl delete pod <pod> --force --grace-period=0
```

---

# HIGH-VALUE INTERVIEW INSIGHT

* Pod crash → check logs + events
* Service not working → check endpoints
* Deployment not updating → check rollout
* HPA not scaling → metrics-server issue
* PVC pending → storage class / PV issue

---

# MENTAL MODEL

* Pod = runtime
* Deployment = controller
* Service = networking
* PVC = storage
* HPA = scaling
* Ingress = external routing

---





## 30 Kubernetes commands you must know: 

1. `kubectl get pods`: lists all the running pods in the current namespace.

2. `kubectl create deployment <deployment-name> --image=<image-name>`: creates a new deployment with the specified name and image.

3. `kubectl expose deployment <deployment-name> --port=<port-number>`: creates a new service for the specified deployment and exposes it on the specified port.

4. `kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>`: scales the specified deployment to the specified number of replicas.

5. `kubectl delete deployment <deployment-name>`: deletes the specified deployment.

6. `kubectl apply -f <filename>`: applies the configuration file specified by the filename.

7. `kubectl logs <pod-name>`: shows the logs for the specified pod.

8. `kubectl exec -it <pod-name> -- /bin/bash`: opens a shell in the specified pod.

9. `kubectl port-forward <pod-name> <local-port>:<remote-port>`: forwards traffic from the specified local port to the specified remote port on the specified pod.

10. `kubectl describe <resource-type> <resource-name>`: provides detailed information about the specified resource.

11. `kubectl get nodes`: lists all the nodes in the cluster.

12. `kubectl get services`: lists all the services in the current namespace.

13. `kubectl get deployments`: lists all the deployments in the current namespace.

14. `kubectl get configmaps`: lists all the configmaps in the current namespace.

15. `kubectl get secrets`: lists all the secrets in the current namespace.

16. `kubectl apply -f <directory>`: applies the configuration files in the specified directory.

17. `kubectl rollout status deployment <deployment-name>`: shows the status of the specified deployment rollout.

18. `kubectl rollout history deployment <deployment-name>`: shows the revision history of the specified deployment.

19. `kubectl edit <resource-type> <resource-name>`: opens the specified resource in the default editor.

20. `kubectl top <resource-type>`: shows the resource usage statistics for the specified resource type.

21. `kubectl create namespace <namespace-name>`: creates a new namespace with the specified name.

22. `kubectl get namespaces`: lists all the namespaces in the cluster.

23. `kubectl config get-contexts`: lists all the contexts in the Kubernetes configuration file.

24. `kubectl config set-context <context-name> --namespace=<namespace-name>`: sets the namespace for the specified context.

25. `kubectl apply -f <url>`: applies the configuration file at the specified URL.

26. `kubectl rollout undo deployment <deployment-name>`: undoes the last rollout of the specified deployment.

27. `kubectl delete pod <pod-name>`: deletes the specified pod.

28. `kubectl delete service <service-name>`: deletes the specified service.

29. `kubectl delete namespace <namespace-name>`: deletes the specified namespace.

30. ‘kubectl config use-context’
