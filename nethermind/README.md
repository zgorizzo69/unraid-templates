# geth-ethereum

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='nethermind-ethereum' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -e HOST_HOSTNAME="BorgCube" -e HOST_CONTAINERNAME="nethermind-ethereum" -e 'NETHERMIND_INITCONFIG_ISMINING'='false' -e 'NETHERMIND_JSONRPCCONFIG_ENABLED'='true' -e 'NETHERMIND_JSONRPCCONFIG_HOST'='0.0.0.0'  -e 'NETHERMIND_JSONRPCCONFIG_ENGINEHOST'='0.0.0.0' -e 'NETHERMIND_JSONRPCCONFIG_ENGINEPORT'='8551' -e 'NETHERMIND_JSONRPCCONFIG_JWTSECRETFILE'='/nethermind/data/keystore/jwt-secret/jwt.hex' -l net.unraid.docker.managed=dockerman -l net.unraid.docker.icon='https://nethermind.io/wp-content/themes/nethermind/images/logo.svg' -p '8545:8545/tcp' -p '8546:8546/tcp' -p '30303:30303/tcp' -p '30303:30303/udp' -v '/mnt/user/blockchain/ethereum/':'/nethermind/data':'rw' 'nethermind/nethermind' --datadir data
 
```
 