# Bitcoin Ordinals
This document is extended guide to help you produce your first [ordinal](https://ordinals.com/). I highly recommend to first browse the original [ordinals handbook](https://docs.ordinals.com/).

## BitcoinCore
BitcoinCore is a Bitcoin node software, which is going to serve the requests from orb wallet. Let's start with installing and running BitcoinCore.

### Install BitcoinCore
Download and install 

1. Make and enter directory for following actions.
- `mkdir btc1` and `cd btc1`

2. Download BitcoinCore tar archive.
- `curl -O https://bitcoincore.org/bin/bitcoin-core-24.0.1/bitcoin-24.0.1-x86_64-linux-gnu.tar.gz`

3. Unpack archive 
- `tar xzf bitcoin-24.0.1-x86_64-linux-gnu.tar.gz`

4. Install. You may need sudo access (add `sudo` before the command).
- `install -m 0755 -o root -g root -t /usr/local/bin bitcoin-24.0.1/bin/*`

5. Verify instalation by succuessfully running.
- `bitcoind -version`

### Configure and run BitcoinCore
Here are two options, either setup a daemon running the program in background, or run the program directly in terminal window. The `tx-index` option used in both options will download all transactions (not only blocks) to local disk using the `$HOME/.bitcoin` direcotory, make sure to have at least +500GB of free space. This option is mandatory for orb wallet, as the wallet later based on this transactions builds index of satoshis.

- Run daemon option:
  - Start daemon process - `bitcoind -txindex -daemon`
  - To stop the daemon use `bitcoin-cli stop`
- Run program directly option:
  - Start program `bitcoind -txindex`.
  - To stop the program close the terminal or use CTRL+C keys.

#### Check status
After starting the BitcoinCore you can check status of synchronization (downloading all blocks and txs to your disk) with command `bitcoin-cli getblockcount`, this number should within several hours match the current blockchain height (which can be found somewhere online).

## Orb wallet
Once we have sucuessfully started and synced the Bitcoin node we can start working with orb wallet.

### Install Orb and prepare wallet

1. Download and install orb wallet
- `curl --proto '=https' --tlsv1.2 -fsLS https://ordinals.com/install.sh | bash -s`

2. Verifiy installation by priting ord version.
- `ord --version`

3. For those getting the Command 'ord' not found error. Navigate to bin folder inside your home directory - `cd $HOME/bin` and try running `./ord --version`. If it helped, hold on inside this directory and always use `./orb` instead of the `orb` in following commands. 

4. Prepare wallet (its recommended to create a new one).
- `ord wallet create`, remember to save you seed phrase.

5. Fund the wallet by generating new address and sending some funds from your other wallet or CEX.
- Generate receiving address `ord wallet receive`

6. Check status of transactions
- `ord wallet transactions` and `ord wallet outputs`

### Build orb index
1. To produce ordinals the ord first needs to build an index. In my case this operation took more time than syncing the BitcoinCore. The command will show you the current progress.
- `ord index`