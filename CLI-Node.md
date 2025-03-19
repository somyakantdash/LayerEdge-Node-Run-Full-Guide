# CLI Node Run Full Guide (PC and VPS for Both)

### Offical Docs Guide - https://docs.layeredge.io/introduction/developer-guide/run-a-node/light-node-setup-guide

1️⃣ Dependencies for WINDOWS & LINUX & VPS
```
sudo apt update && sudo apt upgrade -y
```

For VPS Only
```
apt install screen -y
```

2️⃣ Download Some Files
```
git clone https://github.com/Layer-Edge/light-node.git
cd light-node
```

3️⃣ Install Go & Rust & Risc0 Toolchain
```
cd $HOME
VER="1.22.0"
wget "https://golang.org/dl/go$VER.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$VER.linux-amd64.tar.gz"
rm "go$VER.linux-amd64.tar.gz"
[ ! -f ~/.bash_profile ] && touch ~/.bash_profile
echo "export PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.bash_profile
source $HOME/.bash_profile
[ ! -d ~/go/bin ] && mkdir -p ~/go/bin
go version
```
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustc --version
```
- Then Just Press Enter
```
curl -L https://risczero.com/install | bash && rzup install
```

4️⃣ Configure Environment Variables
```
export GRPC_URL=34.31.74.109:9090
export CONTRACT_ADDR=cosmos1ufs3tlq4umljk0qfe8k5ya0x6hpavn897u2cnf9k0en9jr7qarqqt56709
export ZK_PROVER_URL=http://127.0.0.1:3001
export API_REQUEST_TIMEOUT=100
export POINTS_API=http://127.0.0.1:8080
export PRIVATE_KEY='cli-node-private-key'
```
Make sure to fill in the ZK_PROVER_URL, PRIVATE_KEY with ur Actual Metamask Wallet Private Key
- Replace 'cli-node-private-key' with your actual private key.

### ZK Prover URL Address (for PC)
```
curl ifconfig.me
```
```
ip addr show eth0
```
Example output:
```
inet 192.168.50.150/24 brd 192.168.50.255 scope global eth0
```
the WSL IP is 192.168.50.150
- Use this IP instead of 127.0.0.1
```
export ZK_PROVER_URL=http://192.168.50.150:3001
```

5️⃣ Start the Merkle Service
```
cd risc0-merkle-service
cargo build && cargo run
```
Keep this terminal open and running. You need it for the next step.

## Open Another Window for WSL or VPS (do not close the previous one)

1️⃣ Start Node
```
cd light-node
go build
./light-node
```


