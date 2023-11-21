### Installing StarkNet node

#### *StarkNet is a decentralized, permissionless ZK-Rollup. It operates as an L2 network over Ethereum. Top funds on board: Paradigm, Sequoia, Three Arrows Capital, Polychain, Alameda Resaerch, Coinbase Ventures, Intel and VITALIK BUTERIN himself.*

##### *The node is not demanding - 2 cores // 2 gig // 100 GB*
```bash
sudo apt update
sudo apt full-upgrade -y
sudo apt install -y python3-pip
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
sudo apt-get install libgmp-dev
pip3 install fastecdsa
sudo apt-get install -y pkg-config
apt install curl -y
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
sudo apt install cargo -y
rustup update stable
apt install git -y
```

##### *Attention! Over time, new versions will appear, so instead of v0.1.7-alpha, you will need to register. You can check the current version **[here](https://github.com/eqlabs/pathfinder/tags)**.*

```bash
git clone --branch v0.1.7-alpha https://github.com/eqlabs/pathfinder.git
sudo apt install python3.8-venv
apt-get install screen -y
screen -S myscreen
cd pathfinder/py
python3 -m venv .venv
source .venv/bin/activate
PIP_REQUIRE_VIRTUALENV=true pip install --upgrade pip
PIP_REQUIRE_VIRTUALENV=true pip install -r requirements-dev.txt
cargo build --release --bin pathfinder
```

##### *Go to [Alchemy.com](https://www.alchemy.com/) and register*

##### *On the server we write the following command, in which xxxxxx is replaced with this very API KEY*

```bash
cargo run --release --bin pathfinder -- --ethereum.url https://eth-mainnet.alchemyapi.io/v2/xxxxxx
```

##### *After complete synchronization, we will only have to occasionally check that the node continues to work. New errors, as well as additional commands that need to be written when developers update the network, can be found in the project’s discord.*
