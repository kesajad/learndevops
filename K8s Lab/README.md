# WhiteBoard
![AKS Workflow](https://github.com/kesajad/learndevops/assets/99335234/1ad3fcf5-ff60-41a4-82b6-45f697cfe88c)
# Kubernetes components
## Kubernetes components are broken down in to two parts,
The control plane components which include kube-apiserver, kube-controller-manager,etcd and kube-scheduler and node components which include kubelet, kube-proxy and container runtime.
  
### [x] Control plane components: Provide core k8s services and orchestrations workloads
- Kube-api server : expose workloads, managing the api to access it, like kubectl
- Etcd: maintains the state of the cluster in a key value pair format
- Kube-controller-manager : oversees smaller controllers that perform replication pods or node operations
- Kube-scheduler : create/scaling decide what nodes can run the workloads 
### [x] Node components: Actual application workloads
- Kubelet : agent that process orchestration request from the control plane and schedule the requests
- Kube-proxy : routes network traffic and manages IP addresses for sources and pods
  
## How interactions are happening?

![image](https://github.com/kesajad/learndevops/assets/99335234/42712ace-0c7c-4f93-9ae1-4ff664da40dd)

Login to Azure
```
az login --use-device-code
```
set subscription; only needed if you have multiple subscriptions.
```
az account set --subscription "Visual Studio Enterprise Subscription – MPN"
```
Set subscription; only needed if you have multiple subscriptions.
```
az configure --defaults group=rg-aks-test-001
```
Get credentials from azure
```
az aks get-Credentials --name aks-test-001
```
Just confirming the current-context
```
kubectl config current-context
```
Get the list of pods
```
kubectl get pods
```
Get the list of nodes
```
kubectl get nodes
```
# Create an nginx app using cli
Create a container using cli
```
kubectl create deployment my-app-nginx --image=nginx --replicas=1
```
Get the list of deployment & pods
```
kubectl get deployment
```
```
kubectl get pods
```
Expose the application to public
```
kubectl expose deployment my-app-nginx --type=LoadBalancer --port=80 --target-port=80
```
```
kubectl get pods
```
Get the list of services
```
kubectl get services
```
# Create a Custom Application with nginx in AKS
### Step 1: Create a ConfigMap with Custom HTML
Create a index.html file in your local directory.
```
vim index.html
```
```
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Welcome to Azure Cloud DevOps | Guruschools</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        h1 {
            color: #007bff;
        }
        h2 {
            color: #ff0000;
            animation: blinkAnimation 1s infinite; /* Apply blinking animation */
        }
        p {
            font-size: 18px;
            line-height: 1.6;
        }
        .section-heading {
            font-size: 24px;
            font-weight: bold;
            color: #007bff;
            margin-top: 40px;
        }

        @keyframes blinkAnimation {
            0% { opacity: 1; }
            50% { opacity: 0; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to Azure Cloud DevOps</h1>
        <p>Learn and master cloud-based DevOps with our comprehensive courses and resources.</p>
        <h2>SERVER 1</h2>
    </header>

    <section>
        <div class="section-heading">Courses at Guruschools</div>
        <p>Explore the wide range of courses offered at Guruschools to enhance your skills and knowledge.</p>
    </section>

    <footer>
        <p>© 2024 Azure Cloud DevOps | Guruschools. All rights reserved.</p>
    </footer>
</body>
</html>

```
### Step 2: Create a ConfigMap with Custom HTML 
```
kubectl create configmap custom-html --from-file=index.html
```
### Step 3: Create a Deployment YAML File
Create a deployment YAML file that uses the ConfigMap to serve custom HTML with Nginx. Here’s an example deployment.yaml:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-nginx-app
  template:
    metadata:
      labels:
        app: my-nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - name: html-config
          mountPath: /usr/share/nginx/html
      volumes:
      - name: html-config
        configMap:
          name: custom-html
```
### Step 4: Apply the Deployment
```
kubectl apply -f deployment.yaml
```
### Step 5: Create a LoadBalancer Service
Create a service YAML file to expose your Nginx deployment using a LoadBalancer. Here’s an example service.yaml:
```
apiVersion: v1
kind: Service
metadata:
  name: my-nginx-service
spec:
  type: LoadBalancer
  selector:
    app: my-nginx-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```
### Step 6: Apply the Service
```
kubectl apply -f service.yaml
```
### Step 7: Access the Service
```
kubectl get services my-nginx-service
```
