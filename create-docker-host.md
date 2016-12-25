#Create a Docker Host on Azure using Centos

Make sure you are logged in to your Azure account. 

1. Create a Resource Group
```Shell
  az resource group create -n myResourceGroup -l westus
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
 
