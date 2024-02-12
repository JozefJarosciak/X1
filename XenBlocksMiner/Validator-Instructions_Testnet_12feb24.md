
# How-To: Set Up Your X1 Testnet Validator (Updated Version: 12th February 2024)

## Table of Contents
- [Step 0: Requirements](#step-0-requirements)
- [Step 1: Prepare Your Environment](#step-1-prepare-your-environment)
- [Step 2: Download Snapshot and New X1 Version](#step-2-download-snapshot-and-new-x1-version)
- [Step 3: Backup Validator Keys](#step-3-backup-validator-keys)
- [Step 4: Update and Restart Your Validator Node](#step-4-update-and-restart-your-validator-node)
- [Step 5: Start Your Validator Node](#step-5-start-your-validator-node)
- [Additional Steps](#additional-steps)
- [The End](#the-end)

---

### Step 0: Requirements
- 🐧 Advanced or Expert Linux Knowledge (Ubuntu preferred)
- ☁️ Access to a personal Ubuntu server or an Ubuntu cloud instance
- 🗣️ Access to Metamask

---

### Step 1: Prepare Your Environment
Install all necessary packages. This is crucial for first-time node operators or if you're setting up a new server.

```bash
cd
apt-get update && apt-get upgrade -y
apt-get install python3 python3-pip git nano wget jq tmux moreutils wine htop sudo vim make -y
sudo pip install passlib requests tqdm argon2_cffi web3==6.11.1
sudo git clone --branch x1 https://github.com/FairCrypto/go-x1
sudo wget https://go.dev/dl/go1.21.4.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.4.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
source ~/.profile
source ~/.bashrc
cd && chmod -R 777 go-x1 && cd go-x1 && go mod tidy && make x1 && sudo cp build/x1 /usr/local/bin
```

---

### Step 2: Download Snapshot and New X1 Version
This approach is faster than regular syncing.

```bash
cd
wget --no-check-certificate https://xenblocks.io/snapshots/chaindata1715.pruned.tar
```

---

### Step 3: Backup Validator Keys
It's highly recommended to back up your validator keys as a precaution.

```bash
cd
cp -r ~/.x1/keystore ~/.
```

---

### Step 4: Update and Restart Your Validator Node
Ensure your validator is not running, then proceed with the update.

```bash
cd
rm -rf ~/.x1/chaindata
rm -rf ~/.x1/go-x1
tar -xvf chaindata1715.pruned.tar
cd && cd go-x1
git stash # Optional: Stash any changes if needed
git pull
git checkout x1 # Ensure you're on the latest branch
git stash pop # Optional: Apply stashed changes if any
go mod tidy
make x1
sudo cp build/x1 /usr/local/bin
cd
```

---

### Step 5: Start Your Validator Node
Start your validator with the updated settings. Adjust the cache value as per the network's recommendation.

```bash
clear && cd && cd go-x1
x1 --testnet --validator.id YOUR_VALIDATOR_ID --validator.pubkey YOUR_VALIDATOR_PUBKEY --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode full --cache YOUR_CACHE_VALUE
```

**Note:** For the `--cache` value, it's suggested to initially run your validator without this flag to get a recommended cache value from the network. Then, restart your validator with the specified cache value.

---

### Additional Steps
Continue following the original steps for configuring Metamask, staking, and setting up the validator as a service, as outlined in the initial guide. These steps remain crucial for the complete setup and operation of your X1 Testnet Validator node.

---

### The End
Congratulations, you've updated and are running an X1 Testnet Validator node! Ensure your node remains operational 24/7 to contribute effectively to the network.
