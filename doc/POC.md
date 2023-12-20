# AsciiArtify. Proof of Concept

> We will prepare and deploy the ArgoCD GitOps system on Kubernetes.

1. Let's create a cluster (for demonstration purposes, a single node of the cluster will be enough)

   ```bash
   k3d cluster create argo
   ```
2. Let's create a separate namespace for the needs of ArgoCD

   ```bash
   kubectl create namespace argocd
   ```
3. For convenience, let's set the current context - `argocd`

   ```bash
   kubectl config set-context --current --namespace=argocd
   ```
4. We will apply the installation YAML-manifest file within the `argocd` namespace to install ArgoCD

   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
   ```
5. Let's check the state of the newly created pods in the `argocd` namespace with real-time information updates. In this case, the containers for `argocd` are distributed on separate pods.

   ```bash
   kubectl get po -n argocd -w
   ```
   As a result, about eight pods/containers will be displayed.
6. Let's get access to the ArgoCD interface.

   Typical options:

   - Using a service with a Load Balancer type
   - Port Forwarding

   Let's use Port Forwarding

   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443&
   ```
   For the svc/argocd-server service from the agrocd namespace, we will configure background forwarding from local port 8080 to remote port 443 in the container running the ArgoCD web server.
7. Get the password

   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"|base64 -d;echo
   ```
   The command receives the secret file, decodes the password and outputs it to the terminal.
8. Enter the received password and `admin` login into the ArgoCD Web interface at the address `127.0.0.1:8080`. Agree to use a self-signed certificate.
