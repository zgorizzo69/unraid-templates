# openethereum

# COMMAND

```
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='open-ethereum' --net='bridge' -e TZ="America/Los_Angeles" -e HOST_OS="Unraid" -p '8545:8545/tcp' -p '8546:8546/tcp' -p '30303:30303/tcp' -p '30303:30303/udp' -v '/mnt/user/docker/':'/home/openethereum/.local/share/openethereum/':'rw' 'openethereum/openethereum' --base-path /home/openethereum/.local/share/openethereum/ --config /home/openethereum/.local/share/openethereum/config.toml
```
