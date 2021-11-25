# FoundryVTT Docker Stack

Hi! This is my pre-made Docker stack, which is an all round solution to for FoundryVTT. This stack uses Traefik, FileBrowser and Portainer for management. FileBrowser  [(link)](https://github.com/hurlenko/filebrowser-docker) allows easy access to your files without having to use SCP/FTP. Using Portainer [(link)](https://github.com/portainer/portainer) for easy monitoring & control of your containers. And Traefik [(link)](https://github.com/traefik/traefik) is used as a Reverse-Proxy and also as a super easy management of SSL certs using LetsEncrypt. In this stack I use the FoundryVTT [(link)](https://github.com/BenjaminPrice/fvtt-docker) container which was built by [BenjaminPrice](https://github.com/BenjaminPrice/fvtt-docker/commits?author=BenjaminPrice "View all commits by BenjaminPrice").


# Prerequisites

- **Domain Name**
	- You will need to have a domain name, where you can point a number of subdomains too. This is so that each of the services that are used can be controlled from each domain. All of these domain will be pointed to the same IP (which is the Ubuntu Server).
	- Portainer - `management.domain.com`
	- FileBrowser - `filebrowser.domain.com`
	- FoundryVTT - `foundry.domain.com`
	- Traefik - `deployment.domain.com`
- **Ubuntu Server**
	- You will need a Ubuntu Server with access an public IP. The best option for this is too use a cloud provider like DigitalOcean... AWS..... Linode....etc! 
	- I personally use DigitalOcean with the $5 a mouth droplet. This works perfectly well.
	- You will also need to know basic Linux/Ubuntu so that you can login to your server and also point the required sub domains to your server IP.
- **FoundryVTT License**
	- You will need to buy a license for FoundryVTT which you can buy from [here](https://foundryvtt.com/).
	- You will also need to download the required .zip [here](https://foundryvtt.com/community/jmast3rs/licenses) with the OS 'Linux/NodeJS'.


## Setup
Once you have done the prerequisites e.g. have a server.... pointed your sub domains to your server.... and brought foundry with the need zip file.

First you need to clone my git repo! This is simple and can be done with one line!
`sudo git clone https://github.com/JMast3rs/foundryvtt_docker_stack.git`

Once you have downloaded that you will need to edit the listed files.
- `docker-compose.yml`
	- In this file you will need to replace the line with `.domain.com` with your domain. This will need to be done for `management.domain.com` , `filebrowser.domain.com` , `foundry.domain.com` 
	
- `data/traefik/traefik_dynamic.toml`
	- In this file you will need to replace the line with `deployment.domain.com` with your domain.

Next you can will need to upload your foundry `foundryvtt-0.x.x.zip` to the `foundry_download` folder.

### Installing Docker, Docker-Compose and setting up Traefik!

All the needed commands are in the setup.sh file. You can run it with the command below, this may take up to 5mins to run.
`sudo sh setup.sh`

If you have done everything correct... running the `sudo docker ps` should output something like this.
```root@ubuntu-development-1:~/foundryvtt_docker_stack# sudo docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                                                      NAMES
12c1dd3239bd   portainer/portainer-ce:latest   "/portainer -H unix:…"   10 seconds ago   Up 7 seconds    8000/tcp, 9000/tcp, 9443/tcp                                               portainer
8f576c425478   direckthit/fvtt-docker:latest   "/bin/sh -c /opt/fou…"   10 seconds ago   Up 7 seconds    30000/tcp                                                                  foundry
3d789910f0b7   hurlenko/filebrowser            "/filebrowser --root…"   10 seconds ago   Up 7 seconds    8080/tcp                                                                   filebrowser
a4219b077ba4   traefik:v2.2                    "/entrypoint.sh trae…"   11 seconds ago   Up 10 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp   traefik
```

Give it 5min+ once the command has ran and you should be able to navigate to your webservers..... 

 Logins for Filebrowser & Traefik are both **admin/password**.

