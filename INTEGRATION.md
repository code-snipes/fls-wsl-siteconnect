# Working with the deployment

After we acombished the installation / deployment of the Develpment evirment, desciped before.
We are now ready to see how to integrate it in ```Visual Studio Code```and work with all
the parts of the deployment.

- Visual Studio Code
    - [Starting: Visual Studio Code](#Starting-Visual-Studio-Code)
        - [Open a new VSC Window with the WSL Distribution](#Open-a-new-VSC-Window-with-the-WSL-Distribution)
        - [Select siteconnect-ubuntu-18.04 Distribution](#Select-siteconnect-ubuntu-18-04-Distribution)
- Windows Linux Subsystem (WSL)
- Terminal
- Docker Desktop

# Starting: Visual Studio Code

Simply start ```Visual Studio Code``` on your Computer.

![Open-VSC](images/vsc-001.png)

> **COMMENT:** You maybe will get a message, that ```Visual Studio Code``` realized
> ```WSL``` installed on your computer during the start. It will ask you to intall the integration.
> You need to say ```OK``` if this shows up to go ahed with installing this integration.
> This happens usualy during the first starto of ```Visual Studio Code``` after **WSL** got installed
> Allowing to install this integration is essential for all following steps to have this installed.

[BACK](#Working-with-the-deployment)

## Open a new VSC Window with the WSL Distribution

After you opend ```Visual Studio Code``` you might already realized the new green button
in the left down corner of you ```Visual Studio Code``` window. This is you starting point
of accessing/attaching your ```WSL``` Distribution to ```Visual Studio Code```.

![Open-VSC](images/vsc-002.png)

Simply chlick on it and you will get the posibilty to start a new ```Visual Studio Code```
Window into the ```WSL``` Distribution:

![Open-VSC](images/vsc-003.png)

Select ```Remote-WSL: New Window using Distrio...``` to go ahead.

[BACK](#Working-with-the-deployment)

## Select siteconnect-ubuntu-18.04 Distribution

Now, selet your created ```siteconnect-ubuntu-18.04``` and open it.

![Open-VSC](images/vsc-004.png)

If the connection process ran successfully, you will realize, the
statusbar of ```Visual Studio Code``` will change again. It shows
you the connection in the down left corner, like this:

![Open-VSC](images/vsc-005.png)

[BACK](#Working-with-the-deployment)

## Adding Extentions to VSC

<p float="left">
  <img src="images/wsl_vsc_extentions_installed.png" width="300" />
</p>

## Open a folder (/home/siteconnect)

<p float="left">
  <img src="images/vsc_open_home_folder_siteconnect.png" width="640" />
</p>

## After starting VSC with installed VSC extentions

<p float="left">
  <img src="images/vsc_open_home_with_terminal.png" width="640" />
</p>

# Starting: WSL Distribution in Terminal in parallel

<p float="left">
  <img src="images/wsl_access_siteconnect-ubutu-18.04.png" width="640" />
</p>