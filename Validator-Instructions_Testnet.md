# Simple Guide to Set Up a Validator for X1 Testnet

## Requirements:
- 🐧 Advanced or Expert Linux Knowledge (Ubuntu preferred)
- ☁️ Access to a personal Ubuntu server or a cloud instance (like AWS Lightsail, used in this tutorial)
- 🗣️ Access to Metamask



### Step 1: Order Cloud Ubuntu Linux Instance
The following is the minimum server configuration for an X1 Testnet Validator:
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/adbcf85a-db1f-4e24-a45e-1a59ee5c39ac" width="50%">

Choosing the optimal cloud service can be challenging, as it largely depends on your cloud provider's preferences and budget.
Nevertheless, referencing Ethereum Mainnet Statistics reveals that Amazon AWS, Hetzner, and OVH are among the top three favoured services.
This trend might change in the future, but it could serve as a useful guide in selecting a suitable provider:
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/07c70924-9baf-48b0-a85f-06baa50be658" width="50%">



### Step 2: Create a New Metamask Wallet
You can use the existing Metamask Wallet, or you can create a brand-new one.
If you want to create a dedicated and brand new X1 Testnet Validator Metamask wallet from scratch, follow these instructions in Metamask:
1. Click the account selector at the top of your wallet.
2. Click 'Add account or hardware wallet'.
3. Select 'Add a new account' in the subsequent menu.
4. Enter your preferred name
5. Hit 'Create' to confirm and you'll be able to see the new account
<img src="https://github.com/JozefJarosciak/X1/assets/3492464/d67f8c2d-d943-4585-833a-b8d00bc292d2" width="50%">

For additional guidance, visit [Metamask Support](https://support.metamask.io/hc/en-us/articles/360015289452-How-to-add-accounts-in-your-wallet).



### Step 3: Fill up the X1 Testnet Validator Application Form
To join as a block producer/validator on Testnet, you need 100,000 Test XN tokens (plus a little more to run the staking transaction).
To qualify for the airdrop of 100k XN Testnet tokens, you'll need to fill up the application form.
URLs:
- Application form: [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSdnDAmXrGMKauEqNEpBI8HRhF1L33YkqL5f629cehxU_EyffA/viewform)
- More details in Jack's tweet: [Twitter](https://twitter.com/mrJackLevin/status/1745573668212924719)


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


### Step 5: Configure X1 Validator
Further configuration steps will be provided here.
```bash
./build/x1 --testnet  --validator.id 19 --validator.pubkey 0xc004569809f6e889eaaeba2e8ffe85e5e668142ea74a18e3f9aa888be2f6243047d03cd6d7cb8e14288a78d46c580a74690704bc3e1e85ce12753611761e74943bb4 --xenblocks-endpoint ws://xenblocks.io:6668 --gcmode full --syncmode snap
```


### Step 6: Register Icon

Register your validator icon using the following format and submit it to the specified endpoint.

```json
{
  "name": "xencrypto1",
  "logoUrl": "https://xen.network/XEN-logo-square-dark%20512x512.png",
  "website": "https://xen.network",
  "contact": "https://t.me/XENCryptoTalk"
}
```

