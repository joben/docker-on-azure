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
 
##Attach a new disk to the Linux VM. This will store persistent data for the docker containers.

1. Create a new storage account for project related (application level) data
```Shell
  az storage account create -g dockerdev -n projectrepo -l southeastasia --type Standard_LRS
  ##show newly created storage account
  
  az storage account show -g dockerdev -n projectrepo
  az storage account list -g dockerdev -n projectrepo
```
2. Set environment variable (for the session) to enable the CLI to query the storage account
```Shell
  export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string -g dockerdev -n projectrepo)
```

3. Attach a new disk to the Linux VM
```Shell
az vm disk attach-new -g dockerdev --vm-name mentos \
--vhd https://projectrepo.blob.core.windows.net/vhds/pyprojects.vhd \
--disk-size 50 --name pyprojects.vhd  --lun 0
```
4. Login to the VM
```Shell
  ssh ops@mentos
```

5. View disk partitions

```Shell
dmesg | grep SCSI
```
6. Partition the Disk
```Shell
  sudo fdisk /dev/sdc

  The device presents a logical sector size that is smaller than
  the physical sector size. Aligning to a physical sector (or optimal
  I/O) size boundary is recommended, or performance may be impacted.
  Welcome to fdisk (util-linux 2.23.2).

  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.

  Command (m for help): q
```

https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-linux-add-disk?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json


