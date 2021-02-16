# Development Environment

> After successfull ran to all the Deployment Steps below, you will find a Tutorial about
> the integration of all the services into Visual Studio Code, including
> some examples of how to use the created Development Environment.
>
> Follow the folloing link to the Tutorial Document: 
> [```Working with the deployment```](TUTORIAL.md)

- [Prerequistes](#Prerequistes)
- [Create a work Folder](#Create-a-work-folder)
- [Docker Container](#Docker-Container)
    - [Some Explainations](#Some-Explainations)
    - [Run the Postgres container](#Run-the-Postgres-container)
    - [Verify with DBeaver](#Verify-with-DBeaver)
- [Preparing WSL Ubuntu 18.04 LTS](#Preparing-WSL-Ubuntu-1804-LTS)
- [Build a Distribution Template](#Build-a-Distribution-Template)
    - [Export the Template](#Export-the-Template)
    - [Deploy your Distribution](#Deploy-your-Distribution)
    - [Customize your Distribution](#Customize-your-Distribution)
- [Deoploy a Project Distribution](#Deoploy-a-Project-Distribution)
    - [Customize the Distribution](#Customize-the-Distribution)
    - [Generate SSH Key](#Generate-SSH-Key)
    - [Create ./ssh/config](#Create-sshconfig)
    - [Create /etc/wsl.conf](#Create-etcwslconf)
    - [Set up Node.JS](#Set-up-NodeJS)
    - [Postrgres Database Connect](#Postgres-Database-Connect)

[BACK to the ```README```](README.md)

# Prerequistes

All the following applications need installation on your Developer PC before you begin.
If you do a fresh installation, use all the defaults during the installation.
Follow the Installation Guides of each Application.

- [```Windows Subsystem for Linux```](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- [```Windows Terminal```](https://docs.microsoft.com/en-us/windows/terminal/get-started)
- [```Ubuntu 18.04 LTS```](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
- [```Docker Desktop on Windows```](https://docs.docker.com/docker-for-windows/install/)
- [```DBeaver Community Version```](https://dbeaver.io)
- [```Visual Studio Code```](https://code.visualstudio.com/download)

- [```PowerShell```](https://www.digitalcitizen.life/ways-launch-powershell-windows-admin/) command promt.
    - Use the [```Windows Terminal```](https://docs.microsoft.com/en-us/windows/terminal/get-started), which is on the prerequisite list.

Further explanation integrates each of the applications into the Development Environment.

[BACK](#Deployment-Steps)

# Create a work Folder

Create the following folder on your C Drive:
```bach
C:\Distributions
```

It will be the place to save modifications.

[BACK](#Deployment-Steps)

# Docker Container

There is a lot of information about Docker on the Internet. How you use, build, 
and run Docker containers. Docker Container is a technology that allows you to run microservices, as an example, a Postgres Database Server in a minimum, light, and customized environment. No Operating system to deploy, as we know it from VMware or HyperV.
The Database runs in a container Framework without any Hypervisor in the background.

> !!!! IMPORTANT !!!!
>
> - Containers getting deployed.
> - They can run in the background.
> - You can stop/start container after deployment.
> - Find 10.000 preconfigured contains at [DockerHUB](http://www.dockerhub.com)
> 
> I highly recommend registering an account at [DockerHUB](http://www.dockerhub.com).
> This is free of charge and opens you the [DockerHUB](http://www.dockerhub.com) Repository with
> all the preconfigured Containers, including Documentation, etc.

## Some Explanations

If you are not familiar with **Docker**, here some commands, you should know.
Find a detailed description at https://docs.docker.com

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
- starts a command shell to a container (bash) - similar to an SSH connection to a server.

```docker volume ls```
- lists created (persistent) volumes

Let's go to the **Postgres** deployment.

[BACK](#Deployment-Steps)

## Run the Postgres container

Find a detailed description of the ```Postgres Docker Container``` on https://hub.docker.com/_/postgres

**Settings:**
- Name: siteconnect
- Port: 5432 (listen)
- POSTGRES_USER: siteconnect
- POSTGRES_PASSWORD: siteconnect
- Data Volume (Persitent data): siteconnect_data
- Version: postgres:10

**Command:**
```pws
PS C:\> docker container run `
 --detach `
 --restart unless-stopped `
 --name siteconnect `
 --publish 5432:5432 `
 --env POSTGRES_USER=siteconnect `
 --env POSTGRES_PASSWORD=siteconnect `
 --volume siteconnect_data:/var/lib/postgresql/data `
 postgres:10
```

> COMMENT: The parameter: ```--restart unless-stopped``` forces the Container to continue if it crashes.
> But it will the Container not restart if you, for example, reboot your PC. If you like
> the Container always running, even after a reboot, set the parameter to: ```--restart always``` 

> COMMENT: The start of the container will also create a **siteconnect** database and user.
> The two parameters ```--env POSTGRES_USER=siteconnect``` and ```--env POSTGRES_PASSWORD=siteconnect``` taking 
> care of the creation. You don't need to create this manually (DBeaver).

**Verify:**
```pws
PS C:\> docker container ls
```

```bash
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
b8f0874826c6 postgres:10 "docker-entrypoint.s…" 5 hours ago Up 5 hours 0.0.0.0:5432->5432/tcp siteconnect
```

The Container runs successfully If your Output of ```docker container ls``` is similar to the one above.

[BACK](#Deployment-Steps)

## Verify with DBeaver

> CONTENT MISSING - STILL IN WORK !!!!

[BACK](#Deployment-Steps)

# Preparing WSL Ubuntu 18.04 LTS

As a kind of **Best-Praxis** we will clone the ```Ubuntu 18.04 LTS``` distribution
and do the customization in our project distribution (siteconnect).

Start Ubuntu 18.04 LTS and use the following username/password combination.
Feel free to change the password on your own choice. Keep in mind you maybe
need this password at a later point. Please write it down or save it in a secured place.

```
Username: ubuntu
Password: ubuntu
````

After the initial start of Ubuntu and finalizing the configuration, you can go-ahead 
and set the user ```ubuntu``` in a special **sudo** status.
This avoids the password question, if you execute commands that nedds **root** permissions.
```bash
$ sudo bash -c "echo 'ubuntu ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/ubuntu"
```

The next step is to install the following packages:
```bash
$ sudo apt-get update
$ sudo apt-get install -y vim curl git tree wget postgresql-client
```

Feel free to add more packages of your choice if you think it makes sense to have them in your template.

After the installation, **exit** the Distribution by typing ```exit``` at the command prompt.

[BACK](#Deployment-Steps)

# Build a Distribution Template

The best praxis is always to build a dedicated Distribution for your project.
The advantage is, you can specifically customize the Distribution with
the project's requirements. SSH Keys, Packages, Connections, etc.

Find the necessary steps for the ```siteconnect``` project below.

[BACK](#Deployment-Steps)

## Export the Template

This step will create a template for the final **Project Distribution**.
All commands need to get applied in a **PowerShell** command shell.

```pws
PS C:\> wsl.exe --export Ubuntu-18.04 C:\Distributions\ubuntu-18.04-template.tar
```

> EXPLAINATION: The command exports the ```Ubuntu 18.04 LTS``` Distribution into a 
> TAR file and saves it in ```C:\Distributions\ubuntu-18.04-template.tar```.
> We will use this exported Distribution in below steps.

[BACK](#Deployment-Steps)

# Deoploy a Project Distribution

Now we can create our ```Project Distribution```

It creates a clone of the exported Template of the last [step](#export)
```pws
PS C:\> wsl.exe --import siteconnect-ubuntu-18.04 C:\Distributions\siteconnect-ubuntu-18.04 C:\Distributions\ubuntu-18.04-template.tar
```

Making our life easy, let's set the ```Project Distribution``` as default.
```pws
PS C:\> wsl.exe --set-default siteconnect-ubuntu-18.04
```

You can check the success by typing:
```pws
PS C:\> wsl.exe --list --verbose
```

The Output of this command should show you something like:
```bash
NAME STATE VERSION
* siteconnect-ubuntu-18.04 Running 2
 docker-desktop-data Running 2
 Ubuntu-18.04 Stopped 2
 docker-desktop Running 2
```

The ```*``` made ```siteconnect-ubuntu-18.04``` Distribution as the default.

[BACK](#Deployment-Steps)

## Customize the Distribution

Now we will start the newly created ```siteconnect-ubuntu-18.04```Distribution the first time.
```pws
PS C:\> wsl.exe --user ubuntu
```

After a successfull start and login we will go ahead by creating a new Linux user: **siteconnect** with the same
special **sudo** settings as we did with the **ubuntu** user before.

```bash
$ sudo groupadd -r siteconnect
$ sudo useradd -m -r -g siteconnect -d /home/siteconnect -s /bin/bash -c "SiteConnect User Account" siteconnect
$ sudo usermod -aG sudo siteconnect
$ sudo bash -c "echo 'siteconnect ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/siteconnect"
```

If the commands ran successfully, you need to ```exit``` the Distribution and restart/login with the **siteconnect** user.

```pws
PS C:\> wsl.exe --user siteconnect
```

> !!!! IMPORTANT !!!!
>
> Be sure, you are in the linux-home-directory of the user **siteconnect**.
> Test it by typing ```pwd```. Your Output should look like: ```/home/siteconnect```.
> If the Output shows another folder, use ```cd``` to jump into user's **siteconnect**** Linux-home-directory.
> Be sure you are in the correct folder before you go ahead.

[BACK](#Deployment-Steps)

## Generate SSH Key

We always need an SSH key to authenticate on various services.
GitHub, Azure DevOps, login to another host on SSH, etc.
Therefore, we will create a new SSH key for the user **siteconnect** and
store it in ```~/.ssh/config``` folder.

During the creation, you will get asked about setting a password for the SSH Key.
I always recommend the highest possible protection but in the real world,
especially by automated processes, and SSH Key without the password is handier than with a Key Password.

```bash
$ ssh-keygen -t rsa -b 4096 -C "siteconnect"
```

Alternatively, you can also use an already created SSH key
if you have one you usually use. Feel free and copy this key for the
user **siteconnect**

[BACK](#Deployment-Steps)

## Create ./ssh/config

It is also helpful to use the **ssh-agent** to forward the private key
if you do a "chain-login" to another host on SSH. Let's create a config file
and add your SSH key.

```bash
$ bash -c 'cat << EOF > ~/.ssh/config
Host *
 ForwardAgent yes
 IdentityFile ~/.ssh/id_rsa
EOF'
```

Using the ```-A``` option to forward the key to another SSH session,
you need to enable the **ssh-agent** every time before you do the SSH login.
Here an example of how to enable it:

```bash
eval "$(ssh-agent -s)"
```

[BACK](#Deployment-Steps)

## Create /etc/wsl.conf

Finalizing the Distribution, we should create a **wsl.conf** file.
Here we can set defaults of the Distribution.

Find detailed information about the possibilities here:
- [WSL commands and launch configurations](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)

```bash
$ sudo bash -c 'cat << EOF > /etc/wsl.conf
[network]
generateHosts = true
generateResolvConf = true
[user]
default=siteconnect
EOF'
```

After applying, ```exit``` the Distribution and ```terminate``` it with the following command:
```pws
PS C:\> wsl.exe --terminate siteconnect-ubuntu-18.04
```

> !!!! IMPORTANT !!!!
>
> If you change/add settings to the config file **/etc/wsl.conf**, the Distribution needs to get
> **terminated** after ```exit```. Termination does a complete shutdown of the WSL Distribution. If you reconnect 
> to it, it is like after a reboot. The settings in the configuration file get applied by this reboot.

Restart the ```siteconnect-ubuntu-18.04``` Distribution by type:
```pws
PS C:\> wsl.exe
```

You might realize, the login user is now **siteconnect**.
We achieved this by setting the default username to **siteconnect**.

[BACK](#Deployment-Steps)

## Set up Node.JS

Now we are ready to install NodeJS into the Distribution.
I followed the description on:

- [Set up your Node.js development environment with WSL 2](https://docs.microsoft.com/en-us/windows/nodejs/setup-on-wsl2)

Here the long story short:
```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

Finish the installation by ```exit``` the ```siteconnect-ubuntu-18.04``` Distribution and restart it.

```bash
$ nvm install node
$ nvm install --lts
$ nvm install 10.5.0
```

You finisehd the installation of ```Node.JS``` in your WSL Distribution.

[BACK](#Deployment-Steps)

## Postgres Database Connect

Before we check the setup with Visual Studio Code, we need to set the Database connection.

Login to the ```siteconnect-ubuntu-18.04``` Distribution and set (export) **DATABASE_URL** in **.bashrc** (siteconnect user only):
```bash
$ cat << EOF >> ~/.bashrc
export DATABASE_URL=postgresql://siteconnect:siteconnect@localhost:5432/siteconnect
EOF
$ bash
```

> EXPLAINATION:
> Form the ```siteconnect-ubuntu-18.04``` Distribution, the Database (postgres) runs externely
> but on the same host (your PC). Connecting to the DB, we set the database server to ```localhost```
> and adding **DATABASE_URL** to the **.bashrc** keeps it persistent.

Verify the variable by ```exit``` the ```siteconnect-ubuntu-18.04``` Distribution and restart it.

Check it with:
```bash
$ echo $DATABASE_URL
```

This shold output: ```postgresql://siteconnect:siteconnect@localhost:5432/siteconnect```

You can check your success by testing the database connection.

Login/Start your ```siteconnect-ubuntu-18.04``` Distribution and try the following
connections to the Postgress Database Server, running in the Docker Container.

**With the native Postgress client:**

```bash
$ psql -h localhost -p 5432 -U siteconnect
```

**With a smiple connection script (Node.JS) including the ```DATABASE_URL``` Variable:**

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

Both Tests should run successfully. If you face issues, check if the Container is still running,
with:

 ```docker container ls```

[BACK](#Deployment-Steps)