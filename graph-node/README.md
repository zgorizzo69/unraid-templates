# graph-node

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='graph-node' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -p '8000:8000/tcp' -p '8020:8020/tcp' -p '8001:8001/tcp' 'graphprotocol/graph-node' --release --postgres-url postgresql://USERNAME[:PASSWORD]@localhost:5432/graph-node --ethereum-rpc localhost:8545 --ipfs localhost:5001
```

### Running a Local Graph Node

These are the prerequisites.

1. Install IPFS fill the ipfs url in the arguments `--ipfs localhost:5001`.
2. Install PostgreSQL and fill the url in the arguments `--postgres-url postgresql://USERNAME[:PASSWORD]@localhost:5432/graph-node`.
