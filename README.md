# INITIA-PHASE-2
JAWA PRIDE VALIDATOR  
LINK TELEGRAM : https://t.me/AirdropJP_JawaPride 
LINK DISCUSS  : https://t.me/AirdropJPdiskusi 
LINK TWITTER  : https://x.com/JAWAPRIDE_ID 
LINK DISCORD  : https://discord.com/invite/dHtxRrs2US  

WEBSITE: https://linktr.ee/Jawa_Pride_ID


``` NODE TUTORIAL

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

