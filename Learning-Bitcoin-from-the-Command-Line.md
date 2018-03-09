## [Learning-Bitcoin-from-the-Command-Line](https://github.com/ChristopherA/Learning-Bitcoin-from-the-Command-Line/)
- btcblock
- ~/.bitcoin
  * bitcoin.conf
  * testnet3
    + banlist.dat
    + blocks
    + database
    + debug.log
    + wallet.dat
    + bitcoind.pid
    + chainstate
    + db.log
    + peers.dat
- bitcoin-cli
  * bitcoin-cli help
  * bitcoin-cli help getmininginfo
  * bitcoin-cli getblockchaininfo
  * bitcoin-cli getmininginfo
  * bitcoin-cli getnetworkinfo
  * bitcoin-cli getnettotals
  * bitcoin-cli getwalletinfo
  * bitcoin-cli signmessage [address] [message]
    + bitcoin-cli signmessage "n4cqjJE6fqcmeWpftygwPoKMMDva6BpyHf" "Hello, World"
      - H3yMBZaFeSmG2HgnH38dImzZAwAQADcOiMKTC1fryoV6Y93BelqzDMTCqNcFoik86E8qHa6o3FCmTsxWD7Wa5YY=
  * bitcoin-cli verifymessage [address] [message]
    + bitcoin-cli verifymessage "n4cqjJE6fqcmeWpftygwPoKMMDva6BpyHf" "H3yMBZaFeSmG2HgnH38dImzZAwAQADcOiMKTC1fryoV6Y93BelqzDMTCqNcFoik86E8qHa6o3FCmTsxWD7Wa5YY=" "Hello, World"
      - true
  * bitcoin-cli backupwallet backup.dat
  * bitcoin-cli importwallet backup.dat
  * bitcoin-cli dumpwallet ~/mywallet.txt
  * bitcoin-cli dumpprivkey "n4cqjJE6fqcmeWpftygwPoKMMDva6BpyHf"
  * bitcoin-cli importprivkey cW4s4MdW7BkUmqiKgYzSJdmvnzq8QDrf6gszPMC7eLmfcdoRHtHh
  * bitcoin-cli getnewaddress
    + $ unset NEW_ADDRESS_1
    + $ NEW_ADDRESS_1=$(bitcoin-cli getnewaddress)
