# ISTIO

with Singam

# 1. Create AWS EC2 inastance (min requirement 2cpus, 4gb ram)
####     Login to instance, Switch to root user
    sudo su -
# 2. Install kubectl
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl
    kubectl version --client
    
####     sha256 check u can do after this(optional)
    
# 3. Install eksctl
    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version
# 4. Add IAM role to EC2
# 5. Create cluster 
    eksctl create cluster --name my-cluster --region us-west-1
####    (This takes some time, in the mean time u can install ISTIO(open new terminal and follow step 7)
####    check if cluster is created  
    eksctl get cluster --region=us-west-1
# 6. Create Nodegroup
####    Nodegroups got automatically created for me, if not for u use the below commands
    eksctl create nodegroup --cluster=my-cluster --region=us-west-1
# 7. Install ISTIO
    curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.18.1 TARGET_ARCH=x86_64 sh -

# 8. cd inti istio directory 
    cd istio-1.18.1
#### Explore the files and directories present in the istio directory
# 9. Set PATH for istio
#### Make sure u are in istio directory when doing this
    export PATH=$PWD/bin:$PATH
# 10. Install istio profile
    istioctl install --set profile=demo -y
# 11. Deploy the sample application present in sample directory
# 12. Enable ISTIO on namespace
    kubectl label namespace default istio-injetion=enabled
# 13. Analyse istio config
# 14. Expose ports for which Kiali and Jaegar are liseting
# 15. Explore monitoring and tracking 
