# Node.JS Developer Environment

> Building a solid developer environment with NodeJS in a WSL Distribution 
> and a Connection to a Database Server, running in a Container.
>
> - **Project:** ```SiteConnect```
> - **Elements:** Postgres DB, Node.JS, Visual Studio Code, DBeaver
> - **Engine:** Docker, Windows Subsystem for Linux (WSL)

## Setup Design

![Setup](https://lucid.app/publicSegments/view/74aff30f-a632-4245-b004-4338cb8d9fcc/image.png)

## Depoyment Steps

- [Prerequistes](README.md#Prerequistes)
- [Create a work Folder](README.md#Create-a-work-folder)
- [Docker Container](README.md#Docker-Container)
    - [Some Explainations](README.md#Some-Explainations)
    - [Run the Postgres container](README.md#Run-the-Postgres-container)
    - [Verify with DBeaver](README.md#Verify-with-DBeaver)
- [Preparing WSL Ubuntu 18.04 LTS](README.md#Preparing-WSL-Ubuntu-1804-LTS)
- [Build a Distribution Template](README.md#Build-a-Distribution-Template)
    - [Export the Template](README.md#Export-the-Template)
    - [Deploy your Distribution](README.md#Deploy-your-Distribution)
    - [Customize your Distribution](README.md#Customize-your-Distribution)
- [Deoploy a Project Distribution](README.md#Deoploy-a-Project-Distribution)
    - [Customize the Distribution](README.md#Customize-the-Distribution)
    - [Generate SSH Key](README.md#Generate-SSH-Key)
    - [Create ./ssh/config](README.md#Create-sshconfig)
    - [Create /etc/wsl.conf](README.md#ate-etcwslconf)
    - [Set up Node.JS](README.md#Set-up-NodeJS)
    - [Postrgres Database Connect](README.md#Postgres-Database-Connect)

## Tutorial

 - Visual Studio Code
    - [Starting: Visual Studio Code](INTEGRATION.md#Starting-Visual-Studio-Code)
        - [Open a new VSC Window with the WSL Distribution](INTEGRATION.md#Open-a-new-VSC-Window-with-the-WSL-Distribution)
        - [Select siteconnect-ubuntu-18.04 Distribution](INTEGRATION.md#Select-siteconnect-ubuntu-18-04-Distribution)
        - [Adding helpful Extentions to Visual Studio Code](INTEGRATION.md#Adding-helpful-Extentions-to-Visual-Studio-Code)
        - [Open a folder (/home/siteconnect) in the Remote Session](INTEGRATION.md#Open-a-folder-homesiteconnect-in-the-Remote-Session)
    - [Full Integration View of WSL in Visual Studio Code](INTEGRATION.md#Full-Integration-View-of-WSL-in-Visual-Studio-Code)

- Terminal
    - [Starting: WSL Distribution (Terminal) in parallel](INTEGRATION.md#Starting-WSL-Distribution-Terminal-in-parallel)