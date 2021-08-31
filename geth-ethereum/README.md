# geth-ethereum

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='geth-ethereum' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -p '8545:8545/tcp' -p '8546:8546/tcp' -p '30303:30303/tcp' -p '30303:30303/udp' -v '/mnt/user/blockchain/ethereum/':'/root/.ethereum':'rw' 'ethereum/client-go' --http --http.corsdomain localhost --ws --ws.origins localhost --ipcdisable
```

# Blockchain sync mode

in the `Post Arguments` field you can set the sync mode to "fast", "full", "snap" or "light") (default: snap)

```
 --syncmode  ("fast", "full", "snap" or "light")
```

Full node

- Stores full blockchain data.
- Participates in block validation, verifies all blocks and states.
- All states can be derived from a full node.
- Serves the network and provides data on request.

Light node

- Stores the header chain and requests everything else.
- Can verify the validity of the data against the state roots in the block headers.
- Useful for low capacity devices, such as embedded devices or mobile phones, which can't afford to store gigabytes of blockchain data.

Archive node

you can also tweak the Blockchain garbage collection mode to "full" or "archive") (default: "full")

```
 --gcmode ("full" or "archive")
```

an archive node is very heavy on memory (+1.2To). It stores everything kept in the full node and builds an archive of historical states. Needed if you want to query something like an account balance at block #4,000,000, or simply and reliably test your own transactions set without mining them using hardhat for instance.

# Make my node accessible

you can use for instance `nginxproxymanager` to add a proxy host like `https://my.eth.node` where the destination is your unraid server to port `8545`

then inside the `Post Arguments` field you write this

```
--http
--http.addr 0.0.0.0
--http.corsdomain moz-extension://546546df-564654-fd87f8776729356,http://localhost,https://remix.ethereum.org,http://my.unraid.server.home,https://my.eth.node
--http.vhosts=localhost,192.168.1.42,my.unraid.server.home,my.eth.node
```

now you can access your node from your metamask extension thanks to the `moz-extension://546546df-564654-fd87f8776729356` don't forget to replace the id `546546df-564654-fd87f8776729356` with yours.
you also can access it from `http://my.unraid.server.home` and `https://my.eth.node`
try

```
curl --data '{"method":"eth_syncing","params":[],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST my.unraid.server.home:8545
curl --data '{"method":"web3_clientVersion","params":[],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST https://my.eth.node

```

you could also enable the websocket and disable the IPC. Add a proxy host like `https://ws.my.eth.node` where the destination is your unraid server to port `8546`

```
--ws
--ws.addr 0.0.0.0
--ws.origins http://localhost,https://remix.ethereum.org,http:///my.unraid.server.home,https://ws.my.eth.node
--ipcdisable
```

and you can try with

```
wscat -c ws://my.unraid.server.home:8546
Connected (press CTRL+C to quit)

{"method":"eth_syncing","params":[],"id":1,"jsonrpc":"2.0"}
< {"jsonrpc":"2.0","id":1,"result":{"currentBlock":"0x6fd147","highestBlock":"0xc86d74","knownStates":"0x0","pulledStates":"0x0","startingBlock":"0x6a5d40"}}
```

## Graphql

You can enable GraphQL on the HTTP-RPC server. Note that GraphQL can only be started if an HTTP server is started as well.
You can query things like

- blocks
- pending
- transaction
- logs
- gasPrice
- protocolVersion
- syncing
- chainID

you need to add these lines

```
--graphql
--graphql.corsdomain http://localhost,https://remix.ethereum.org,http://my.unraid.server.home,https://my.eth.node
--graphql.vhosts localhost,192.168.1.42,my.unraid.server.home,my.eth.node
```

here is the [full schema](https://eips.ethereum.org/EIPS/eip-1767#schema)

it will start a UI at `http://my.unraid.server.home:8545/graphql/ui`
