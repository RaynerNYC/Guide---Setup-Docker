# Guide---Setup-Docker
Simple Guide on setting up Docker Environment

Docker is a tool that allows developers, sys-admins etc. to easily deploy their applications in a sandbox (called containers) to run on the host operating system i.e. Linux. 
The key benefit of Docker is that it allows users to package an application with all of its dependencies into a standardized unit for software development. 
Unlike virtual machines, containers do not have the high overhead and hence enable more efficient usage of the underlying system and resources.

Reference tutorial : 
https://jaxenter.com/playing-with-spring-boot-docker-in-netbeans-ide-127672.html

(with JPA h5 and postgre)
https://jaxenter.com/how-to-write-a-java-ee-application-using-spring-boot-and-docker-on-netbeans-ide-8-2-133200.html


---------------------------------------------------------------------------------------------------------------------------------------
### Installation with Docker Desktop
---------------------------------------------------------------------------------------------------------------------------------------
** pre-requisite Requires Microsoft Windows 10 Professional or Enterprise 64-bit.
1. download docker for windows : https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe

2. extra info (installation guide) : https://docs.docker.com/docker-for-windows/install/#install-docker-for-windows-desktop-app

3. Install : Docker for Windows Installer.exe

4. Follow the install wizard to accept the license, authorize the installer, and proceed with the install.
You are asked to authorize Docker.app with your system password during the install process. 
Privileged access is needed to install networking components, links to the Docker apps, and manage the Hyper-V VMs.
Click Finish on the setup complete dialog to launch Docker.

---------------------------------------------------------------------------------------------------------------------------------------
### Installation with Docker Toolbox for older/other Windows version 
---------------------------------------------------------------------------------------------------------------------------------------
1. download docker for windows : https://download.docker.com/win/stable/DockerToolbox.exe

2. extra info >> Docker Toolbox overview : https://docs.docker.com/toolbox/overview/#whats-in-the-box
			        >> Docker Toolbox get started tutorial : https://docs.docker.com/get-started/

3. Install : DockerToolbox.exe

4. Follow the install wizard to accept the license, authorize the installer, and proceed with the install.
You are asked to authorize Docker.app with your system password during the install process. 
Privileged access is needed to install networking components, links to the Docker apps, and manage the Hyper-V VMs.
Click Finish on the setup complete dialog to launch Docker.

---------------------------------------------------------------------------------------------------------------------------------------
### Start docker
---------------------------------------------------------------------------------------------------------------------------------------
1. Windows START MENU > search for Docker Quickstart Terminal, select Docker for Windows in the search results, and click it (or hit Enter).
   >> Alternatively, "C:\Program Files\Git\bin\bash.exe" --login -i "C:\Program Files\Docker Toolbox\start.sh"

2. ** ERROR ** VT-x/AMD-V hardware acceleration is not available on your system
SOL : 	
    1) Try uninstall Hyper-V first : 
		Control Panel > Uninstall a Program. 
		In the “Programs and Features” window, click “Turn Windows features on or off.”
		In the “Windows Features” window, clear the “Hyper-V” checkbox and then click “OK.”
		restart your PC and then you can try using VirtualBox or VMware again.

		2) Turn Intel VT-x On in Your BIOS or UEFI Firmware:
		Go to Windows START menu > SHIFT+Restart Windows
		Once in UEFI: go Startup Settings > ... advance > find “Intel VT-x,” “Intel Virtualization Technology,” “Virtualization Extensions,” “Vanderpool, and enable
		Save and quit

---------------------------------------------------------------------------------------------------------------------------------------
### Hello World
---------------------------------------------------------------------------------------------------------------------------------------
1. Start Docker Toolbox : "C:\Program Files\Git\bin\bash.exe" --login -i "C:\Program Files\Docker Toolbox\start.sh"

2. Verify Docker environment is running : 	$docker --version 
											$docker version
											$docker info
											
3. Run a helloworld application (build in) : 	$docker run hello-world
** it will download if cannot find the application or will download latest image if have

4. Check output where it printed : Hello from Docker!

5. To check downloaded image : 			$docker image ls

6. List the hello-world container:		$docker container ls
** since hello-world container (spwned by the image) will exit after displaying the message, it's not running anymore.
** therefore u need to run with -all so that non running container is shown >>>> $docker image ls -all

---------------------------------------------------------------------------------------------------------------------------------------
### Cheat sheet commands
---------------------------------------------------------------------------------------------------------------------------------------

## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls
docker image --all

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq

## Docker machine
docker-machine ls
docker-machine create
docker-machine create --driver virtualbox default      (for Mac)
docker-machine create --driver hyperv default          (for Win)
docker-machine env <environment machine name>          (tell Docker to talk to new machine)
docker-machine env default
eval "$(docker-machine env default)"					(connect shell to the new machine)
docker-machine ip default
docker run -d -p 8000:80 nginx							 (run a Nginx webserver)
curl $(docker-machine ip default):8000
docker-machine stop default
docker-machine start default

