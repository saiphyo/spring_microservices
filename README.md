# Microservices with Spring Boot 3 and Spring Cloud - Implementation Project

This repository contains the implementation of a microservices landscape. It serves as a practical guide and reference for building resilient and scalable microservices using the latest Spring technologies and cloud-native tools.

## Tech Stack

This project leverages a comprehensive set of technologies, frameworks, and tools:

### Core Microservices Development

*   **Spring Boot 3**: The foundation for building production-ready, stand-alone, Spring-powered applications with minimal configuration.
*   **Spring Framework 6**: The underlying framework providing comprehensive infrastructure support for developing Java applications.
*   **Spring WebFlux**: Used for developing reactive, non-blocking RESTful APIs.
*   **Spring Data**: Provides a consistent programming model for accessing various types of databases, including SQL and NoSQL.
    *   Support for **MongoDB** using reactive non-blocking drivers.
    *   Support for **MySQL** using conventional blocking code.
*   **Spring Cloud Stream**: Facilitates building message-driven microservices ( `RabbitMQ` or `Kafka` ).
*   **springdoc-openapi**: For generating **OpenAPI**-based API documentation at runtime, enabling API exploration with **Swagger UI**.
*   **Resilience4j**: Implemented for improving the resilience of the microservices through mechanisms like **circuit breakers, time limiters, and retry mechanisms**.

### Containerization and Orchestration

*   **Docker**: Used for packaging and running microservices as lightweight containers.
*   **Kubernetes**: A powerful container orchestrator for managing a cluster of servers running the microservices. (via `minikube`)
*   **Helm**: A package manager for Kubernetes, used for packaging and configuring microservices for deployment in different environments.

### Service Mesh

*   **Istio**: Implemented as a service mesh to enhance resilience, security, traffic management, and observability within the microservice landscape on Kubernetes.

### Service Discovery

*   Initially using **Netflix Eureka** for service discovery in Spring Cloud.
*   Transitioning to **Kubernetes Service objects** and **kube-proxy** for built-in service discovery within Kubernetes.

### API Gateway

*   **Spring Cloud Gateway**: Used as an edge server to route external traffic to the appropriate microservices.
*   Utilizing **Kubernetes Ingress** as an alternative for managing external access in a Kubernetes environment.

### Configuration Management

*   **Spring Cloud Config Server**: Introduced for centralized management of microservices configurations.
*   Leveraging **Kubernetes ConfigMaps** and **Secrets** for managing configuration within Kubernetes.

### Observability

*   **EFK Stack**: Used for centralized logging with **Elasticsearch**, **Fluentd**, and **Kibana** for collecting, storing, and visualizing log streams.
*   **Micrometer Tracing** with **Zipkin**: Implemented for distributed tracing across microservices.
*   Integration with **Istio's Jaeger** component as an alternative for distributed tracing in a service mesh environment.
*   **Prometheus** and **Grafana**: Used for performance monitoring and setting up alarms based on collected metrics.
*   **Kiali**: Provides observability into the Istio service mesh, visualizing its topology and traffic.

### Security

*   **OAuth 2.0** and **OpenID Connect**: Implemented for securing access to APIs.
*   Using a local **Authorization Server** based on Spring Authorization Server.
*   Demonstrating integration with an external **OpenID Connect provider (Auth0)**.
*   Securing external communication with **HTTPS**.
*   Utilizing **cert-manager** in Kubernetes for automated certificate provisioning.

### Build Tool

*   **Gradle**: Used as the build automation tool for managing project dependencies and building the microservices.

### Testing

*   Manual testing using **Swagger UI**.
*   Automated tests using bash scripts and tools like `curl` and `jq`.
*   **Siege** used for load testing.

This comprehensive tech stack demonstrates the practical application of modern microservices architecture principles and the powerful capabilities of the Spring ecosystem and cloud-native tools.

## Getting Started

To get started with this project, you will need to have the necessary tools installed as described in **set up your development environment**.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/saiphyo/spring_microservices.git
    cd spring_microservices
    ```
2.  Follow the instructions to set up your development environment.
    
## Installation Guide: Microsoft Windows with WSL 2 and Ubuntu

This guide helps you set up a development environment to run all examples and commands in a bash shell on a Linux server within WSL 2, with minimal adjustments.

## Technical Requirements

To use WSL 2, your Windows PC must be running **Windows 10, version 2004 (build 19041) or later**. This guide uses **Ubuntu 24.04** as the Linux distribution within WSL 2.

## Tools Covered

This guide will cover the installation and configuration of the following tools:

**On Windows:**
*   **Windows Subsystem for Linux v2 (WSL 2)**
*   **Ubuntu 24.04 in WSL 2**
*   **Windows Terminal**
*   **Docker Desktop for Windows**
*   **Visual Studio Code and its extension for Remote WSL**

**On the Linux server in WSL 2:**
*   **Git** (pre-installed)
*   **Java**
*   **curl** (pre-installed)
*   **jq**
*   **Spring Boot CLI**
*   **Siege**
*   **Helm**
*   **kubectl**
*   **minikube**
*   **istioctl**

**Specific versions used**
*   Git: 2.43.0
*   Docker Desktop for Windows: 28.0.4
*   Java (Openjdk): 17.0.13
*   curl: 8.5.0
*   jq: 1.7
*   Spring Boot CLI: v3.0.4
*   Siege: 4.0.7
*   Helm: v3.17.3
*   kubectl: v1.26.1
*   minikube: v1.29.0
*   istioctl: 1.17.0

## Installation Steps

### Installing tools on Windows

1.  **Install WSL 2 with a default Ubuntu server:** 
    * Open PowerShell as an administrator and run `wsl --install`. 
    * Restart your PC to complete. 
    * When prompted in the new Terminal window, enter a username and password for the Ubuntu server. 
    * Verify the Ubuntu version with `lsb_release -d`.
2.  **Install Windows Terminal:** 
    * Install from the Microsoft Store. It will be pre-configured to start a terminal in the Linux   
      server (e.g., Ubuntu-22.04).
3.  **Install Docker Desktop for Windows:**
    * Download and install Docker Desktop
    * Ensure the `Use the WSL 2 based engine` checkbox is selected during or after installation in Settings.
4.  **Install Visual Studio Code and its extension for Remote WSL:** 
    * Download and install VS Code. 
    * Select the `Add to PATH` option during installation. 
    * After launching VS Code, install the `Remote WSL` extension.

### Installing tools on the Linux server in WSL 2

Launch Windows Terminal and open a session for your Ubuntu server. Git and curl are typically pre-installed on Ubuntu.

1.  **Install tools using `apt install`:** 
    * To install jq, zip, unzip, and siege with the following commands:
        ```bash
        sudo apt update
        sudo apt install -y jq
        sudo apt install -y zip
        sudo apt install -y unzip
        sudo apt install -y siege
        ```

    * To install Helm, run the following commands:
        ```bash
        curl -s https://baltocdn.com/helm/signing.asc | \
        gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
        sudo apt-get install apt-transport-https --yes
        echo "deb [arch=$(dpkg --print-architecture) \
        signed-by=/usr/share/keyrings/helm.gpg] \
        https://baltocdn.com/helm/stable/debian/ all main" | \
        sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
        sudo apt-get update
        sudo apt install -y helm
        ```
2.  **Install Java and Spring Boot CLI using SDKman:** 
    * First, install SDKman (https://sdkman.io). 
    * Install SDKman with the following commands:
        ```bash
        curl -s "https://get.sdkman.io" | bash
        source "$HOME/.sdkman/bin/sdkman-init.sh"
        ```
    * To install Java
        ```bash
        sdk install java 17.0.6-tem
        ```
    *  To install the Spring Boot CLI.
        ```bash
        sdk install springboot 3.0.4
        ```
3.  **Install kubectl, minikube, and istioctl using curl and install:** 
    * To install the kubectl, run the following commands:
        ```bash
        curl -LO "https://dl.k8s.io/release/v1.26.1/bin/linux/amd64/kubectl"
        sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
        rm kubectl
        ```
    * To install the minikube, run the following commands:
        ```bash
        curl -LO https://storage.googleapis.com/minikube/releases/v1.29.0/minikubelinux-amd64
        sudo install -o root -g root -m 0755 minikube-linux-amd64/usr/local/bin/minikube
        rm minikube-linux-amd64
        ```
    * To install the istioctl, run the following commands:
        ```bash
        curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.17.0 TARGET_ARCH=x86_64 sh -
        sudo install -o root -g root -m 0755 istio-1.17.0/bin/istioctl /usr/local/bin/istioctl
        rm -r istio-1.17.0
        ```

## Post-Installation Configuration

*   **Configure Docker Desktop:** 
    * In Docker Settings -> General, **ensure 'Use the WSL 2 based engine' is checked** 
    * In Settings -> Resources, **allocate sufficient memory** (e.g., 10 GB, 6 GB may work initially) and CPU cores to the WSL 2 engine. 
    * Click 'Apply & Restart'.

## Verifying Installation

Run the following commands in your bash shell within the Linux server in WSL 2 to verify the installed versions:

```bash
git version && \
docker version -f json | jq -r .Client.Version && \
java -version 2>&1 | grep "openjdk version" && \
curl --version | grep "curl" | sed 's/(.*//' && \
jq --version && \
spring --version && \
siege --version 2>&1 | grep SIEGE && \
helm version --short && \
kubectl version --client -o json | \
jq -r .clientVersion.gitVersion && \
minikube version | grep "minikube" && \
istioctl version --remote=false
```
Expect output similar to the versions listed above.

## Running the Application (Building and deploying the microservices)

1.  Build the Docker images from the source with the following commands:
    ```bash
    minikube start
    cd ~/spring_microservices
    eval $(minikube docker-env -u)
    ./gradle build
    eval $(minikube docker-env)
    docker-compose build
    ```
2.  Create the namespace, hands-on, and set it as the default namespace:
    ```bash
    kubectl apply -f kubernetes/hands-on-namespace.yml
    kubectl config set-context $(kubectl config current-context) --namespace=hands-on
    ```
3.  Resolve the Helm chart dependencies with the following commands:
    * First, update the dependencies in the components folder:
        ```bash
        for f in kubernetes/helm/components/*; do helm dep up $f; done
        ```
    * Next, update the dependencies in the environments folder:
        ```bash
        for f in kubernetes/helm/environments/*; do helm dep up $f; done
        ```
4.  Deploy the system landscape using Helm and wait for all deployments to complete:
    ```bash
    helm install hands-on-dev-env kubernetes/helm/environments/dev-env -n hands-on --wait
    ```
5.  Start the Minikube tunnel
    ```bash
    minikube tunnel
    ```
6.  Run the tests to verity the deployment with the following command:
    ```bash
    ./test-em-all.bash
    ```
