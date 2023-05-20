# qnapJellyfin
easy to access tutorial on how to install [Jellyfin](https://jellyfin.org) on most 5.0 [QNAP](https://www.qnap.com) systems (made for myself so I don't need to traverse half of the internet again but could be useful for others).


## Pre-requisites 
* Any QNAP system on ver 5.0+. For some models, you may need to opt-in to beta to access ver 5.0+, although you can get Jellyfin working on any 4.x. 

## Method
1. Open **App Center** and install **Container Station**.
2. While/after that installs, make a new shared folder at the root level of the drive you want Jellyfin on. This can be done via **File Station**. Call it something cool, like *Jellyfin* or something. 
3. Make a new user with read and write permission to the new shared folder you made. This can be done via **Control Panel** --> **Privilege** --> **Users**. Ensure they have read and write permissions as mentioned prior! Name it something cool, like *Docker* or something.
4. While you're in **Control Panel**, head to **Network and File services** --> **Telnet / SSH**.
5. SSH into your QNAP system - the easiest way on Windows is [PuTTY](https://www.putty.org). To SSH with PuTTY, just enter the IP of the QNAP system (LAN) into it, and enter the admin details. 
6. Enter "*username* id", where *username* is the new user you just made. No quotes too! You should receive a "PGID" and a "PUID". Note these down. You can close the SSH connection now if you'd like.
7. 
