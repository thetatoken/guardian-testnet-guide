# Running a Guardian Node through Command Line

## Install the guardian node

Please follow the instructions below to download the lastest Linux binary and the necessary data. If you prefer to compile from the source code, please follow the steps [here]().

```
mkdir ~/theta
cd ~/theta
mkdir bin
mkdir -p guardian_testnet/node
wget -O bin/theta `curl 'http://guardian-testnet-data.thetatoken.org:3000/binary?os=linux&name=theta'`
wget -O bin/thetacli `curl 'http://guardian-testnet-data.thetatoken.org:3000/binary?os=linux&name=thetacli'`
wget -O guardian_testnet/node/snapshot `curl http://guardian-testnet-data.thetatoken.org:3000/snapshot`
wget -O guardian_testnet/node/config.yaml `curl 'http://guardian-testnet-data.thetatoken.org:3000/config?is_guardian=true'`
chmod +x bin/theta
chmod +x bin/thetacli
```

The steps to install the binary on MacOSX and Windows are similar (on Windows you can use the PowerShell or Cygwin). The only difference is that the `os` parameter for downloading the MacOSX and Windows binary are `macos` and `windows`, respectively.

## Run the guardian node

Now launch the Theta node in a console with the following commands:

```
cd bin/
./theta start --config=../guardian_testnet/node
```

**NOTE**: When the Theta node launches for the first time, you need to choose a password to encrypt the signing key of the guardian node. **Please choose a secure password and keep it in a safe place**. The next time when you restart the node, you will need the password to unlock it.

Next we can stake some tokens to this node to make it carry out guardian duties. First we need to know the guardian address of this node. In another console, run 

```
thetacli query guardian
```

The output should look something like this:

```
{
    "Address": "0x8f3B...E819",
    "BlsPubkey": "a1225b...16ebe",
    "BlsPop": "b49fd2a...d025c",
    "Signature": "14deb5e...52500",
    "Summary": "0x8f3Bc...952500"
}
```

The `summary` part is what we need for the staking. To stake from the Theta Wallet. Please follow the steps [here]().

If everything is successful, this node will start to send out guardian vote for every 100th block. In a few minutes we should start to see guardian votes in the log:

```
[2019-10-10 10:01:46] DEBUG [guardian] Boardcasting guardian vote vote=AggregatedVotes{Block: 0xab2a360ed292a14bb675837d1b1fe26de87414bdd8b9838d8d3646ca2c004844, Gcp: 0xd717f1d2bbdf0d8314341afcb30dc0d7d5419914c59754158cfa7a830c9d4c74,  Multiplies: [1]}
```
