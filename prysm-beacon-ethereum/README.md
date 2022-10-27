# prism (prysmaticlabs) beacon chain node

# COMMAND

```
docker run -it -v $HOME/.eth2:/data -p 4000:4000 -p 13000:13000 -p 12000:12000/udp --name beacon-node \  gcr.io/prysmaticlabs/prysm/beacon-chain:stable \  --datadir=/data \  --jwt-secret=<YOUR_JWT_SECRET> \  --rpc-host=0.0.0.0 \  --grpc-gateway-host=0.0.0.0 \  --monitoring-host=0.0.0.0 \  --execution-endpoint=<YOUR_ETH_EXECUTION_NODE_ENDPOINT>
```
