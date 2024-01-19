
# XENBLOCKS - Effortless GPU Mining with 1 line of Code
Learn how to automate the XenBlocks Miner using a single command line that automatically prefills your ETH address as well as Dev Fee.

## One-Liner Command

The command provided below automates the process of downloading, extracting, making the XenBlocks Miner executable, and running it with predefined user inputs (EIP-55 address and dev fee).

```bash
wget https://github.com/woodysoil/XenblocksMiner/releases/download/v1.1/xenblocksMiner-v1.1.1-Linux-x86_64.tar.gz && tar -vxzf xenblocksMiner-v1.1.1-Linux-x86_64.tar.gz && chmod +x xenblocksMiner && echo -e "0xca5F023af4F822353A563Ae6a3591bA2024495E8\n0" | ./xenblocksMiner
```

## Video Demo
https://github.com/JozefJarosciak/X1/assets/3492464/3a061c84-4422-44b8-b25f-0315bc6d3142


## How It Works

1. `wget`: Downloads the XenBlocks Miner tarball from the provided GitHub link.
2. `tar -vxzf`: Extracts the downloaded tar.gz file.
3. `chmod +x`: Makes the `xenblocksMiner` file executable.
4. `echo -e "...
..." |`: The `echo -e` command is simulating the Enter key. This part automatically inputs your EIP-55 address and dev fee into the miner.

## Customizing the Command

To use this command for your mining setup, replace `0xca5F023af4F822353A563Ae6a3591bA2024495E8` with your EIP-55 account address and `0` with your desired dev fee percentage.

Example:

![image](https://github.com/JozefJarosciak/X1/assets/3492464/1d867356-8e02-41c5-8fe8-5b28f1d8b36d)
