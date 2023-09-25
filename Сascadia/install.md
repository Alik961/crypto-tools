### Install Cascadia node

```bash
apt update && apt upgrade -y
apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

```bash
ver="1.20.3" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```

```bash
git clone https://github.com/cascadiafoundation/cascadia && cd cascadia
git checkout v0.1.2
make install

cascadiad version --long | grep -e version -e commit
# v0.1.1
# commit: bde803072f5f52884a372c02d2249e743de9538d
```

```bash
cascadiad init NAME --chain-id cascadia_6102-1
```

```bash
wget -O $HOME/.cascadiad/config/genesis.json "https://anode.team/Cascadia/test/genesis.json"
```

```bash
wget -O $HOME/.cascadiad/config/addrbook.json "https://anode.team/Cascadia/test/addrbook.json"
```

```bash
pruning="custom"
pruning_keep_recent="1000"
pruning_interval="10"
sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" $HOME/.cascadiad/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" $HOME/.cascadiad/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" $HOME/.cascadiad/config/app.toml
```

```bash
tee /etc/systemd/system/cascadiad.service > /dev/null <<EOF
[Unit]
Description=Cascadiad
After=network-online.target

[Service]
User=$USER
ExecStart=$(which cascadiad) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

```bash
systemctl daemon-reload
systemctl enable cascadiad
systemctl restart cascadiad
journalctl -u cascadiad -f -o cat
```

```bash
cascadiad keys add name_wallet

cascadiad keys add name_wallet --recover

cascadiad keys add name_wallet --recover
```

```bash
cascadiad tx staking create-validator \
--chain-id cascadia_6102-1 \
--commission-rate 0.05 \
--commission-max-rate 0.2 \
--commission-max-change-rate 0.1 \
--min-self-delegation "1000000" \
--amount 1000000000000000000aCC \
--pubkey $(cascadiad tendermint show-validator) \
--moniker "moniker" \
--from <name_wallet> \
--gas auto \
--gas-adjustment=1.2 \
--gas-prices=7aCC
```
