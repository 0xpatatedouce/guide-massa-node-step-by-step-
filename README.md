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
let's install rust :

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

![Capture d’écran 2024-02-20 200824](https://github.com/0xpatatedouce/guide-massa-node-step-by-step-/assets/123324096/c793a87b-163e-4354-a197-d337ab7702fc)

Rust is installed now configure path:
```
source $HOME/.cargo/env
```

![Capture d’écran 2024-02-20 200859](https://github.com/0xpatatedouce/guide-massa-node-step-by-step-/assets/123324096/e7b571cd-f286-45fc-901a-abf6eb430841)

Install rust stable version: 
```
rustup toolchain install 1.74.1
```
```
rustup default 1.74.1
```

Let's install the node via cloning Massa repo from GitHub:
```
git clone https://github.com/massalabs/massa.git
```

Now your node is installed, go to the cloned repository and checkout the latest tag:
```
cd massa
```
```
git checkout MAIN.2.1
```
In this step, we will enter your IP address into the node and open the ports so that the node can communicate with other nodes:

Firstly enter your IP address with this command :
```
cd massa-node/config
```                                                                              
```
nano config.toml
```
```
Replace the letter "AAA.BBB.CCC.DDD" with your address IP : 
[protocol]
routable_ip = "AAA.BBB.CCC.DDD"
```
![massa ip](https://github.com/0xpatatedouce/guide-massa-node-step-by-step-/assets/123324096/538cddcd-5f87-4027-8d86-7492d003929b)

```
apt install ufw -y 
ufw allow ssh 
ufw allow https 
ufw allow http 
ufw allow 31244
ufw allow 31245
ufw enable
```
```
cd $home
```
```
cd massa/massa-node/
```
```
screen -S massa_node
```
```
RUST_BACKTRACE=full cargo run --release -- -p <PASSWORD> |& tee logs.txt
```
![Capture d’écran 2024-02-20 201502](https://github.com/0xpatatedouce/guide-massa-node-step-by-step-/assets/123324096/1887581e-4893-43bd-b7f3-260aa64e9765)

```
cd $home
```
```
cd massa/massa-client/
```
```
screen -S massa_client
```
```
cargo run --release -- -p <PASSWORD>
```

![Capture d’écran 2024-02-20 201758](https://github.com/0xpatatedouce/guide-massa-node-step-by-step-/assets/123324096/7c714251-3b6c-40e3-b839-219913ac4547)

```
wallet_generate_secret_key
```
```
wallet_info
```
```
buy_rolls <address> <roll count> <fee>
```
```
node_start_staking <your_address>
```
```
git fetch
```
```
git checkout MAIN.2.1
```
https://github.com/massalabs/massa/wiki/Monitoring-scripts-and-commands

https://medium.com/@securisas/security-best-practices-si-vous-lancez-un-node-validateur-99f44b520f84

https://github.com/dex2code/massa_acheta?tab=readme-ov-file
