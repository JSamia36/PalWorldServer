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

