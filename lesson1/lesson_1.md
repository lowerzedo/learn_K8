# Lesson 1: Kubernetes Fundamentals Summary

This lesson covered the deployment of a basic web application using fundamental Kubernetes resources.

### Core Concepts Learned:

1.  **Kubernetes Resources:** We worked with three key resources defined in YAML files:

    - **`Deployment`**: The blueprint for our application. Its primary job is to manage a set of replica **Pods** and ensure the desired number are always running and healthy. It uses a pod `template` to create new pods.
    - **`Pod`**: The smallest deployable unit in Kubernetes. It's an isolated environment that runs our application container (in this case, NGINX). Pods are _ephemeral_—they can be destroyed and recreated at any time, receiving a new IP address.
    - **`Service`**: The resource that provides a stable network endpoint (a consistent IP address and DNS name) for our ephemeral pods. It makes our application accessible to other applications and external users.

2.  **The Selector-Label Mechanism:** This is the glue that connects resources.

    - The `Deployment` knows which pods to manage because its `spec.selector` matches the `metadata.labels` on the pods created from its `template`.
    - The `Service` knows which pods to send traffic to because its `spec.selector` matches the same labels on the pods.

3.  **Networking and Ports:** We learned how traffic gets to our application.

    - **`containerPort`**: The port the application is listening on inside the container (e.g., NGINX on port 80).
    - **`targetPort`**: The port on the pod that the `Service` forwards traffic to. It must match the `containerPort`.
    - **`port`**: The port that the `Service` itself exposes on the internal cluster network.
    - **`NodePort`**: A type of `Service` that exposes the application on a high-numbered port on the physical Node's IP, making it accessible from outside the cluster.

4.  **Local Development Workflow:** We used `minikube` and `kubectl` to deploy and interact with our application.
    - **`minikube start`**: To create a local Kubernetes cluster.
    - **`kubectl apply -f <filename>`**: To create or update resources from a YAML file.
    - **`kubectl get pods/service`**: To inspect the status of our resources.
    - **`minikube service <service-name>`**: To create a convenient, reliable tunnel for accessing a `Service` from our local machine.
    - **`kubectl logs` & `kubectl exec`**: For debugging by viewing logs or getting a shell inside a running pod.

---

### Final State:

- `nginx_deployment.yaml`: Defines a Deployment to run 2 replicas of NGINX.
- `nginx-service.yaml`: Defines a `NodePort` Service to expose the NGINX pods.
- The application is running on Minikube and is accessible via the `minikube service` command.
