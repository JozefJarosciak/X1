# How-To: Set Up Your X1 Testnet Validator

## Table of Contents
- [Step 0: Requirements](#step-0--requirements)
- [Step 1: Order Cloud Ubuntu Linux Instance](#step-1-order-cloud-ubuntu-linux-instance)
- [Step 2: Create a New Metamask Wallet](#step-2-create-a-new-metamask-wallet)
- [Step 3: Fill up the X1 Testnet Validator Application Form](#step-3-fill-up-the-x1-testnet-validator-application-form)
- [Step 4: Configure X1 Validator](#step-4-configure-x1-validator)
- [Step 5: Configure X1 Validator in Read-Only Mode](#step-5-configure-x1-validator-in-read-only-mode)
- [Step 6: Create a new validator key](#step-6-create-a-new-validator-key)
- [Step 7: Stake 100,000 XN using Metamask](#step-7-stake-100000-xn-using-metamask)
- [Step 7.1 (Optional): Sync Data](#step-71-optional-sync-data)
- [Step 7.2 (Optional): Updating an Existing Installation of X1 Full Node](#step-72-optional-updating-an-existing-installation-of-x1-full-node)
- [Step 8: Start your X1 Validator Node](#step-8-start-your-x1-validator-node)
- [Step 9: Register Validator Name and Icon](#step-9-register-validator-name-and-icon)
- [Step 10: Run as a Service](#step-10-run-as-a-service)
- [The End](#the-end)

<br><br><br>

### Step 0:  Requirements:
- 🐧 Advanced or Expert Linux Knowledge (Ubuntu preferred)
- ☁️ Access to a personal Ubuntu server or an Ubuntu cloud instance
- 🗣️ Access to Metamask

<br><hr><br>

### Step 1: Order Cloud Ubuntu Linux Instance
The following is the minimum server configuration for an X1 Testnet Validator:

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/adbcf85a-db1f-4e24-a45e-1a59ee5c39ac" width="50%">

In terms of operating system, I would aim at minimum for Ubuntu 22.04.3 LTS (Jammy Jellyfish) that has a long term support.

Choosing the optimal cloud service can be challenging, as it largely depends on your cloud provider's preferences and budget.
Nevertheless, referencing Ethereum Mainnet Statistics reveals that Amazon AWS, Hetzner, and OVH are among the top three favoured services.
This trend might change in the future, but it could serve as a useful guide in selecting a suitable provider:

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/07c70924-9baf-48b0-a85f-06baa50be658" width="50%">

<br><hr><br>

### Step 2: Create a New Metamask Wallet
You can use the existing Metamask Wallet (we highly recommend using a hardware wallet connected to Metamask), or you can create a brand-new Metamask software wallet (less secure).
If you want to create a dedicated and brand new software X1 Testnet Validator Metamask wallet from scratch, follow these instructions in Metamask:
1. Click the account selector at the top of your wallet.
2. Click 'Add account or hardware wallet'.
3. Select 'Add a new account' in the subsequent menu.
4. Enter your preferred name
5. Hit 'Create' to confirm and you'll be able to see the new account
   
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/d67f8c2d-d943-4585-833a-b8d00bc292d2" width="50%">

For additional guidance, visit [Metamask Support](https://support.metamask.io/hc/en-us/articles/360015289452-How-to-add-accounts-in-your-wallet).


Switch your Metamask to X1 Testnet, if you do not have the X1 Tesnet Network configured in Metamask, add the following RPC:
* Network name: X1 Testnet
* New RPC URL: https://x1-testnet.xen.network/
* Chain ID: 204005
* Currency symbol: XN
* Block explorer URL: https://explorer.x1-testnet.xen.network/

<br><hr><br>

### Step 3: Fill up the X1 Testnet Validator Application Form
To join as a block producer/validator on Testnet, you need 100,000 Test XN tokens (plus a little more to run the staking transaction).
To qualify for the airdrop of 100k XN Testnet tokens, you'll need to fill up the application form.
URLs:
- Application form: [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSdnDAmXrGMKauEqNEpBI8HRhF1L33YkqL5f629cehxU_EyffA/viewform)
- More details in Jack's tweet: [Twitter](https://twitter.com/mrJackLevin/status/1745573668212924719)

After ensuring your validator wallet has sufficient XN, you're ready to move on to STEP 4. 
If you're currently low on XN, you can still advance to STEP 4, but be aware that the instructions provided will only take you up to Step 5. 
However, there's no cause for concern, as you'll have the opportunity to establish a read-only node and operate it while awaiting the XN airdrop.

<br><hr><br>

### Step 4: Configure X1 Validator

Now, connect to your Ubuntu server. In the examples below, I am using: Ubuntu Linux 22.04.3.
Once logged into the Ubuntu server, configure the X1 Testnet Blockchain following [these instructions](https://github.com/FairCrypto/go-x1) or the steps below:

Login as root.
```bash
sudo su
```

Update your package lists and upgrade the system.
```bash
apt-get update && apt-get upgrade -y
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/a6a55730-fa35-4fef-9f1c-2f768cb48f56" width="50%">


Double check that you're in the /home/ubuntu directory.
You should see the response: /home/ubuntu.
```bash
pwd
```

If you're not in /home/ubuntu directory, run:
```bash
cd /home/ubuntu
```

Install dependencies and other useful tools.
```bash
apt install -y golang python3 python3-pip git nano wget jq tmux moreutils wine htop sudo vim make
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/19a76602-e669-4dd9-9f08-f4b7d11d73f4" width="50%">

Clone and build the X1 binary. This command sequence clones the x1 branch of the go-x1 repository from GitHub, downloads the Go 1.21.4 Linux binary, extracts it to /usr/local, adds Go to the system PATH, and then reloads the .profile and .bashrc files to update the current shell environment with the new PATH.
```bash
git clone --branch x1 https://github.com/FairCrypto/go-x1 && sudo wget https://go.dev/dl/go1.21.4.linux-amd64.tar.gz && sudo tar -C /usr/local -xzf go1.21.4.linux-amd64.tar.gz && export PATH=$PATH:/usr/local/go/bin && source ~/.profile && source ~/.bashrc
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8d38bd21-7e50-4b4b-87c3-2e424656a1a5" width="50%">


The following command sets the permissions of the go-x1 directory and all its contents to 777 (read, write, execute for all users), navigates into the go-x1 directory, and then runs go mod tidy to clean up the module's dependencies.
```bash
chmod -R 777 go-x1 && cd go-x1 && go mod tidy
```

The next command compiles and builds the X1.
```bash
make x1
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/c0409b49-f418-4813-8003-a600531f1671" width="50%">


Now, let's copy the x1 executable from the build directory to the /usr/local/bin directory, making it accessible system-wide as a command.
```bash
cp build/x1 /usr/local/bin
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/d730ae85-5b84-418f-9d68-860678859091" width="50%">

Your Testnet Validator is now successfully installed!


<br><hr><br>

### Step 5 (Optional): Configure X1 Validator to run in Read-Only Mode
If you do not wish to run the full X1 Testnet Validator node, you can finish with the following step and run your validator in the read-only mode with Xenblocks reporting enabled.

To do so, run the following command:
```bash
x1 --testnet --syncmode snap --xenblocks-endpoint ws://xenblocks.io:6668
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8f8a4158-89d4-4c72-a9d7-c059f770c397" width="50%">

Be aware that the completion of the above step may take a while, as the server needs time to synchronize data. During this period, you can monitor the progress, which is illustrated in the provided screenshot. After the synchronization is fully complete, the status displayed on the screen will appear as follows:

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/d730ae85-5b84-418f-9d68-860678859091" width="50%">

Note:
<i>
If operating an X1 node in read-only mode meets your needs for now, you can conclude by following these instructions here, as your server setup is now complete.

I highly recommend keeping the read-only node running (while waiting for the airdrop) or just running it in the read-only node permanently. Running a read-only blockchain node plays a crucial and highly valuable role in supporting the X1 blockchain community. By doing so, you contribute to the network's robustness and decentralization. A read-only node helps in maintaining a copy of the blockchain, ensuring data integrity and consistency across the network and this improves the network's resilience against potential attacks and failures, as multiple copies of the blockchain data exist. By participating in this way, you're not only supporting the underlying infrastructure of the blockchain but also fostering a more trustful and transparent environment for all users, but you may also be rewarded by XN airdrops (update on this soon).
</i>

If your goal is to operate an X1 Testnet Validator node and you have confirmed that your validator wallet has enough XN, you should press CTRL-C to terminate the active X1 service and proceed to STEP 6.

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/1966c91c-99ff-4fa3-87ad-8347b8d840f0" width="50%">

<br><hr><br>


### Step 6: Create a new validator key

If you don't have the existing validator private key to sign the consensus messages, we need to first create one. This is critical step in order to run a full X1 validator.
After entering the command, you will be prompted to enter a password—use a strong one! 
You can, for example, use a password manager to generate a strong password to secure your wallet.

```bash
x1 validator new
```

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8b18bb33-53bb-4908-b1a6-2c799b61d645" width="50%">

Remember to make a note of the validator public key (indicated by the red arrow in the image above, as it will be required in STEP 7) and also make sure to securely save your validator key password (you will need this password each time you start the validator).
The path of the actual secret key file should be pointing to: /root/.x1/keystore/validator/...

<br><hr><br>

### Step 7: Stake 100,000 XN using Metamask

Navigate to the SFC Contract (Write part) on the explorer:
https://explorer.x1-testnet.xen.network/address/0xFC00FACE00000000000000000000000000000000/write-contract#address-tabs

Click the "Connect wallet" button at the top, and connect to the wallet, that has at least 100,000 XN in it.

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8cfaaeb2-f4fe-46c0-8405-edecbc0f6b2d" width="50%">

Once connected, go to #4 function called: **createValidator** and enter your validator public key and the amount of XN you want to stake, then click "Write".

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/a1af478d-0342-4aba-8ab1-98c48d34b75d" width="50%">

Confirm the transaction in your wallet (note: this will deduct 100,000 XN from your wallet):

![image](https://github.com/JozefJarosciak/X1/assets/3492464/83c075a5-835a-4390-8f32-e044dc6bd8c1)

Now, we need to retrieve your Validator ID. This is critical to run the full X1 validator node.
Navigate to the SFC Contract (Read part) on the explorer:
https://explorer.x1-testnet.xen.network/address/0xFC00FACE00000000000000000000000000000000/read-contract#address-tabs
Go to #18 function called: ** getValidatorID** and enter your Ethereum wallet address and press 'Query' button.

Then Mark down the Validator ID, the number that was provided to you. 


<br><hr><br>


### Step 7.1: Sync Data
This process may not be necessary, and may take some time depending on your internet speed, but it could be quicker than the regular syncing method.

1) Open your terminal and navigate to your home directory:
    ```
    cd /home/ubuntu
    ```
2) Download the snapshot:
    ```
    wget --no-check-certificate https://xenblocks.io/snapshots/chaindata1715.pruned.tar
    ```

3) Extract the downloaded snapshot:     
   ```
   tar -xvf chaindata1715.pruned.tar -C /root
   ```

### Step 7.2 (Optional): Updating an Existing Installation of X1 Full Node 

Skip this step if you're doing the first time installation.

If you are updating an existing X1 full node installation, follow the instructions below.

0) Open your terminal and navigate to your home directory:
    ```
    cd /home/ubuntu
    ```
1) Backup your validator keys:
    ```
    cp -r ~/.x1/keystore ~/
    ```
2) Remove your existing chaindata:
    ```
    rm -rf ~/.x1/chaindata
    ```
3) Remove the existing go-x1 directory:
    ```
    rm -rf ~/.x1/go-x1
    ```
4) Extract the downloaded snapshot:
    ```
    tar -xvf chaindata1715.pruned.tar -C /root
    ```
5) Navigate to the go-x1 directory and stash any changes you've made:
    ```
    cd && cd go-x1
    git stash
    ```
6) Pull the latest changes from the repository:
    ```
    git pull
    ```
7) Checkout the x1 branch (double-check if this is the most current version):
    ```
    git checkout x1
    ```
8) Pop the changes you've stashed:
    ```
    git stash pop
    ```
9) Tidy up the Go modules:
    ```
    go mod tidy
    ```
10) Make x1:
    ```
    make x1
    ```
11) Copy the x1 binary to your bin directory:
    ```
    sudo cp build/x1 /usr/local/bin
    ```
12) Navigate to your home directory:
    ```
    cd
    ```


<br><hr><br>

### Step 8: Start your X1 Validator Node

Let's create your password file.
This is not necessary, but it simplifies the creation of the X1 service.
It also allows us to automatically start the X1 node, rather than entering your password every time you restart the server.

Replace YOUR_PASSWORD with your password:
```bash
echo "YOUR_PASSWORD" > ~/.x1/.password
```

Double check that the file is there and your password is inside it. 
Note: The location of the file should be in /root/.x1/.password
```bash
nano ~/.x1/.password
```


Ensure your node is stopped (in case it's running) and let's clear the terminal screen, change to our home directory, and navigates into the go-x1 directory within the home directory.
```bash
clear && cd /home/ubuntu && cd go-x1
```

Now, let's start the X1 validator node!

Ensure your node is stopped (in case it's running). 

- Add the --validator.id (we've collected this earlier from SFC Contract).
- Add --validator.pubkey.
- Add --validator.password 
, flags to your node's command line:

Execute this and prepare to stop the validator within a couple of seconds after start.
```
x1 --testnet --validator.id VALIDATOR_ID --validator.pubkey VALIDATOR_PUBKEY --validator.password ~/.x1/.password --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap
```

As you could see, when we started the Validator by using the above command line, it warned us about allocating more cache, that looked something like this:
```
WARN [02-13|16:10:37.405] Please add '--cache 32034' flag to allocate more cache for X1. Total memory is 64068 MB.
```

The --cache suggested amount will likely differ from server to server. 

So take a note of your --cache number and let's improve our validator, running with the --cache variable (suggested method).

```bash
x1 --testnet --validator.id VALIDATOR_ID --validator.pubkey VALIDATOR_PUBKEY --validator.password ~/.x1/.password --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap --cache YOUR_CACHE_RESULT
```

Once fully synchronized and running, you'd see something like this on your screen:

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/de820bca-84eb-4d49-8b71-f33acd0d24e1" width="50%">

<br><hr><br>


### Step 9: Register Validator Name and Icon

To register your validator's name and icon on the X1 Testnet, follow these detailed instructions. Note that you will require a web server to host the image file.

1. **Create an Icon Image:**
   Design a 100x100 px image with a transparent background. For example, the following logo was created using the Snagit Editor:
   <img src="https://github.com/JozefJarosciak/X1/assets/3492464/d3ba09b1-3389-437a-a290-8fa9f5799806" width="50%">

3. **Save and Upload the Image:**
   Save the image in PNG format. For instance, the image might be named `logo.png`. Upload the image to a web server or an online location that allows direct file linking. For example, the image can been uploaded to `https://yourwebsite.com/images/logo.png`, making it accessible via a web browser.

4. **Create a JSON Configuration File:**
   You will need to create a JSON file containing the validator's name, logo URL, website, and contact information. This file will later be uploaded to the X1 Testnet smart contract.

   Template for JSON file:
   ```json
   {
     "name": "VALIDATOR_NAME", /* Name of the validator */
     "logoUrl": "LOGO_URL", /* Validator logo (PNG|JPEG|SVG) - 100px x 100px */
     "website": "WEBSITE_URL", /* Website URL */
     "contact": "CONTACT_URL" /* Contact URL */
   }
   ```
   Example JSON configuration:
   ```json
   {
     "name": "Validator_1", 
     "logoUrl": "https://yourwebsite.com/images/logo.png",
     "website": "https://yourwebsite.com",
     "contact": "https://t.me/your_twitter_name"
   }
   ```

   Important: As a name of the server, do not include any special characters or spaces (e.g. Validator_1 is valid, but something like "🐧Validator #1" would not work).

5. **Upload the JSON File:**
   Save the JSON file with a `.json` extension and upload it to your web server. The file should be available at `https://yourwebsite.com/.../validator.json`, accessible to anyone with a web browser.

6. **Update the X1 Testnet Smart Contract:**
   Visit the URL: [X1 Testnet Smart Contract](https://explorer.x1-testnet.xen.network/address/0x891416e8bDB4437d4D0D303781A3828262220581/write-proxy#address-tabs).
   Connect your Metamask wallet and navigate to section number 5 (`updateInfo`):

   <img src="https://github.com/JozefJarosciak/X1/assets/3492464/2af1ab65-6087-4892-affc-fcd87a3938e1" width="50%">

   Enter the URL of your JSON file (e.g., `https://yourwebsite.com/.../validator.json`) and press 'Write':

   <img src="https://github.com/JozefJarosciak/X1/assets/3492464/26ca60d4-853b-4164-b379-92585a404bbc" width="50%">
  
   Upon completion, your validator's logo and name will be displayed on the list of validators at [X1 Testnet Staking Explorer](https://pwa-explorer.x1-testnet.xen.network/staking).

   <img src="https://github.com/JozefJarosciak/X1/assets/3492464/d633c4fa-8b7f-4c48-be15-dc707c2750d1" width="50%">
   

### Step 10: Run as a Service

This last step is not required, but if you want to run X1 Validator as a service that automatically starts on boot, and restarts on failure, you can follow the below instructions.
<i>Note: This method is okay, just note that through the use t exposes your validator key password in a flat file.</i>

Let's create a service file a new file 'x1-testnet.service':

```bash
nano /etc/systemd/system/x1-testnet.service
```

Add the following content:

```bash
[Unit]
Description=x1-testnet service
After=network.target

[Service]
Type=simple
User=root
ExecStart=/home/ubuntu/go-x1/build/x1 --testnet --validator.id VALIDATOR_ID --validator.pubkey VALIDATOR_PUBKEY --validator.password /root/.x1/.password --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap --cache YOUR_CACHE_RESULT
WorkingDirectory=/home/ubuntu/go-x1

[Install]
WantedBy=multi-user.target
```

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/ca9bf1ca-3f58-4bd2-a095-fe60a5e31d8e" width="50%">


Now, reload services, enable the new service and start it.
```bash
sudo systemctl daemon-reload
sudo systemctl enable x1-testnet.service
sudo systemctl start x1-testnet.service
```

Now you can test it, to ensure it's running:
```bash
sudo systemctl status x1-testnet.service
```

You should see the system as active and running:
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/964f9ae8-13aa-49cc-9f96-57bb1a2cb917" width="50%">

If you want you can monitor your service in real-time by using journalctrl:

```bash
sudo journalctl -u x1-testnet.service -f --output=cat
```


<br><hr><br>

### The End
Congratulations, you are now running an X1 validator node! Make sure to keep your node up and running 24 hours a day. 

Fellow Xenians, if this guide helped, consider a donation: https://xen.pub/donate.php or delegate your XN with XenPub validators.

