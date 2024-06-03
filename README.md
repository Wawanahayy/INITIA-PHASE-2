# INITIA-PHASE-2                                                                 
JAWA PRIDE VALIDATOR                                                 
LINK TELEGRAM : https://t.me/AirdropJP_JawaPride                               
LINK DISCUSS  : https://t.me/AirdropJPdiskusi                                            
LINK TWITTER  : https://x.com/JAWAPRIDE_ID                                                             
LINK DISCORD  : https://discord.com/invite/dHtxRrs2US                                                                            

WEBSITE: https://linktr.ee/Jawa_Pride_ID                                       


About Initia                                  
Initia is a pioneering network for interwoven rollups, revolutionizing blockchain by simplifying complexity and providing a unified platform akin to using your favorite smartphone, inspired by Apple's design philosophy.
                                                         
Website : https://initia.xyz/                                                                                                            
Githubh : https://github.com/initia-labs                                                                            
Twitter : https://x.com/initiaFDN                                                                               
Discord : https://discord.gg/initia                                                               
Blog    : https://medium.com/@initiafdn                                                      
docs    : https://docs.initia.xyz/                                                                        

INITIA TASK: https://initia-xyz.notion.site/The-Initiation-Validator-Tasks-6d88ab0034644473907435662f9285b3                                                                              


```                                                       NODE TUTORIAL

1) Install Dependencies
sudo apt update && sudo apt install curl git jq build-essential gcc unzip wget lz4 -y


2) Install Go
ver="1.22.0" && wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && rm "go$ver.linux-amd64.tar.gz" && echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && source $HOME/.bash_profile && go version


3) Install Binary
git clone https://github.com/initia-labs/initia.git
cd initia
git checkout v0.2.15
make install
initiad version


4) Set Variables
echo 'export MONIKER="TEST_NODE"' >> ~/.bash_profile
echo 'export CHAIN_ID="initiation-1"' >> ~/.bash_profile
echo 'export WALLET="wallet"' >> ~/.bash_profile 
source $HOME/.bash_profile


5) Initialize the node
cd $HOME
initiad init $MONIKER --chain-id $CHAIN_ID


6) Download Genesis and Addrbook File
wget -O genesis.json https://files2.blacknodes.net/initiatestnet/genesis.json --inet4-only
mv genesis.json $HOME/.initia/config/
wget -O addrbook.json https://files2.blacknodes.net/initiatestnet/addrbook.json --inet4-only
mv addrbook.json $HOME/.initia/config/


7) Use Our Live Peers
peers=$(curl -s https://services.blacknodes.net/Initia-Testnet/data/peers.txt)
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.initia/config/config.toml


8) Use Our Fast Node Snapshot
curl -L http://snapshots.staking4all.org/testnet-snapshots/initia/latest/initia.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.initia


9) Create a Service File
sudo tee /etc/systemd/system/initiad.service > /dev/null <<EOF
[Unit]
Description=Initia Node
After=network.target

[Service]
User=$USER
Type=simple
ExecStart=$(which initiad) start --home $HOME/.initia
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF


10) Enable and Start The Node
sudo systemctl daemon-reload
sudo systemctl enable initiad.service
sudo systemctl restart initiad.service
sudo journalctl -u initiad.service -f -o cat





                                      Initia Validator Tutorial

1. Add Wallet OR RECOVERY WALLET
initiad keys add $WALLET
or
initiad keys add $WALLET --recover


2. Use Faucet To Get Balance for Creating validator
Initia Testnet Faucet: https://faucet.testnet.initia.xyz/


3) Create a validator
initiad tx mstaking create-validator \
  --amount=1000000uinit \
  --pubkey=$(initiad tendermint show-validator) \
  --moniker=$MONIKER \
  --chain-id=$CHAIN_ID \
  --commission-rate=0.05 \
  --commission-max-rate=0.10 \
  --commission-max-change-rate=0.01 \
  --from=$WALLET \
  --identity="" \
  --website="" \
  --details="BlackNodes Tutorial" \
  --gas=2000000 --fees=300000uinit \
  --node https://initia-testnet-rpc.blacknodes.net:443 \
  -y



                                      Service operations COMMAND ⚙️
1. BLOCK HIGHT/LEFT
local_height=$(curl -s localhost:26657/status | jq -r .result.sync_info.latest_block_height); network_height=$(curl -s http://initia-testnet-rpc.staking4all.org/status | jq -r .result.sync_info.latest_block_height); blocks_left=$((network_height - local_height)); echo "Your node height: $local_height"; echo "Network height: $network_height"; echo "Blocks left: $blocks_left"

2. NODE LOGS
sudo journalctl -u initiad -f -o cat

3. Check logs
sudo journalctl -u initiad -f

4. Start service
sudo systemctl start initiad

5. Stop service
sudo systemctl stop initiad

6. Restart service
sudo systemctl restart initiad
sudo journalctl -u initiad -f -o cat

7. Check service status
sudo systemctl status initiad

8. Reload services
sudo systemctl daemon-reload

9. Enable Service
sudo systemctl enable initiad

10. Disable Service
sudo systemctl disable initiad

10. Node info
initiad status 2>&1 | jq






                             COMMAND CHEAT

1. List All Wallets
initiad keys list

2. Delete wallet
initiad keys delete $WALLET

3. Check Balance
initiad q bank balances $WALLET_ADDRESS 

4. Withdraw all rewards
initiad tx distribution withdraw-all-rewards --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff 

5. Withdraw rewards and commission from your validator
initiad tx distribution withdraw-rewards $VALOPER_ADDRESS --from $WALLET --commission --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff

6. Check your balance
initiad query bank balances $WALLET_ADDRESS

7. Delegate to Yourself
initiad tx mstaking delegate $(initiad keys show $WALLET --bech val -a) 1000000uinit --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff 
Delegate

8. initiad tx mstaking delegate <TO_VALOPER_ADDRESS> 1000000uinit --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff
	
Redelegate Stake to Another Validator
initiad tx mstaking redelegate $VALOPER_ADDRESS <TO_VALOPER_ADDRESS> 1000000uinit --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff

9. Unbond
initiad tx mstaking unbond $(initiad keys show $WALLET --bech val -a) 1000000uinit --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff 

10. Transfer Funds
initiad tx bank send $WALLET_ADDRESS <TO_WALLET_ADDRESS> 1000000uinit --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff 


                                      Validator COMMAND CHEAT

1. Validator info
initiad status 2>&1 | jq

2. Validator Details
initiad q staking validator $(initiad keys show $WALLET --bech val -a) 

3. Jailing info
initiad q slashing signing-info $(initiad tendermint show-validator) 

4. Slashing parameters
initiad q slashing params 

5. Unjail validator
initiad tx slashing unjail --from $WALLET --chain-id initiation-1 --gas=2000000 --fees=563000move/944f8dd8dc49f96c25fea9849f16436dcfa6d564eec802f3ef7f8b3ea85368ff 

6. Active Validators List
initiad q staking validators -oj --limit=2000 | jq '.validators[] | select(.status=="BOND_STATUS_BONDED")' | jq -r '(.tokens|tonumber/pow(10; 6)|floor|tostring) + " 	 " + .description.moniker' | sort -gr | nl
 
7. Check Validator key
[[ $(initiad q staking validator $VALOPER_ADDRESS -oj | jq -r .consensus_pubkey.key) = $(initiad status | jq -r .ValidatorInfo.PubKey.value) ]] && echo -e "Your key status is ok" || echo -e "Your key status is error"

8. Signing info
initiad q slashing signing-info $(initiad tendermint show-validator) 

                             Delete node
sudo systemctl stop initiad
sudo systemctl disable initiad
sudo rm -rf /etc/systemd/system/initiad.service
sudo rm $(which initiad)
sudo rm -rf $HOME/.initia
sed -i "/INITIA_/d" $HOME/.bash_profile
