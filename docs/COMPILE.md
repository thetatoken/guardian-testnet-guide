# Install Guardian Node from Source Code

## Install Go 1.12.1

Install Go and set environment variables `GOPATH` , `GOBIN`, and `PATH` following the commands below. The current code base should compile with **Go 1.12.1** on a Linux like system (i.e. Ubuntu, Mac OS X). Below are the steps to install Go 1.12.1 and setup the environments on Ubuntu.

```
screen -S theta
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install gcc
sudo apt-get install make
sudo wget https://dl.google.com/go/go1.12.1.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.12.1.linux-amd64.tar.gz
echo 'export GOROOT=/usr/local/go' >> ~/.bashrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOROOT/bin:$GOPATH/bin' >> ~/.bashrc
echo 'export THETA_HOME=$GOPATH/src/github.com/thetatoken/theta'
source ~/.bashrc
```

## Checkout and compile the Theta Guardian source code

Clone the `guardian-testnet` branch of the Theta Ledger repo https://github.com/thetatoken/theta-protocol-ledger into your `$GOPATH` with the following command. The path should look like this: `$GOPATH/src/github.com/thetatoken/theta`

```
git clone --branch guardian-testnet https://github.com/thetatoken/theta-protocol-ledger.git $GOPATH/src/github.com/thetatoken/theta

cd $THETA_HOME
export GO111MODULE=on
make install
```

## Download necessary data for the Guardian Node

```
cd $THETA_HOME
mkdir -p ../guardian_testnet/node
wget -O ../guardian_testnet/node/snapshot `curl -k https://guardian-testnet-data.thetatoken.org/snapshot`
wget -O ../guardian_testnet/node/config.yaml `curl -k 'https://guardian-testnet-data.thetatoken.org/config?is_guardian=true'`
```

## Launch the node and stake

Please continue with the instructions [here](./CLI.md#launch-the-guardian-node).


