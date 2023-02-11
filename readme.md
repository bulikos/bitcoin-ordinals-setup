### Install BitcoinCore

Download and install 

1. Make and enter directory for following actions.
- `mkdir btc1` and `cd btc1`

2. Download bitcoin core tar archive.
- `curl -O https://bitcoincore.org/bin/bitcoin-core-24.0.1/bitcoin-24.0.1-x86_64-linux-gnu.tar.gz`

3. Unpack archive 
- `tar xzf bitcoin-24.0.1-x86_64-linux-gnu.tar.gz`

4. Install. You may need sudo access (add `sudo` before the command).
- `install -m 0755 -o root -g root -t /usr/local/bin bitcoin-24.0.1/bin/*`

5. Verify instalation by succuessfully running.
- `bitcoind -version`

### Configure and run BitcoinCore
Here are two options, either setup a daemon running the program in background, or run the program directly in terminal window. The `tx-index` option used in both options will download all transactions (not only blocks) to local disk using the `$HOME/.bitcoin` direcotory, make sure to have at least +500GB of free space.

- Run daemon option:
  - Start daemon process - `bitcoind -txindex -daemon`
  - To stop the daemon use `bitcoin-cli stop`
- Run program directly option:
  - Start program `bitcoind -txindex`.
  - To stop the program close the terminal or use CTRL+C keys.

#### Check status
After starting the BitcoinCore you can check status of synchronization (downloading all blocks and txs to your disk) with command `bitcoin-cli getblockcount`, this number should within several hours match the current blockchain heigh (which can be found somewhere online).
