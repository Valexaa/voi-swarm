# Docker Swarm Voi Participation node setup

## Prerequisites
- `curl` installed. If on a system without `curl` installed, follow applicable OS guidance for installing `curl`. 
- Ability to use `sudo`

## Supported OS and compute platforms
### OS
- Debian
- Ubuntu

### Compute platform
- arm64
- amd64 (x86_64)

## New to Voi
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/VoiNetwork/docker-swarm/main/install.sh)"
```

##  Have an existing account/address with mnemonic that you want to use
```bash
export VOINETWORK_IMPORT_ACCOUNT=1
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/VoiNetwork/docker-swarm/main/install.sh)"
```

## Want to install with no wallet setup included
```bash
export VOINETWORK_SKIP_WALLET_SETUP=1
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/VoiNetwork/docker-swarm/main/install.sh)"
```

## Set custom telemetry name
```bash
export VOINETWORK_TELEMETRY_NAME="my_custom_telemetry_name"
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/VoiNetwork/docker-swarm/main/install.sh)"
```
Custom telemetry name can be combined with other environment variables.

## Uninstalling
- `rm -rf ~/voi/algod`
- `docker stack rm voinetwork`
- `docker swarm leave --force`

## Useful scripts
This section of the README closely follows commands outlined in the excellent D13 guide for setting up a Voi participation
node under Ubuntu 22.04. The guide can be found here: https://d13.co/posts/set-up-voi-participation-node/

Commands are wrapped in shell scripts that execute into a running docking container.

### Creating a node wallet
```bash
~/voi/bin/create-wallet.sh <wallet_name>
```

### Creating an account
```bash
~/voi/bin/create-account.sh 
```

### Get account mnemonic
```bash
~/voi/bin/get-account-mnemonic.sh <account_address>
```

### Importing an account
```bash
~/voi/bin/import-account.sh
```

### Generating participation key
```bash
~/voi/bin/generate-participation-key.sh <account_address>
```

### Get account status
```bash
~/voi/bin/get-account-status.sh <account_address>
```

### Go online
```bash
~/voi/bin/go-online.sh <account_address>
```

### Go offline
```bash
~/voi/bin/go-offline.sh <account_address>
```

### Goal
```bash
~/voi/bin/goal.sh <goal_command>
```

### Open bash in AVM container
```bash
~/voi/bin/bash.sh
```

## Debugging
### Startup state for services in stack
`docker stack ps --no-trunc voinetwork`

### Replication state for services in stack
`docker service ls`

### Pull log files
`docker service logs voinetwork_algod`

### Inspect service
`docker inspect voinetwork_algod`

## TODO
- [ ] Add apprise / alarming on scaling events in docker-compose.yml
- [ ] Add participation key rotation
- [ ] Add mechanism for updating scripts and compose files (and swarm) on top of existing installation
- [ ] Adds script for participation key management