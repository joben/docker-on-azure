#Create a Docker host on Linux
This docker host will be a CentOS Linux VM running on Azure

1. install coreos on azure
https://coreos.com/os/docs/latest/booting-on-azure.html
2. install docker on coreos
3. secure docker daemon

#Secure the Docker Daemon and accessible via https
https://docs.docker.com/engine/security/https/

reference: https://blogs.msdn.microsoft.com/opensourcemsft/2015/09/26/step-by-step-set-up-docker-on-azure-connect-to-nginx-container-from-windows/
reference: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-quick-create-cli/

#Create a docker host on Windows Server 2016

az vm create -g rockthedemo -n windcon \
--image MicrosoftWindowsServer:WindowsServer:2016-Datacenter-with-Containers:2016.0.20161108 \
--admin-username joben --admin-password Pass@word123 --public-ip-address-allocation static \
--public-ip-address-dns-name windcon --size Standard_D3_v2 
##Show status
az vm show --name windcon -g rockthedemo
