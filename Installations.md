# Installing maven 
```
* wget https://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.9.9-bin.tar.gz
  tar -xvf apache-maven-3.9.9-bin.tar.gz
  mv apache-maven-3.9.9 /opt/
  sudo vi ~/.bashrc ## Copy the below path in bashrc file
   M2_HOME='/opt/apache-maven-3.9.9'
   PATH="$M2_HOME/bin:$PATH"
   export PATH
  source ~/.bashrc 
       or 
  vi /etc/environment
   :/opt/apache-maven-3.9.9/bin
  source /etc/environment

  mvn --version
```
# Installing AWS CLI 
```
*curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  sudo apt install unzip
  unzip awscliv2.zip
  sudo ./aws/install
* aws --version  

* aws configure                ## Create an access key from iAM 
```
# Installing AZURE CLI 

* [Refer here ](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt) for using ACR
  
```
* sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

* sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
  gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg

* AZ_DIST=$(lsb_release -cs)
echo "Types: deb
URIs: https://packages.microsoft.com/repos/azure-cli/
Suites: ${AZ_DIST}
Components: main
Architectures: $(dpkg --print-architecture)
Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources

* sudo apt-get update
sudo apt-get install azure-cli
```

# Installing Docker 

```

* curl -fsSL https://get.docker.com -o install-docker.sh
  sudo sh install-docker.sh
* sudo usermod -aG docker <username>

* docker info 
```
# Command to Run sonarQube and Nexus
```
* docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
* docker run -d --name nexus -p 8181:8181 sonatype/nexus3 
```

# Installing java & jenkins on ubuntu

```
* sudo apt update 
  sudo apt install openjdk-17-jdk -y
```


```
* sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y

```

# Installing trivy
```

* sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y

* trivy --version
 
```


# Installing kubeadm, kubelet, kubectl

```
* sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg	
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list


* sudo apt-get update
  sudo apt-get install -y kubelet kubeadm kubectl
  sudo apt-mark hold kubelet kubeadm kubectl
```

* [Refer here ](https://github.com/Mirantis/cri-dockerd/releases) for cri socket

```
wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.15/cri-dockerd_0.3.15.3-0.ubuntu-jammy_amd64.deb
sudo dpkg -i cri-dockerd_0.3.15.3-0.ubuntu-jammy_amd64.deb


# Choose your (master node) become a root user
kubeadm init --cri-socket unix:///var/run/cri-dockerd.sock


# In nodes copy from master node to nodes
kubeadm join 10.138.0.7:6443 --token 4tq73h.nkj0pheitofzmh0k \
        --discovery-token-ca-cert-hash sha256:1c8c3352dfd8bc614055938004c425d0018fbca9e0bf2d07107fdc9f712d5811 --cri-socket unix:///var/run/cri-dockerd.sock
      

# For Network (In Master Node)
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```


# Installing Prometheus (Monitoring Tool) [Refer here ](https://prometheus.io/download/) for prometheus application

```
* wget https://github.com/prometheus/prometheus/releases/download/v3.0.0-beta.0/prometheus-3.0.0-beta.0.linux-amd64.tar.gz
* tar -xvf prometheus-2.52.0.linux-amd64.tar.gz  #extact the tar file
* mv prometheus-2.52.0.linux-amd64 prometheus   # copy or move the file 
```

#### And also install blackbox_exporter and Node_exporter and extract the file and do same process as prometheus

```
* ./prometheus &  ==> To run prometheus in background
* pgrep prometheus  
* kill 106377  ==> To kill the prometheus
```
# Installing Grafana (Monitoring Tool) [Refer here ](https://grafana.com/grafana/download) for grafana application
```
* sudo apt-get install -y adduser libfontconfig1 musl
* wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.2.2_amd64.deb
* sudo dpkg -i grafana-enterprise_11.2.2_amd64.deb

* sudo /bin/systemctl start grafana-server   ==> To start the grafana server
# 3000 => Grafana running port




