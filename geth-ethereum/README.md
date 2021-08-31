# geth-ethereum

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='geth-ethereum' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -p '8545:8545/tcp' -p '8546:8546/tcp' -p '30303:30303/tcp' -p '30303:30303/udp' -v '/mnt/user/blockchain/ethereum/':'/root/.ethereum':'rw' 'ethereum/client-go'
```
