# XenbBlocksMiner

## Description
XenbBlocksMiner is a command-line tool for XenBlocks cryptocurrency mining (regular, Xuni and superblocks).
Attached is a latest version of the code, with support for switches. 

Tool created by WoodySoil, also available at:
https://github.com/woodysoil/XenblocksMiner/releases/tag/v1.1.2

## Usage
To use XenbBlocksMiner, run the following commands in your terminal:

```bash
./xenbBlocksMiner [switch options]
```

## Options

- `-h`, `--help`  
  Display help information about the XenbBlocksMiner options.

- `--totalDevFee arg`  
  Set the total developer fee. The argument `arg` should be replaced with the desired fee amount.

- `--ecoDevAddr arg`  
  Set the ecosystem developer address. This address will receive half of the total developer fee. Replace `arg` with the actual ecosystem developer address.

- `--minerAddr arg`  
  Set the miner address for receiving mining rewards. Replace `arg` with your actual miner address.

- `--saveConfig`  
  Update the configuration file with the inputs provided via the console.

## Configuration

To save the configuration on the server so next time it assumes all settings just by running the ./xenbBlocksMiner command automatically, use the `--saveConfig` option after setting your parameters.

For example that mines splits 1% of all fees between 0xYourMinerAddress (0.5%) and WoodySoil (0.5%), while mining 99% of the time for 0xYourMinerAddress:
```bash
./xenbBlocksMiner --totalDevFee 10 --ecoDevAddr 0xEcoDevAddress --minerAddr 0xYourMinerAddress --saveConfig
```

Replace `0xYourEcoDevAddress` and `0xYourMinerAddress` with your respective addresses.
