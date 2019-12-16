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
export PATH=$PATH:~/theta/bin
```

The steps to install the binary on MacOSX and Windows are similar (on Windows you can use the PowerShell or Cygwin). The only difference is that the `os` parameter for downloading the MacOSX and Windows binary are `macos` and `windows`, respectively.

## Launch the guardian node

Now launch the Theta node in a console with the following command:

```
theta start --config=./guardian_testnet/node
```

**NOTE**: When the Theta node launches for the first time, you need to choose a password to encrypt the signing key of the guardian node. **Please choose a secure password and keep it in a safe place**. The next time when you restart the node, you will need the password to unlock it.

It might take some time for the node to sync up with the network (typically should be less than 10 minutes). To check if the node is already in-sync with the network, you can execute the following command

```
thetacli query status
```

The `syncing` field in the return indicates whether the node is still in the synchronization mode. If it is `false`, it means the node is already synced to the lastest block.

## Stake to the guardian node

After the node is synced (i.e. `syncing` is `false`), we can proceed to make it a **Guardian Node**. First we need to know the guardian address of this node. In another console, run 

```
./thetacli query guardian
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

The `summary` part is what we need for staking. For the next step, please follow the steps [here]() to stake some testnet Theta tokens from the Theta Wallet.

If everything works out, this node will start to send out guardian votes for the checkpoint blocks (i.e. the blocks whose `height%100 == 1`). In a few minutes we should start to see guardian votes in the log.

```
[2019-10-10 10:01:46] DEBUG [guardian] Boardcasting guardian vote vote=AggregatedVotes{Block: 0xab2a360ed292a14bb675837d1b1fe26de87414bdd8b9838d8d3646ca2c004844, Gcp: 0xd717f1d2bbdf0d8314341afcb30dc0d7d5419914c59754158cfa7a830c9d4c74,  Multiplies: [1, 3, 0, ...., 1, 2]}
```

Cheers! Now you should expect to receive your first TFUEL reward at the next checkpoint block!!!

