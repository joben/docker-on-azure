#Run a docker container
docker run -it ubuntu:latest bash
cat /etc/*release

docker run -it centos:latest bash
cat /etc/*release

docker run -it debian:jessie bash
cat /etc/*release

touch somefile.txt

docker images

docker run ubuntu echo "hello. this is ubuntu"

docker ps

docker pull nginx
docker run -d nginx
docker run -d -p 80:80 --name nginxweb nginx

docker run -d -p 80:80 --name static-site seqvence/static-site

docker run -d -p 8000:8000 --name nginxweb2 nginx

docker stop nginxweb

docker rm static-site

#Visual Studio Docker Tools

*Create an ASP.NET Core WebApp in VS 2017
*Enable docker support
*F5
*docker ps
*edit layout . add to footer <p>Made with <span class="glyphicon glyphicon-heart"></span> by DX</p>

#setup an ACS DCOS cluster
##Using azure cli 2.0 -- much simpler than using a template
az resource group create -l "Southeastasia" -n "tiltokyo"

az acs create -d til -n tilimetu -g tiltokyo --admin-username joben --agent-count 1 \
   -l "Southeastasia" --master-count 1 --orchestrator-type dcos \
   --ssh-key-value /home/joben/.ssh/id_rsa.pub

az acs list

#Live Debugging on Docker
https://blog.docker.com/2016/07/live-debugging-docker/
