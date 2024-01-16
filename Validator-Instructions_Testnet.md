# Simple Guide to Set Up a Validator for X1 Testnet

## Requirements:
- 🐧 Advanced or Expert Linux Knowledge (Ubuntu preferred)
- ☁️ Access to a personal Ubuntu server or a cloud instance (like AWS Lightsail, used in this tutorial)
- 🗣️ Access to Metamask

### Step 1: Create a New Metamask Wallet
To start from scratch, let's create a new Metamask wallet:
1. Click the account selector at the top of your wallet.
2. Click 'Add account or hardware wallet'.
3. Select 'Add a new account' in the subsequent menu.
4. Enter your preferred name and then hit 'Create' to confirm.

For additional guidance, visit [Metamask Support](https://support.metamask.io/hc/en-us/articles/360015289452-How-to-add-accounts-in-your-wallet).

### Step 2: Fill up the X1 Testnet Validator Application Form
To join as a block producer/validator on Testnet, you need 100,000 Test XN tokens. 

- Application form: [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSdnDAmXrGMKauEqNEpBI8HRhF1L33YkqL5f629cehxU_EyffA/viewform)
- More details in Jack's tweet: [Twitter](https://twitter.com/mrJackLevin/status/1745573668212924719)

### Step 3: Create a Cloud Ubuntu Server
Requirements: At least 2 GB RAM, 2 vCPUs, and 60 GB SSD.

1. **Sign in to AWS Lightsail**
   - Open [AWS Lightsail](https://lightsail.aws.amazon.com/)
   - Log in or create an account at [AWS](https://aws.amazon.com)

2. **Create a New Instance**
   - In the dashboard, click "Create instance".
   - Select Location: Choose Ohio (us-east-2) or another region.
   - Choose Instance Image: Select Linux/Unix and Ubuntu 22.04.
   - Choose Instance Plan: Select the plan with 2 GB RAM, 2 vCPUs, and 60 GB SSD (typically $10/month after 3 months free).
   - Name your instance.
   - Click "Create instance".

3. **Instance Configuration and Management**
   - Wait for Setup: Your instance will be ready in a few minutes.
   - Manage Instance: Use the Lightsail dashboard for management.

4. **Start the Instance**
   - Start it from the Lightsail dashboard if it's not running.

### Step 4: Connect to Your Ubuntu Server

1. **Connect Using SSH (Using PuTTY)**
   1.1 **Download PuTTY**
   - Download from [PuTTY download page](https://www.putty.org/).
   
   1.2 **Obtain SSH Key**
   - In the Lightsail dashboard, go to the Account page and download the default key under the SSH keys tab.
   
   1.3 **Convert the PEM file to PPK**
   - Open PuTTYgen and load the .pem file. Then, save it as a .ppk file.
   
   1.4 **Connect to Your Instance**
   - Open PuTTY.
   - Enter the public IP address of your Lightsail instance.
   - Go to Connection -> SSH -> Auth and select the .ppk file.
   - Click Open to initiate the connection.
   - Log in as `ubuntu` when prompted.

### Step 5: Configure X1 Validator

Now, logged into the Ubuntu server, configure the X1 Testnet Blockchain following [these instructions](https://github.com/FairCrypto/go-x1) or the steps below:

```bash
# Login as root
sudo su

# Install dependencies (ex: ubuntu)
apt update -y
apt install -y golang wget git make

Clone and build the X1 binary
git clone --branch x1 https://github.com/FairCrypto/go-x1
cd go-x1
make x1
cp build/x1 /usr/local/bin


This concludes the initial setting.


### Step 6: Configure X1 Validator
Further configuration steps will be provided here.
./build/x1 --testnet  --validator.id 19 --validator.pubkey 0xc004569809f6e889eaaeba2e8ffe85e5e668142ea74a18e3f9aa888be2f6243047d03cd6d7cb8e14288a78d46c580a74690704bc3e1e85ce12753611761e74943bb4 --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap


### Step 7: Register Icon

Register your validator icon using the following format and submitting it to the specified endpoint.

```json
{
  "name": "xencrypto1",
  "logoUrl": "https://xen.network/XEN-logo-square-dark%20512x512.png",
  "website": "https://xen.network",
  "contact": "https://t.me/XENCryptoTalk"
}


