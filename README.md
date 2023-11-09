# INSTALL AVAIL FULL NODE
## INSTALL AVAIL NODE

***
**THE FIRST STEP IS TO BUY A  VPS**
```
Minimum	/ Recommended
RAM: 4GB/8GB
CPU (amd64/x86 architecture):2 core/4 core
Storage (SSD):20-40 GB/200-300 GB.
I would suggest go with recommended specifications for smooth installation.
Make sure you have UBUNTU 22.0 selected for buying vps,as other versions have some issues.
```
**INSTALLING RUST**
```
Copy paste this code one by one in ur terminal.
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

**NOW,run the Avail Node using the following command:(V 1.8.0.01)/GOLDBERG**
```
git clone https://github.com/availproject/avail.git
cd avail
mkdir -p output
mkdir -p data
git checkout v1.8.0.0
cargo run --locked --release -- --chain goldberg -d ./output
```
**This will compile and run node connected to goldberg network(wait for about 45 mins for the process to complete)**
```
2023-10-11 16:11:31 Avail Node    
2023-10-11 16:11:31 ✌️  version 1.7.0-ad024ff050e    
2023-10-11 16:11:31 ❤️  by rerrts, 2017-2023    
2023-10-11 16:11:31 📋 Chain specification: Avail goldberg Testnet    
2023-10-11 16:11:31 🏷  Node name: drifter    
2023-10-11 16:11:31 👤 Role: FULL    
2023-10-11 16:11:31 💾 Database: RocksDb at /tmp/substrateJwM8xd/chains/Avail Testnet_116d7474-0481-11ee-bc2a-7bfc086be54e/db/full    
2023-10-11 16:11:32 🔨 Initializing Genesis block/state (state: 0x6bc8…8ac6, header-hash: 0xd120…50c6)    
2023-10-11 16:11:32 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2023-10-11 16:11:33 👶 Creating empty BABE epoch changes on what appears to be first startup.    
2023-10-11 16:11:33 🏷  Local node identity is: 12D3KooWMmY2QLodvBGSiP1Cg9ysWrPSMN19qK3w35mRnUhq6pMX    
2023-10-11 16:11:33 Prometheus metrics extended with avail metrics    
2023-10-11 16:11:33 💻 Operating system: linux    
2023-10-11 16:11:33 💻 CPU architecture: x86_64    
2023-10-11 16:11:33 💻 Target environment: gnu    
2023-10-11 16:11:33 💻 CPU: 13th Gen Intel(R) Core(TM) i7-13700K
```
**Now,create systemd**
```
touch /etc/systemd/system/availd.service
nano /etc/systemd/system/availd.service
```
**Make sure you change your validator name**
```
[Unit] 
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart= /root/avail/target/release/data-avail --base-path `pwd`/data --chain goldberg --name "alxx14"
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target
```

**Save it by inputting ctrl+X**
```
systemctl enable availd.service
systemctl start availd.service
systemctl status availd.service
Tail the logs with:journalctl -f -u availd
Check your node on https://telemetry.avail.tools/
..........................................................







