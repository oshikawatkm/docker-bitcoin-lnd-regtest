# bitcoind & lnd simnet遊び

## bitcoind 側のコマンド
### ウォレット作成 & 残高確認
```
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass createwallet miner
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner getbalance
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner getwalletinfo
```

### マイニング
```
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner getnewaddress "miner" bech32
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner generatetoaddress 101 <MINER_ADDR>
```

### Alice/Bob への送金
```
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner sendtoaddress <ALICE_ADDR> 10
bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass -rpcwallet=miner generatetoaddress 1 <MINER_ADDR>
```

## Alice 側のコマンド
### ウォレット操作
```
lncli --network=regtest --rpcserver=localhost:10009 create
lncli --network=regtest --rpcserver=localhost:10009 getinfo
lncli --network=regtest --rpcserver=localhost:10009 walletbalance
lncli --network=regtest --rpcserver=localhost:10009 newaddress p2tr
```

### チャネル操作
```
lncli --network=regtest --rpcserver=localhost:10009 connect <BOB_PUBKEY>@bob:9736
lncli --network=regtest --rpcserver=localhost:10009 openchannel <BOB_PUBKEY> 1000000
lncli --network=regtest --rpcserver=localhost:10009 listchannels
lncli --network=regtest --rpcserver=localhost:10009 channelbalance
lncli --network=regtest --rpcserver=localhost:10009 closechannel --funding_txid=<TXID> --output_index=0
```

### 支払い
```
lncli --network=regtest --rpcserver=localhost:10009 payinvoice <PAYMENT_REQUEST>
```

## Bob 側のコマンド
### ウォレット操作
```
lncli --network=regtest --rpcserver=localhost:10010 create
lncli --network=regtest --rpcserver=localhost:10010 getinfo
lncli --network=regtest --rpcserver=localhost:10010 walletbalance
lncli --network=regtest --rpcserver=localhost:10010 newaddress p2tr
```

### チャネル操作
```
lncli --network=regtest --rpcserver=localhost:10010 listchannels
lncli --network=regtest --rpcserver=localhost:10010 channelbalance
```

### Invoice 発行
```
lncli --network=regtest --rpcserver=localhost:10010 addinvoice 50000
```