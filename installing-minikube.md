REF:https://pwittrock.github.io/docs/tasks/tools/install-kubectl/
////////////////////////install kubectl////////////////
1  curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.7.0/bin/linux/amd64/kubectl
    2  chmod +x ./kubectl
    3  kubectl version
    4  kubectl restart
    5  kubectl
    6  kubectl --version
    7  kubectl version
    8  sudo apt-get update
   ------------------------Install Docker Engine on Ubuntu----------------------
    REF:https://docs.docker.com/engine/install/ubuntu/

sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
    sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    
    sudo apt-get update
    
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

------------installing cri-dockerd------------------
REF: https://github.com/Mirantis/cri-dockerd#build-and-install
       sudo groupadd docker
   18  sudo usermod -aG docker $USER
   19  sudo systemctl enable docker
   20  sudo systemctl status docker
   21  git clone https://github.com/Mirantis/cri-dockerd.git
   22  # Run these commands as root
###Install GO###
wget https://storage.googleapis.com/golang/getgo/installer_linux
chmod +x ./installer_linux
./installer_linux
source ~/.bash_profile

cd cri-dockerd
mkdir bin
go build -o bin/cri-dockerd
mkdir -p /usr/local/bin
install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
cp -a packaging/systemd/* /etc/systemd/system
sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
systemctl daemon-reload
systemctl enable cri-docker.service
systemctl enable --now cri-docker.socket

...................................................installing minikube,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,




   66  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   67  ls
   69  chmod +x minikube-linux-amd64
       mv minikube-linux-amd64 minikube
   71  sudo mv minikube /usr/local/bin/
   75  minikube version
   76  sudo minikube start --vm-driver=none
   
   Error: X Exiting due to GUEST_MISSING_CONNTRACK: 
   
   77  sudo apt-get install -y conntrack
   78  sudo minikube start --driver=none
   
   Error: Exiting due to RUNTIME_ENABLE: Temporary Error: sudo crictl version: exit stat                                                                              us 1

-----------------------------------solution copy full------------------
VERSION="v1.25.0"
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-$VERSION-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
--------------------------------------------------------------------------  


minikube start --driver=none


//MiniKube Installed you can check by :- minikube status





