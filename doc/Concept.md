# AsciiArtify Kubernetes Deployment Tools Evaluation

## Introduction
Startup AsciiArtify wants to select the right tool for local Kubernetes cluster development. Three options are considered: minikube, kind and k3d.

## Characteristics
### Minikube
- `Supported OS and Architectures:` Multiple operating systems including Windows, macOS, and Linux. Various architectures.  
- `Automation Capability:` Automation for cluster creation and management.

### Kind (Kubernetes IN Docker)
- `Supported OS and Architectures:` Multiple operating systems including Windows, macOS, and Linux. Various architectures.  
- `Automation Capability:` Creation of local Kubernetes clusters in Docker containers.  

### k3d
- `Supported OS and Architectures:` Multiple operating systems including Windows, macOS, and Linux. Various architectures.
- `Automation Capability:` Creation and testing of Kubernetes clusters in Docker containers.

### Characteristic

| **Pros and Cons**                               | **Minikube**                                     | **Kind**                                         | **k3d**                                          | **Podman**                                       |
|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|--------------------------------------------------|
| **Pros**                                      | + Easy to use<br>+ Suitable for local development and testing | + Suitable for local development and testing<br>+ Works within Docker containers<br>+ Possibility for local testing | + Suitable for local development and testing<br>+ Works within Docker containers<br>+ Fast cluster creation and testing | + Easy to use<br>+ Suitable for local development and testing<br>+ Works within Docker containers<br>+ Light alternative to Docker |
| **Cons**                                      | - Scalability<br>- Potential limitations | - Limited information on scalability<br>- Limited documentation | - Limited documentation<br>- Scalability | - Limited information on scalability<br>- Limited documentation |

## Conclusion
k3d stands out as the recommended tool for AsciiArtify's PoC. Quick cluster creation and simplicity makes it suitable for initial development. However, it's downside is limited community documentation and potential scalability concerns. Additionally, Podman is introduced as a lightweight alternative to Docker, offering rootless containers and direct integration with systemd.