# SiteConnect Developer Envirnment

Building a solid developer envirment for ```Siteconnect``` development 
with NodeJS in a WSL Distribution and a ```Postgres``` database running in a
Docker Container.

![Setup](https://lucid.app/publicSegments/view/74aff30f-a632-4245-b004-4338cb8d9fcc/image.png)

**Components:**

- Visual Studio Code
- Microsoft's WSL (linux core system)
- Docker Desktop
- DBeaver (Univeral Database Client)
- Postgres Database (Docker Container)
- Ubnutu 18.04 LTS (WSL Distribution)

# Prerequistes

All the following applications needs to be installed before you begin.
If you do a fresh installation, use all the defaults during the installation.
Follow the Installation Guides of each Application.

- [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- [Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/get-started)
- [Ubuntu 18.04 LTS](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
- [Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)
- [DBeaver Community Version](https://dbeaver.io)

Further explaination integrates each of the applications into the devlopement environment.

# Preparing WSL (Ubuntu 18.04.LTS)

All the following steps needs a [```PowerShell```](https://www.digitalcitizen.life/ways-launch-powershell-windows-admin/) command promt.

Use the ```Windows Terminal``` which you installed before. [Check the Prerequisites.](#prerequsites)

# Distribution

As a kind of **Best-Praxis** we will clone the ```Ubuntu 18.04 LTS``` distribution
and do the customization in our own project distribution (siteconnect).

**Steps:**
- [Create a work foler](#workfolder)
- [Prepare the ```Ubuntu 18.04.LTS``` Distribution for cloning.](#prepare)
- [Clone into our porject distribution.](#clone)
- [Customize the ```siteconnect``` project distribution.](#customize)

## Workfolder

Create the folloing folder on your C Drive:
```bach
C:\Distributions
```
## Prepare

Start Ubuntu 18.04 LTS and use the folloing username/password combination.
Feel free to change the password on you own choise. Keep in mind you maybe
need this password at a later point. Write it down or save it in secured place.

```
Username: ubuntu
Password: ubuntu
````

After the initial start of Ubuntu and finalizing the configuration you can go ahead 
and set the user ```ubuntu``` in a special **sudo** status.
This avoids the password question, if you execute commands that nedds **root** permissions.
```bash
$ sudo bash -c "echo 'ubuntu ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/ubuntu"
```

Next step is to install the following packages:
```bash
$ sudo apt-get update
$ sudo apt-get install -y install vim curl git tree wget postgresql-client
```

Feel free to add more if you think it makes sense to have them in your template.

After the installation is completed, **exit** the distribution by typing ```exit``` at the command promt.

## Clone

Best praxis is always to build a dedicated Distribution for your project.

Steps will be:
- [Export the Template (Ubuntu 18.04 LTS) we prepared in the prevous step.](#export)
- [Create a Clone of the Template (Project Distribution).](#create)
- [Customize the cloned Distribution.](#cutomize)

### Export

This step will create a template for the final **Project Distribution**.
It simply exports the customized ```Ubuntu 18.04 LTS```.
All commands needs to get applied in a **PowerShell** command shell.
```pws
PS C:\> wsl.exe --export Ubuntu-18.04 C:\Distributions\ubuntu-18.04-template.tar
```

### Create

Now we can create our ```Project Distribution```

It creates a clone of the exported Template of the last [step](#export)
```pws
PS C:\> wsl.exe --import siteconnect-ubuntu-18.04 C:\Distributions\siteconnect-ubuntu-18.04 C:\Distributions\ubuntu-18.04-template.tar
```

Making our life easy, let's set the ```Project Distibution``` as default.
```pws
PS C:\> wsl.exe --set-default siteconnect-ubuntu-18.04
```

You can check the success by typing:
```pws
PS C:\> wsl.exe --list --verbose
```

The Output of this command should show you something like:
```bash
NAME                        STATE           VERSION
* siteconnect-ubuntu-18.04    Running         2
  docker-desktop-data         Running         2
  Ubuntu-18.04                Stopped         2
  docker-desktop              Running         2
```

The ```*``` maked Distibution is the default.

## Customize

Now we start the new created ```siteconnect-ubuntu-18.04``` Distribution the first time.
```pws
PS C:\> wsl.exe --user ubuntu
```

After a successfull start and login crate a new user **siteconnect** with the same
special **sudo** settings as we did with the **ubuntu** user.
```bash
$ sudo groupadd -r siteconnect
$ sudo useradd -m -r -g siteconnect -d /home/siteconnect -s /bin/bash -c "SiteConnect User Account" siteconnect
$ sudo usermod -aG sudo siteconnect
$ sudo bash -c "echo 'siteconnect ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/siteconnect"
```

If the commands are done go and ```exit``` the Distribution again.

Now we will login with the new created user **siteconnect** and finalize the customization.

```pws
PS C:\> wsl.exe --user siteconnect
```

> IMPORTANT:
>  
> Be sure, you are in the linux-home-directory of the user **siteconnect**.
> YOu can test this by typing ```pwd```. You should get an output: ```/home/siteconnect```.
> If you are in another folder, use ```cd``` to jump to the linux-home-directory.
> Be sure you are in the right folder, before you go ahed.

Generate SSH Key for user **siteconnect**
```bash
- ssh-keygen -t rsa -b 4096 -C "siteconnect"
```

Aternatively, you can also use an already created SSH key
if you have one you normaly use. Feel free and copy this key for the
user **siteconnect**

Create a ./ssh/config file
```bash
$ bash -c 'cat << EOF > ~/.ssh/config
Host *
 ForwardAgent  yes
 UseKeychain yes
 IdentityFile ~/.ssh/id_rsa
EOF'
```

Usind the ```-A``` option to forward the key to another SSH session,
you need to enable the **ssh-agent** every time, before you do the SSH login.
Here an example of how to enable it:

```bash
eval "$(ssh-agent -s)"
```

As a last step, we need to create a **wsl.conf** file.
Here we can set default of the Distribution.

Find detailed information about the posibilties here:
- [WSL commands and launch configurations](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)

Create /etc/wsl.conf with defaults:
```bash
$ sudo bash -c 'cat << EOF > /etc/wsl.conf
[network]
generateHosts = true
generateResolvConf = true

[user]
default=siteconnect
EOF'
```

After applying, **exit** the Distribution and **terminate** it with the following command:
```pws
PS C:\> wsl.exe --terminate siteconnect-ubuntu-18.04
```

> IMPORTANT: 
> 
> If you change/add somthing in **/etc/wsl.conf** the Distribution needs to get
> **teminated**. This command does a complete shutdown of the Distribution. If you reconnect 
> to it, it is like a reboot. The settings in the configuration file gets applied by this reboot.

Restart the ```siteconnect-ubuntu-18.04``` Distribution by simply type:
```pws
PS C:\> wsl.exe
```

You might realize, the login user is now **siteconnect**.

## Install NodeJS

Now we are ready to install NodeJS into the Distribution.
I simply followed the description on:

- [Set up your Node.js development environment with WSL 2](https://docs.microsoft.com/en-us/windows/nodejs/setup-on-wsl2)

Here the long story short:
```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
$ nvm install node
$ nvm install --lts
```

In addidion, I installed the Postgress extension:
```bash
$ npm install pg
```

We are now ready to go with the WSL Distribution!

# Docker Container

The next part descips how we run the **postgres** databse in a Docker container.

Docker Desktop for Windows needs to be successfully intalled. [Check the Prerequisites.](#prerequsites)

Short explaination:

Docker is a new modern IT term. There are a lot of information in the Internet about
the posibliries you have by building or using Docker container. In simple words, 
Docker is a technologie that allows you to run microservices as a postgres Database Server
in a minimum invirment. No Operationg system to deploy, as we know it from VMware or HyperV.
The Database runs in a container Framework without any kind of Hypervisor in the background.

> IMPORTENT:
> - Docker Container needs to deployed.
> - They can run in the background.
> - You can stop/start container after deployment.
> - Find 10.000 preconfigured contains at [DockerHUB](http://www.dockerhub.com)
> 
> You should login to [DockerHUB](http://www.dockerhub.com) and create a personal user.
> This is free of chage but opens the [DockerHUB](http://www.dockerhub.com) Repositry with
> all the preconfigured Containers, including Documentation, etc. I highly recommend it.

Here some simple docker commandlines you should know:

```docker image ls```
- list all downloaded images (containers)

```docker container ls -a```
- shows all running/not-running containers

```docker container rm [CONTAINER-ID]```
- delete a container

```docker container stop [CONTAINER-ID]```
- stops a deployed container

```docker container start [CONTAINER-ID]```
- starts a deployed container

```docker container exec -it [CONTAINER-ID] bash```
- starts a command shell to a container (bash) - simular to a SSH connection to a server.

```docker volume ls```
- lists created (persistent) volumes

Let's go to the **postgres** deployment.

## Run Postgres Container

**Settings:**
- Name: siteconnect
- Port: 5432 (listen)
- POSTGRES_USER: siteconnect
- POSTGRES_PASSWORD: siteconnect
- Data Volume (Persitent data): siteconnect_data
- Version: postgres:10

**Command:**
```pws
PS C:\> docker container run -d --name siteconnect -p 5432:5432 -e POSTGRES_USER=siteconnect -e POSTGRES_PASSWORD=siteconnect -v siteconnect_data:/var/lib/postgresql/data postgres:10
```

**Verify:**
```pws
PS C:\> docker container ls
```

```bash
CONTAINER ID   IMAGE         COMMAND                  CREATED       STATUS       PORTS                    NAMES
b8f0874826c6   postgres:10   "docker-entrypoint.s…"   5 hours ago   Up 5 hours   0.0.0.0:5432->5432/tcp   siteconnect
```

The Container runs successfully, If your output of ```docker container ls``` is simual to the one above.

# Database Connect

Before we check the setup with Visual Studio Code, we need to set the Database connection.

Login to the ```siteconnect-ubuntu-18.04``` Distribution and set (export) DATABASE_URL to **.bashrc** (siteconnect user only):
```bash
$ bash -c 'cat << EOF >> ~/.bashrc
GATEWAY_IP=`ip route show | awk '{print $3}' | head -n 1`
export DATABASE_URL=postgresql://siteconnect:siteconnect@$GATEWAY_IP:5432/siteconnect
EOF'
```

> EXPLAINATION:
> Form the ```siteconnect-ubuntu-18.04``` Distribution, the Database (postgres) runs externely.
> This means, we need to point it to the Gateway IP of the WSL envirment. 

Verfy the variable by **exit** the ```siteconnect-ubuntu-18.04``` Distribution and restart it.

Check it with:
```bash
$ echo $DATABASE_URL
```

This shold output: ```postgresql://siteconnect:siteconnect@<YourGatewayIP>:5432/siteconnect```

# Verify

Test (Postgres client):
psql -h `ip route show | awk '{print $3}' | head -n 1` -p 5432 -U siteconnect
--> \l
--> \q

Test NODE code (with Ev. Variable):

```node
const { Pool, Client } = require('pg')
const connectionString = process.env.DATABASE_URL
const pool = new Pool({
  connectionString,
  })
  pool.query('SELECT NOW()', (err, res) => {
    console.log(err, res)
      pool.end()
      })
      const client = new Client({
        connectionString,
})
client.connect()
client.query('SELECT NOW()', (err, res) => {
  console.log(err, res)
    client.end()
    })
```