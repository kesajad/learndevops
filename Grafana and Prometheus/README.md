# Grafana and Prometheus with HELM
## What is HELM?
- Helm is a package manager for Kubernetes, an open-source container orchestration platform. Helm helps you manage Kubernetes applications by providing a way to define, install, and upgrade even the most complex Kubernetes applications.
  Here are some key aspects of Helm:
- Charts: Helm uses a packaging format called "charts." A Helm chart is a collection of files that describe a related set of Kubernetes resources. This includes YAML configuration files, templates, and other dependencies that are needed to run an application or service.
- Release Management: Helm allows you to manage the lifecycle of Kubernetes applications. You can install, upgrade, and rollback releases of applications using Helm commands. Each installation of a chart is referred to as a release.
- Templates: Helm charts support templating, which means you can create flexible and reusable configurations. Templates in Helm use the Go templating language to dynamically generate YAML files based on input values.
- Repositories: Helm charts can be stored in repositories, making it easy to distribute and share charts. Public and private Helm repositories can be used to manage collections of charts.
- Dependencies: Helm allows you to specify dependencies between charts. This means you can create a chart that depends on other charts, and Helm will handle fetching and installing those dependencies for you.
- Configuration Management: Helm simplifies the process of configuring applications by allowing you to pass in custom values during installation. These values override the default configuration provided by the chart.
- Community and Ecosystem: Helm has a large and active community that maintains a wide variety of charts for popular applications. This makes it easier to find and deploy applications in Kubernetes.

Overall, Helm enhances the Kubernetes experience by simplifying the deployment and management of applications, making it easier to adopt Kubernetes for complex workloads.

## Steps by Step Configurations
### 1. Provision an Ubuntu VM
### 2. Create an AKS Cluster
### 3. Install kubectl with bash file
   ```
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    kubectl version --client
   ```
   Run the following commands
   ```
     chmod +x kubectl.sh
     bash kubectl.sh
   ```
### 4. Install Azure CLI
https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt
### 5. Install HELM with bash file
   ```
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
  chmod 700 get_helm.sh
  ./get_helm.sh
  helm version --client
   ```
### 6. Prometheus and grafana implementation
Need to add the Helm Stable Charts in local
   ```
helm repo add stable https://charts.helm.sh/stable
   ```
### 7. Add prometheus Helm repo
   ```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm search repo prometheus-community
   ```
### 8. Create Prometheus namespace
   ```
kubectl create namespace prometheus
   ```
### 9. Install Prometheus Stack
   ```
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
   ```
### 10. Lets check if prometheus and grafana pods are running already
   ```
kubectl get pods -n prometheus
kubectl get svc -n prometheus
   ```
This confirms that prometheus and grafana have been installed successfully using Helm

### 11. Edit Prometheus Service
Update the ClusterIP to LoadBalancer
   ```
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
   ```
### 12. Edit Grafana Service
Update the ClusterIP to LoadBalancer
   ```
kubectl edit svc stable-grafana -n prometheus
   ```
### 13. Verify if service is changed to LoadBalancer and also to get the Load Balancer IP.
   ```
kubectl get svc -n prometheus
   ```
### 14. Go to the Grafana Server and Create Dashboards
Use the default credentials:
- UserName: admin
- Password: prom-operator
### 14. Import Dashboards with IDs
12740,3119,6417(pods)
