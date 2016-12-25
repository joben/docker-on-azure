#Create a Docker Host on Azure using Centos

Make sure you are logged in to your Azure account. 

1. Create a Resource Group
```Shell
  az resource group create -n myResourceGroup -l southeastasia
```

2. Create a Linux VM using Centos image
```Shell
  az vm create \
  --image centos \
  --admin-username ops \
  --ssh-key-value ~/.ssh/id_rsa.pub \
  --public-ip-address-dns-name mydns \
  --resource-group myResourceGroup \
  --location southeastasia \
  --name myVM
```

The CLI will not show any progress indicator. 

https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-linux-quick-create-cli?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json

3. Connect to your linux vm

```Shell
  ssh ops@mydns.southeastasia.cloudapp.azure.com
```

4. Create a config file for ssh connections

```Shell
  touch ~/.ssh/config
  nano ~/.ssh/config
  chmod 600 ~/.ssh/config
```

Enter the following in the config file

```Shell
  Host myVM
    HostName mydns.southeastasia.cloudapp.azure.com
    User ops
    Port 22
    IdentityFile ~/.ssh/id_rsa
 ```
 ##Installing the Docker Engine
 ###Installing with yum
 
 1. Update packages
 
 ```Shell
  sudo yum update
 ```
 2. Add yum repo
 ```Shell
  sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
  [dockerrepo]
  name=Docker Repository
  baseurl=https://yum.dockerproject.org/repo/main/centos/7/
  enabled=1
  gpgcheck=1
  gpgkey=https://yum.dockerproject.org/gpg
  EOF
  ```
  3. Install the docker engine
  ```Shell
  sudo yum install docker-engine
 ```
 4. Enable the service
 ```Shell
 sudo systemctl enable docker.service
 ```
 
 5. Start the docker daemon
 ```Shell
 sudo systemctl start docker
 ```
 
 6. Verify docker is running
 ```Shell
 sudo docker run --rm hello-world
 ```

 7. Create a docker group
 
 ```Shell
   sudo groupadd docker
   sudo usermod -aG docker ops
 ```
 8. Log out and log back in
 
 You should now be able to run docker without sudo
 
 
References:
 https://docs.docker.com/engine/installation/linux/centos/
 

