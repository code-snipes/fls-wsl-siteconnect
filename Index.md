# Node.JS Developer Environment

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

> Building a solid developer environment with NodeJS in a WSL Distribution 
> and a Connection to a Database Server, running in a Container.
>
> - **Project:** ```SiteConnect```
> - **Elements:** Postgres DB, Node.JS, Visual Studio Code, DBeaver
> - **Engine:** Docker, Windows Subsystem for Linux (WSL)

## Setup Design

![Setup](https://lucid.app/publicSegments/view/74aff30f-a632-4245-b004-4338cb8d9fcc/image.png)

## Overview

- [Development Environment](#README.md)
    - [Prerequistes](README.md#Prerequistes)
    - [Create a work Folder](README.md#Create-a-work-folder)
    - [Docker Container](README.md#Docker-Container)
    - [Preparing WSL Ubuntu 18.04 LTS](README.md#Preparing-WSL-Ubuntu-1804-LTS)
    - [Build a Distribution Template](README.md#Build-a-Distribution-Template)
    - [Deoploy a Project Distribution](README.md#Deoploy-a-Project-Distribution)

- [Tutorials](#INTEGRATION.md)
    - Visual Studio Code
        - [Starting: Visual Studio Code](INTEGRATION.md#Starting-Visual-Studio-Code)
        - [Full Integration View of WSL in Visual Studio Code](INTEGRATION.md#Full-Integration-View-of-WSL-in-Visual-Studio-Code)
    - Terminal
        - [Starting: WSL Distribution (Terminal) in parallel](INTEGRATION.md#Starting-WSL-Distribution-Terminal-in-parallel)

<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/code-snipes/fls-wsl-siteconnect.svg?style=flat-square
[contributors-url]: https://github.com/code-snipes/fls-wsl-siteconnect/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/code-snipes/fls-wsl-siteconnect.svg?style=flat-square
[forks-url]: https://github.com/code-snipes/fls-wsl-siteconnect/network/members
[stars-shield]: https://img.shields.io/github/stars/code-snipes/fls-wsl-siteconnect.svg?style=flat-square
[stars-url]: https://github.com/code-snipes/fls-wsl-siteconnect/stargazers
[issues-shield]: https://img.shields.io/github/issues/code-snipes/fls-wsl-siteconnect.svg?style=flat-square
[issues-url]: https://github.com/code-snipes/fls-wsl-siteconnect/issues
[license-shield]: https://img.shields.io/github/license/code-snipes/fls-wsl-siteconnect.svg?style=flat-square
[license-url]: https://github.com/code-snipes/fls-wsl-siteconnect/blob/master/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/patrickhayo/?locale=en_US
