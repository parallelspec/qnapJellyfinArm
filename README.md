# qnapJellyfin

I no longer use Jellyfin/host local media in general, so I won't be able to provide support and will check for any comments/issues on a very periodic basis. Feel free to use this in your own guide/website/post. Thanks y'all

Not sure if anyone reads this but I've recently changed my setup process for Jellyfin such that the port remains consistent (8096 by default), making it a lot easier for static address things (Tailscale, Duck DNS etc.) I'll revisit this in some time but the steps are pretty much the same. Just either edit your docker compose yaml with the correct ports and PGID and GIDs and it'll stay that port even after restarts/shutdowns.


easy to access tutorial on how to install [Jellyfin](https://jellyfin.org) on most 5.0 [QNAP](https://www.qnap.com) systems (made for myself so I don't need to traverse half of the internet again but could be useful for others). 

We will use the [linuxserver/jellyfin 10.8.13](https://hub.docker.com/layers/linuxserver/jellyfin/10.8.13/images/sha256-6a0f9c6f092557e34d9fad158e72e0980574a8e2caddb033bf3afcc96f67dc07) release. This is the last Jellyfin release which supports ARM QNAP devices, as QNAP has not updated the Linux kernel on these devices in a minute (thanks IonCharge for the headsup).

This is targeted towards ARM CPU QNAP devices, since the Intel models can simply use [Jellyfin for QNAP](https://github.com/pdulvp/jellyfin-qnap). We are using [Docker](https://hub.docker.com) via Container Station in this tutorial.

FULL DISCLAIMER - please backup your media and metadata etc.


## Pre-requisites 
* Any QNAP system on ver 5.0+. For some models, you may need to opt-in to beta to access ver 5.0+, although you can get Jellyfin working on any 4.x. 
* Any method of SSH'ing into the QNAP system - if you're on/using Windows, then [PuTTY](https://www.putty.org) might be your best bet here. Any method works though!

## Method
1. Open **App Center** and install **Container Station**.
2. While/after that installs, make a new shared folder at the root level of the drive you want Jellyfin on. This can be done via **File Station**. Call it something cool, like *Jellyfin* or something. 
3. In that new folder, create **Config**, **Cache**, and **Media** folders. Doesn't need to be shared, just a regular folder will work.
4. Make a new user with read and write permission to the new shared folder you made. This can be done via **Control Panel** --> **Privilege** --> **Users**. Ensure they have read and write permissions as mentioned prior! Name it something cool, like *Docker* or something.
5. While you're in **Control Panel**, head to **Network and File services** --> **Telnet / SSH**. Enable SSH.
6. SSH into your QNAP system - the easiest way on Windows is [PuTTY](https://www.putty.org). To SSH with PuTTY, just enter the IP of the QNAP system (LAN) into it, and enter the admin details. 
7. Enter "*username* id", where *username* is the new user you just made. No quotes too! You should receive a "PGID" and a "PUID". Note these down. You can close the SSH connection now if you'd like.
8. Open **Container Station**, and click on **Containers** on the left. 
9. Click on **+ Create** in the top right. A pop-up window will appear. Ideally, you will see three steps: **Select Image**, **Configure Container**, and **Summary**.
10. Make sure the **Registry** is **Docker Hub**. For **Image**, type **linuxserver/jellyfin**. Click **Next**.
11. Leave everything default, but click on **Advanced Settings**, then click on **Environment**. Add a new variable, with the name **PGID**, and the value that you wrote down in step 7. Repeat for **PUID** too. 
12. Click on **Storage**, then remove the default storage options. Click on the arrow next to **Add Volume**, and choose **Bind Mount Host Path**. 
13. Click on the folder button to the right of **Host**. Navigate to your **Config** folder. For **Container**, type */config*. Repeat this step and step 12 for **Cache** and **Media**. 
14. For **Media**, I'd suggest leaving it as **RO** (read-only). The other two folders should always be **RW** (read & write).
15. Click **Apply** when done and continue with the installation. When it's done, it'll run automatically. 
16. Click on the Jellyfin container. Under **Details**, click on the **Port forwarding** number. You have will the link needed to access the web-gui of Jellyfin. 
17. Paste that link in the new tab. Congrats!!! You're done! The setup is pretty simple from here, just make sure you put your media files in */media* in your NAS. 

Make sure you disable SSH connections once your complete.

### To-do list
* Learn how setup a VPN for remote connections outside of local network 
* Probably learn how to format better in markdown
* Need to learn more about port forwarding, in particular - keeping a constant port so it doesn't change everytime we restart the server
