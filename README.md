
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
