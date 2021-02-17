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
> 
> I highly suggest reading his Visual Studio Code Guite for Developers: [```VS Code Remote Development```](https://code.visualstudio.com/docs/remote/remote-overview),
> before you move on with the deployment as described below. It gives you a good overview of how it works, and the possibilities
> you get with WSL (Windows Subsystem for Linux) as part of your Development Environment.
> It also contains even more information by talking about Docker Containers, what makes your Development Environment
> more OS agnostic.

# Content:

| File                            | Descriptiom                                                        |
|:--------------------------------|:-------------------------------------------------------------------|
| [```README.md```](README.md)    | This Document                                                      |
| [```INSTALL.md```](INSTALL.md)  | Complete Setup Guide                                               |
| [```TUTORIAL.md```](TUTORIAL.md)| Examples and Tutorials                                             |
| [```LICENSE```](LICENSE)        | [MIT](https://choosealicense.com/licenses/mit/) License agreement  |

## Setup Design

 <p float="left">
  <img src="https://lucid.app/publicSegments/view/74aff30f-a632-4245-b004-4338cb8d9fcc/image.png" width="640" />
</p>

## Overview

- [Install Development Environment](INSTALL.md)
    - [Prerequistes](INSTALL.md#Prerequistes)
    - [Create a work Folder](INSTALL.md#Create-a-work-folder)
    - [Docker Container](INSTALL.md#Docker-Container)
    - [Preparing WSL Ubuntu 18.04 LTS](INSTALL.md#Preparing-WSL-Ubuntu-1804-LTS)
    - [Build a Distribution Template](INSTALL.md#Build-a-Distribution-Template)
    - [Deoploy a Project Distribution](INSTALL.md#Deoploy-a-Project-Distribution)

- [Tutorials and Examples](TUTORIAL.md)
    - **Visual Studio Code**
        - [Starting: Visual Studio Code](TUTORIAL.md#Starting-Visual-Studio-Code)
        - [Full Integration View of WSL in Visual Studio Code](TUTORIAL.md#Full-Integration-View-of-WSL-in-Visual-Studio-Code)
    - **Terminal**
        - [Starting: WSL Distribution (Terminal) in parallel](TUTORIAL.md#Starting-WSL-Distribution-Terminal-in-parallel)
        - [Example: Clone a DevOps Repository](TUTORIAL.md#Example-Clone-a-DevOps-Repository)
    - **Docker Desktop**
        - ```COMING SOON```

- [License](#license)
- [Contact](#contact)

## License

Distributed under the [MIT](https://choosealicense.com/licenses/mit/) License. See `LICENSE` for more information.

## Contact

Project Link: [fls-wsl-siteconnect](https://github.com/code-snipes/fls-wsl-siteconnect)

[Patrick Hayo](mailto:patrick.hayo@flsmidth.com)

[![N00ky2010](https://img.shields.io/twitter/follow/N00ky2010)](https://www.twitter.com/N00ky2010)

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
