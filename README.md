# Start Chainlink node for development
This repository contains [docker-compose](https://docs.docker.com/compose) scripts
to facilitate the creation of a [Chainlink](https://github.com/smartcontractkit/chainlink) node.

## Configuration

### Create an Ethereum node
Chainlink requires access to the websocket API of an Ethereum node.
It is possible to operate such a node locally or to use 3rd party services like
[alchemy](https://www.alchemy.com) or [infura](https://infura.io) for this purpose.

### Create an `.env` file

Create the `.env` based on the template and adjust it to your needs.
Most specifically the `ETH_URL` needs to be set to the websocket URL.
```
cp env.template chainlink-volume/.env
cd chainlink-volume
nano .env
```

### Set the API email and password
```
echo "user@example.com" > .api
echo "password" >> .api
```

### Set the wallet password
```
echo "my_wallet_password" > .password
```

## Start the Chainlink node

### Start the postgres database docker container
```
docker-compose -f db-compose.yml up
```
Note that this command also creates a docker network called `chainlink`
and a DB administration UI  reachable under the URL
[http://localhost:8090](http://localhost:8090)

### Start the chainlink docker container
```
docker-compose -f chainlink-compose.yml up
```
Afterwards, the Chainlink web UI will be reachable under the URL
[http://localhost:6688](http://localhost:6688)

## Stopping the Chainlink node
Shutting down the containers should happen in reverse order of startup:
```
docker-compose -f chainlink-compose.yml down
docker-compose -f db-compose.yml down
```