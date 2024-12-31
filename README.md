# Creating a dedicated PalWorld server without port forwarding
This will be setup using Debian 12 bookworm and playit.gg on Proxmox

## Recomendations
- Ethernet connection
- at Minimum 16gb of ram (server eats up ram - this might be fixed now)
- 2 dedicated cores (would recommend more if possible)
- 30gb Storage

## Getting Started
I had significant issues with installing steam on Debian for whatever reason, but I started out by creating a PalWorld directory. 
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
## PalWorld server install
If we run a simple 'ls' we will notice steamcmd.sh is now in our folder, typing `steamcmd` should get it to install it and you'll notice instead of user@debian its showing as Steam. This means everything so far has been done correctly. From here we will move on back to the [PalWorld instructions](https://tech.palworldgame.com/getting-started/deploy-dedicated-server/).

The instructions have you run it all as one command but I prefer to run seperately so for the sake of this that's what we will do, in the Steam terminal paste:
```
login anonymous
```
This is just logging in as anonymous user so we don't have to sign into our steam or create a new one just for this. We then want to get the files for the server 
```
app_update 2394010 validate
```
Just let this download and run its course, it could take a bit depending on how good of internet you have. That's all we need to do in the Steam terimnal so we can close that out with `exit` We pretty much have it installed now and can run it with ./PalServer.sh but this would only allow people to connect locally.

### Update
I ran through this 12/31/24 and found that the PalWorld server file was no longer saved in the created directory, instead it was found under ```/home/{username}/.local/share/Steam/steamapps/common/PalServer```

## Creating a tunnel
Unfortunately Cloudflare doesn't allow you to do so without port forwarding but luckily there is an alternative way, we will be using the website [playit.gg](playit.gg). This is really easy to install, we just follow the script they have under their 'download' tab.
```
curl -SsL https://playit-cloud.github.io/ppa/key.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/playit.gpg >/dev/null
echo "deb [signed-by=/etc/apt/trusted.gpg.d/playit.gpg] https://playit-cloud.github.io/ppa/data ./" | sudo tee /etc/apt/sources.list.d/playit-cloud.list
sudo apt update
sudo apt install playit
```
If everything went well, we just have to run it now and get the IP address off of the website in order to connect. You do have to create an account and verify your email if you haven't done so already. In order to run this navigate to /usr/local/bin and here you should see "playit" to run just type `./playit` it then checks if the key is valid and will create the tunnel. Please make sure on the website that you have the IP address set to the LOCAL address, in my case 10.0.0.179:8211. On default PalWorld servers are setup at port 8211 unless you change that.

## Updating PalWorld server settings
You must first launch your server before configing, meaning you can launch then shut-down if you desire. In your Palworld server we created in the Getting Started phase, we will navigate to `Pal/Saved/Config/LinuxServer`. In this folder we are just looking for PalWorldSettings.ini, you will notice this is empty so we have to copy the contents of DefaultPalWorldSettings.ini over, you can do so with the command 
```
cp DefaultPalWorldSettings.ini /Pal/Saved/Config/LinuxServer
```
We then need to rename it
```
mv DefaultPalWorldSettings.ini PalWorldSettings.ini
```
It should have content now, we are able to edit using `nano` just make sure to restart your server for changes to take place. If you need to search for something specific use `ctrl+W`

## Additional Commands
When running your palworld server you can now run additional arguements such as 
```
./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS -players=10
```
You may also want to keep note of the command list, it can be found on their [website](https://tech.palworldgame.com/settings-and-operation/commands)
