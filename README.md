# Prometheus_Project
# Monitoring a Kubernetes Cluster Using Prometheus
Monitoring a Kubernetes cluster is essential for ensuring the stability, performance, and health of containerized applications running in a dynamic environment. Prometheus, a popular open-source monitoring and alerting toolkit, provides powerful capabilities for collecting, querying, and visualizing metrics from Kubernetes clusters. By integrating Prometheus with Kubernetes, you gain insights into resource utilization, application performance, and infrastructure health, enabling proactive management and timely response to issues.

## Prerequisites
- Docker
- Minikube
- Helm
- Prometheus
- Grafana

## Installation

## Docker Installation

First you have to uninstall old versions. 
bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine


Then begin the installation process:

1. Install `` yum-utils`` package:
bash 
sudo yum install -y yum-utils 


2. Add docker-ce.repo repository to download Docker:
bash 
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 

3. Installing Docker packages:
bash 
$ sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin 

4. Enabling Docker service:
bash 
$ sudo systemctl enable --now docker


## Install and Set Up kubectl

1. Download the latest release with the command:
bash 
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl


2. Make the kubectl binary executable:
bash 
$ chmod +x ./kubectl


3. Move the binary into your PATH:
bash 
$ sudo mv ./kubectl /usr/local/bin/kubectl


4. Verifying Installation:
bash 
$ kubectl version


## Minikube Installation

1. Download Minikube last release:
bash 
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

2. Install Minikube package:
bash 
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube

3. Start Minikube:
bash 
$ minikube start --driver=docker --force


## Helm Installation

1. Fetch that script:
bash 
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

2. Provide execute permission to the file:
bash 
$ chmod 700 get_helm.sh

3. Run the script:
bash 
$ ./get_helm.sh


### Deploy Prometheus
1.Add Prometheus Helm repository
bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

2.Update the Helm repositories:
bash
helm install prometheus prometheus-community/prometheus

3.Install Prometheus using Helm:
bash
helm repo update

4.Install Prometheus:
bash
helm install prometheus prometheus-community/prometheus

5.Expose Prometheus service:
bash
kubectl expose service prometheus-server — type=NodePort — target-port=9090 — name=prometheus-server-ext

6.Open Web App of Prometheus
bash
minikube service prometheus-server-ext

### Deploy Grafana

1.Add Grafana Helm repository:
bash
helm repo add grafana https://grafana.github.io/helm-charts

2.Update the Helm repositories:
bash
helm install grafana grafana/grafana

3.Install Grafana using Helm:
bash
helm repo update

3.Expose Grafana service:
bash
kubectl expose service grafana — type=NodePort — target-port=3000 — name=grafana-ext

3.Open Grafana Web APP
bash
minikube service grafana-ext


## Get Grafana Credintials
bash
kubectl get secret --namespace default grafa
na -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

### Conclusion

In conclusion, implementing Prometheus for monitoring a Kubernetes cluster provides crucial visibility into resource usage, performance metrics, and overall cluster health. By deploying Prometheus alongside Grafana, teams can efficiently visualize and analyze these metrics, enabling proactive management and timely resolution of issues. This monitoring setup empowers organizations to optimize their Kubernetes environments, enhance operational efficiency, and deliver reliable containerized applications. Continuing to refine and expand monitoring capabilities with Prometheus supports a culture of continuous improvement and ensures the stability and scalability of Kubernetes deployments.

## Outputs


![K8Scluster](https://github.com/ebthall619/Prometheus_Project/assets/81996620/4311199a-2890-4b79-b756-7541f955021d)
![k8s2](https://github.com/ebthall619/Prometheus_Project/assets/81996620/85cab3f6-e3d5-4c5a-8af1-0025715c9079)
![k83](https://github.com/ebthall619/Prometheus_Project/assets/81996620/df71eddc-32d3-416e-a1db-f7b662e2d134)
![WhatsApp Image 2024-05-03 at 3 11 47 PM](https://github.com/ebthall619/Prometheus_Project/assets/81996620/737bc17b-d11e-4a1b-8b59-cb491ccfaf58)


