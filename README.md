![Base](logo.png)

# Base node

Base is a secure, low-cost, developer-friendly Ethereum L2 built to bring the next billion users to web3. It's built on Optimism’s open-source [OP Stack](https://optimism.io).

This repository contains the relevant Docker builds to run your own node on the Base network.

### Supported networks

| Ethereum Network | Status |
|------------------|--------|
| Goerli testnet   | ✅      |
| Mainnet          | 🚧     |


### Usage

1. Ensure you have an Goerli L1 node RPC available, and set `OP_NODE_L1_ETH_RPC` (in `docker-compose.yml` if using docker-compose).
2. Run:
```
docker-compose up
```
3. You should now be able to `curl` your Base node:
```
curl -d '{"id":0,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' \
  -H "Content-Type: application/json" http://localhost:8545
```

### Syncing

Sync speed depends on your L1 node, as the majority of the chain is derived from data submitted to the L1. You can check your syncing status using the `optimism_syncStatus` RPC on the `op-node` container. Example:
```
echo Latest synced block behind by: $((($(date +%s)-$( \
  curl -d '{"id":0,"jsonrpc":"2.0","method":"optimism_syncStatus"}' \
  -H "Content-Type: application/json" http://localhost:7545 | \
  jq -r .result.unsafe_l2.timestamp))/60)) minutes
```
