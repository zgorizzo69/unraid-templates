# geth-ethereum

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='geth-ethereum' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -p '8545:8545/tcp' -p '8546:8546/tcp' -p '30303:30303/tcp' -p '30303:30303/udp' -v '/mnt/user/blockchain/ethereum/':'/root/.ethereum':'rw' 'ethereum/client-go' --http --http.corsdomain localhost --ws --ws.origins localhost --ipcdisable
```

# Make my node accessible

you can use for instance `nginxproxymanager` to add a proxy host like `https://my.eth.node` where the destination is your unraid server to port `8545`

then inside the `Post Arguments` field you write this

```
--http --http.addr 0.0.0.0 --http.corsdomain moz-extension://546546df-564654-fd87f8776729356,http://localhost,https://remix.ethereum.org,http://my.unraid.server.home,https://my.eth.node --http.vhosts=localhost,192.168.1.42,my.unraid.server.home,my.eth.node
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
--ws --ws.addr 0.0.0.0 --ws.origins http://localhost,https://remix.ethereum.org,http:///my.unraid.server.home,https://ws.my.eth.node --ipcdisable
```
