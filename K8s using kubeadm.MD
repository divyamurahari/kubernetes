sudo apt-get update

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update -y

sudo apt-get install docker-ce docker-ce-cli containerd.io -y


cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF





sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl restart docker

sudo apt-get update


sudo apt-get install -y apt-transport-https ca-certificates curl


sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg



echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update


sudo apt-get install -y kubelet kubeadm kubectl


sudo apt-mark hold kubelet kubeadm kubectl

------------Only in Master------------------

sudo kubeadm init --pod-network-cidr 10.0.0.0/16

if this error occur
If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher


use it 

rm /etc/containerd/config.toml
systemctl restart containerd
sudo kubeadm init --pod-network-cidr 10.0.0.0/16


kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml




----------------------------------------Worker Node---------

kubeadm join 172.31.5.129:6443 --token 9c3yfc.inau0ckha26mtxg8 --discovery-token-ca-cert-hash sha256:796067f0e8bcdbd839b69463d0bf8517d98c3b30eee26a11d9de80ac2ef2746c

--------------------------------------------

kubectl get nodes   //get ip

-------in Master to label the Worker node as Worker--- ---
kubectl label node

kubectl label node ip-172-31-7-102 node-role.kubernetes.io/worker=worker


sudo nano nginx-deploy.yml
-------------------nginx deploment.yml-------

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
------------------------------------------------------

kubectl apply -f nginx-deploy.yaml

kubectl get pods
kubect get deploy
kubectl edit deplo <deploy name>

kubectl create service nodeport nginx --tcp=80:80

