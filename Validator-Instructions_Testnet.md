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

Now, connect to your Ubuntu server.
Once logged into the Ubuntu server, configure the X1 Testnet Blockchain following [these instructions](https://github.com/FairCrypto/go-x1) or the steps below:

```bash
# Login as root
sudo su
```

```bash
# Run system update
apt update -y
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/a6a55730-fa35-4fef-9f1c-2f768cb48f56" width="50%">

```bash
# Install dependencies (ex: ubuntu)
apt install -y golang wget git make
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/19a76602-e669-4dd9-9f08-f4b7d11d73f4" width="50%">

```bash
# Clone and build the X1 binary
git clone --branch x1 https://github.com/FairCrypto/go-x1
git stash
git pull && git checkout jacklevin74-patch-1
git stash pop
go mod tidy
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8d38bd21-7e50-4b4b-87c3-2e424656a1a5" width="50%">

```bash
cd go-x1
make x1
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/c0409b49-f418-4813-8003-a600531f1671" width="50%">

```bash
cp build/x1 /usr/local/bin
```
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/d730ae85-5b84-418f-9d68-860678859091" width="50%">

Your Testnet Validator is now successfully installed!

<br><hr><br>

### Step 5: Configure X1 Validator in Read-Only Mode
Let's first see if we can run the X1 Testnet node in the read-only mode with Xenblocks reporting enabled and also let's sync the database.
Run the following command:
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

To create a validator private key to sign consensus messages, use the below command.
After entering the command, you will be prompted to enter a password—use a strong one! 
You can, for example, use a password manager to generate a strong password to secure your wallet.

```bash
x1 validator new
```

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8b18bb33-53bb-4908-b1a6-2c799b61d645" width="50%">

Remember to make a note of the validator public key (indicated by the red arrow in the image above, as it will be required in STEP 7) and also make sure to securely save your validator key password (you will need this password each time you start the validator).

<br><hr><br>

### Step 7: Stake 100,000 XN using Metamask

Navigate to the SFC Contract on the explorer:
https://explorer.x1-testnet.xen.network/address/0xFC00FACE00000000000000000000000000000000/write-contract#address-tabs


Click the "Connect wallet" button and connect to your validator wallet.

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/8cfaaeb2-f4fe-46c0-8405-edecbc0f6b2d" width="50%">

Enter your validator public key and the amount of XN you want to stake, then click "Write".

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/a1af478d-0342-4aba-8ab1-98c48d34b75d" width="50%">

Confirm the transaction in your wallet (note: this will deduct 100,000 XN from your wallet):

![image](https://github.com/JozefJarosciak/X1/assets/3492464/83c075a5-835a-4390-8f32-e044dc6bd8c1)

Verify that your validator is registered by looking up your validator ID on the PWA explorer at:
https://pwa-explorer.x1-testnet.xen.network/staking

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/c8b3b702-e363-4ab8-9d7a-7d65c6dca514" width="50%">

<br><hr><br>

### Step 8: Start your X1 Validator Node

Ensure your node is stopped, and add the --validator.id and --validator.pubkey flags to your node's command line:

```bash
x1 --testnet --validator.id VALIDATOR_ID --validator.pubkey VALIDATOR_PUBKEY --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap
```
Note: You can also attach --validator.password ~/.x1/.password

For example, if you're the validator number 24 and your public key looks something like this: 0xc004569...1e74943bb4. You'd use the following command:

```bash
./build/x1 --testnet  --validator.id 24 --validator.pubkey 0xc004569...1e74943bb4 --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap
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
   Save the JSON file with a `.json` extension and upload it to your web server. The file should be available at `https://yourwebsite.pub/.../validator.json`, accessible to anyone with a web browser.

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
<i>Note: This method is not recommended, as it exposes your validator key password in a flat file.</i>

Create a new file 'automate_x1.sh'

```bash
sudo nano /root/go-x1/automate_x1.sh
```

Add the following content. Replace YOUR_PUBLIC_KEY_VALIDATOR_PASSWORD without your validator key password.

```bash
#!/usr/bin/expect
set timeout -1
spawn /root/go-x1/build/x1 --testnet --validator.id YOURID --validator.pubkey 0xc004....
expect "Passphrase:"
send -- "YOUR_PUBLIC_KEY_VALIDATOR_PASSWORD\r"
expect eof
```

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/aa10e679-c0c6-4f88-ac43-6efac68d2798" width="50%">

Now, let's create a service file a new file 'x1-testnet.service':

```bash
sudo nano /etc/systemd/system/x1-testnet.service
```

Add the following content:

```bash
[Unit]
Description=x1-testnet service
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/bin/expect /root/go-x1/automate_x1.sh
WorkingDirectory=/root/go-x1

[Install]
WantedBy=multi-user.target
```

<img src="https://github.com/JozefJarosciak/X1/assets/3492464/ca9bf1ca-3f58-4bd2-a095-fe60a5e31d8e" width="50%">


Ensure 'expect' is installed:
```bash
sudo apt-get install expect
```

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

<br><hr><br>

### The End
Congratulations, you are now running an X1 validator node! Make sure to keep your node up and running 24 hours a day. 

Fellow Xenians, if this guide helped, consider a donation: https://xen.pub/donate.php or delegate your XN with XenPub validators.

