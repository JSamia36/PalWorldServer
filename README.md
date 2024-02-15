# Creating a dedicated PalWorld server without port forwarding
This will be setup using Debian 12 bookworm and playit.gg on Proxmox

## Recomendations
- Ethernet connection
- at Minimum 16gb of ram (server eats up ram)
- 2 dedicated cores (would recommend more if possible)
- 30gb Storage

## Getting Started
I had significant issues with installing steam on Debian for whatever reason, but I started out by creating a PalWorld directory
```
mkdir PalWorld && cd PalWorld
```
Obviously you can name it whatever you'd like but this makes the most sense to me. We will be following the manual install instructions from [here](https://developer.valvesoftware.com/wiki/SteamCMD#Linux)
```
sudo apt-get install lib32gcc-s1
```
We will be ignoring switching to the steam user and creating the steam folder as I am strictly just running a palworld server and have no other current usage for Steam.
```
curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
```
If we run a simple 'ls' we will notice steamcmd.sh is now in our folder, typing `steamcmd` should get it to install it and you'll notice instead of user@debian its showing as Steam. This means everything so far has been done correctly. From here we will move on back to the [PalWorld instructions](https://tech.palworldgame.com/getting-started/deploy-dedicated-server/).

