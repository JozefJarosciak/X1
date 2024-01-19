
# XENBLOCKS - Effortless GPU Mining with 1 line of Code
This repository explains how to automate the initial setup and running of the XenBlocks Miner using a single command line that automatically prefills your ETH address as well as Dev Fee.

## One-Liner Command

The command provided below automates the process of downloading, extracting, making the XenBlocks Miner executable, and running it with predefined user inputs (EIP-55 address and dev fee).

```bash
wget https://github.com/woodysoil/XenblocksMiner/releases/download/v1.1/xenblocksMiner-v1.1.1-Linux-x86_64.tar.gz && tar -vxzf xenblocksMiner-v1.1.1-Linux-x86_64.tar.gz && chmod +x xenblocksMiner && echo -e "0xca5F023af4F822353A563Ae6a3591bA2024495E8
0" | ./xenblocksMiner
```

## Video Demo
https://github.com/JozefJarosciak/X1/assets/3492464/fb04edd7-7639-425c-91a8-baeac9c0f19e


## How It Works

1. `wget`: Downloads the XenBlocks Miner tarball from the provided GitHub link.
2. `tar -vxzf`: Extracts the downloaded tar.gz file.
3. `chmod +x`: Makes the `xenblocksMiner` file executable.
4. `echo -e "...
..." |`: The `echo -e` command is used with `
` to simulate the Enter key. This part automatically inputs your EIP-55 address and dev fee into the miner.

## Customizing the Command

To use this command for your mining setup, replace `0xca5F023af4F822353A563Ae6a3591bA2024495E8` with your EIP-55 account address and `0` with your desired dev fee percentage.

For example:

```bash
echo -e "your_EIP-55_address_here
your_dev_fee_here" | ./xenblocksMiner
```

Replace `your_EIP-55_address_here` with your EIP-55 address and `your_dev_fee_here` with your desired dev fee.

## Disclaimer

This script assumes that the `xenblocksMiner` accepts input from standard input (stdin). If this is not the case, the script might not work as intended, and you might need to look for alternative ways to automate the process.
