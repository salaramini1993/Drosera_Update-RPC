# Drosera_Update-RPC
*first go to Alchemy https://dashboard.alchemy.com/ and Create a new App, Copy the Holskey URL
```
# open your vps

cd my-drosera-trap
nano drosera.toml

## replace Holesky Url in the first line

** press Ctrl + x , y, Enter

```
```bash
# Deploy Trap
DROSERA_PRIVATE_KEY=xxx drosera apply
## Replace `xxx` with your `Pv_Key`
```
```bash
cd ~
```
# Resister operator
```bash
drosera-operator register --eth-rpc-url New-RPC --eth-private-key PV_KEY

## Replace `PV_KEY` with your Drosera EVM privatekey 
## Replace `New-RPC` with your `ALchemy RPC` 
```
Enter this command in the terminal, But first replace:
* `New_RPC` with your `Alchemy_URL`
* `PV_KEY` with your `privatekey`
* `VPS_IP` with your solid vps IP (without anything else)
* if using a `local` system, then replace vps ip with `0.0.0.0`
```bash
sudo tee /etc/systemd/system/drosera.service > /dev/null <<EOF
[Unit]
Description=drosera node service
After=network-online.target

[Service]
User=$USER
Restart=always
RestartSec=15
LimitNOFILE=65535
ExecStart=$(which drosera-operator) node --db-file-path $HOME/.drosera.db --network-p2p-port 31313 --server-port 31314 \
    --eth-rpc-url New-RPC \
    --eth-backup-rpc-url https://1rpc.io/holesky \
    --drosera-address 0xea08f7d533C2b9A62F40D5326214f39a8E3A32F8 \
    --eth-private-key PV_KEY \
    --listen-address 0.0.0.0 \
    --network-external-p2p-address VPS_IP \
    --disable-dnr-confirmation true

[Install]
WantedBy=multi-user.target
EOF

```
```bash
# reload systemd
sudo systemctl daemon-reload
sudo systemctl enable drosera
# start systemd
sudo systemctl start drosera
```
# wait 10 min
Blocks starts to get green 

done!

![Drosera](https://github.com/user-attachments/assets/c634f3e8-323d-492d-8b05-304fb767c300)

