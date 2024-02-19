# guide-massa-node-step-by-step
If you follow this guide, you will be able to independently run and monitor your own Massa node:


I will use Ubuntu for this guide, you need Ubuntu 20.04 and higher and a computer with 8 cores, 16 GB RAM, 1TB disk and a decent internet connection. On your local machine or you can also use a cloud VPS (Virtual Private Servers) like Contabo, AWS, Hetzner...

Now your computer/vps is ready, we are going to update/upgrade the apt command :

```bash
sudo apt update && sudo apt upgrade -y
```
Install all of needed libraries in one command : 

```
sudo apt install pkg-config curl git build-essential libssl-dev libclang-dev cmake screen -y
```
