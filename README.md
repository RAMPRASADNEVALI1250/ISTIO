# ISTIO

with Singam

# 1. Create AWS EC2 inastance (min requirement 2cpus, 4gb ram)
    Login to instance, Switch to root user --> ```sudo su -```
# 2. Install kubectl
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl
    kubectl version --client
    --> sha256 check u can do after this(optional)
    
# 3. Install eksctl
    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version
# 4. Add IAM role to EC2
# 5. Create cluster 
    eksctl create cluster --name my-cluster --region us-west-1
    (This takes some time, in the mean timeu can install ISTIO(open new terminal and follow step 7)
    check if cluster is created  --> eksctl get cluster --region=us-west-1
# 6. Create Nodegroup
    Nodegroups got automatically created for me, if not for u use below commands
    eksctl create nodegroup --cluster=my-cluster --region=us-west-1
# 7. Install ISTIO
    curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.18.1 TARGET_ARCH=x86_64 sh -
    
    cd into istio folder
    export PATH=$PWD/bin:$PATH
    istioctl install --set profile=demo -y
