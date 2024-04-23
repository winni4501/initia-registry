# Initia Registry

This repo contains a `chain.json` and `assetlist.json` for a number of chains in Initia ecosystem. A `chain.json` contains data that makes it easy to start running or interacting with a node.

Schema files containing the recommended metadata structure can be found in the `*.schema.json` files located in the root directory. Schemas are still undergoing revision as user needs are surfaced. Optional fields may be added beyond what is contained in the schema files.

# How to add Minitia to registry

1. Fork this repo
2. Add a new directory with the name of the chain you want to add
3. Add a `chain.json` file with the metadata of the chain
4. Add an `assetlist.json` file with the metadata of the assets on the chain
5. Add an `initia-minitia.json` file with the metadata of the IBC connections and channels. The file name should be in alphabetical order of the chain names. Ex: `Achain-Bchain.json`.
6. Create a pull request

## chain.json

A sample chain.json includes the following information.

```json
{
  "$schema": "../../chain.schema.json",
  "chain_name": "minimove",
  "chain_id": "minimove-2",
  "website": "https://initia.xyz",
  "pretty_name": "Minimove",
  "status": "live",
  "network_type": "devnet",
  "bech32_prefix": "init",
  "daemon_name": "minitiad",
  "node_home": "$HOME/.minitia",
  "key_algos": ["secp256k1"],
  "slip44": 118,
  "fees": {
    "fee_tokens": [
      {
        "denom": "l2/2588fd87a8e081f6a557f43ff14f05dddf5e34cb27afcefd6eaf81f1daea30d0",
        "fixed_min_gas_price": 0.15,
        "low_gas_price": 0.15,
        "average_gas_price": 0.15,
        "high_gas_price": 0.4
      },
      {
        "denom": "ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5",
        "fixed_min_gas_price": 0.15,
        "low_gas_price": 0.15,
        "average_gas_price": 0.15,
        "high_gas_price": 0.4
      }
    ]
  },
  "staking": {
    "staking_tokens": []
  },
  "codebase": {
    "git_repo": "https://github.com/initia-labs/minimove",
    "recommended_version": "v0.2.3",
    "compatible_versions": ["v0.2.3", "main"],
    "binaries": {
      "linux/amd64": "https://initia.s3.ap-southeast-1.amazonaws.com/minimove-2/minimove_v0.2.3_Linux_x86_64.tar.gz",
      "linux/arm64": "https://initia.s3.ap-southeast-1.amazonaws.com/minimove-2/minimove_v0.2.3_Linux_aarch64.tar.gz",
      "darwin/amd64": "https://initia.s3.ap-southeast-1.amazonaws.com/minimove-2/minimove_v0.2.3_Darwin_x86_64.tar.gz",
      "darwin/arm64": "https://initia.s3.ap-southeast-1.amazonaws.com/minimove-2/minimove_v0.2.3_Darwin_aarch64.tar.gz"
    },
    "genesis": {
      "genesis_url": "https://initia.s3.ap-southeast-1.amazonaws.com/minimove-2/genesis.json"
    },
    "versions": []
  },
  "description": "Minimove Closed Devnet",
  "peers": {
    "seeds": [],
    "persistent_peers": []
  },
  "apis": {
    "rpc": [
      {
        "address": "https://rpc.minimove-2.initia.xyz",
        "provider": "Foundation"
      }
    ],
    "rest": [
      {
        "address": "https://lcd.minimove-2.initia.xyz",
        "provider": "Foundation"
      }
    ],
    "api": [
      {
        "address": "https://api.minimove-2.initia.xyz",
        "provider": "Foundation"
      }
    ],
    "grpc": [
      {
        "address": "grpc://34.124.237.204:9090",
        "provider": "Foundation"
      }
    ]
  },
  "explorers": [
    {
      "kind": "explorer",
      "url": "https://explorer.minimove-2.initia.xyz/?layer=minimove",
      "tx_page": "https://explorer.minimove-2.initia.xyz/tx/${txHash}?layer=minimove",
      "account_page": "https://explorer.minimove-2.initia.xyz/address/${accountAddress}?layer=minimove"
    },
    {
      "kind": "initia scan",
      "url": "https://scan.initia.xyz/minimove-2",
      "tx_page": "https://scan.initia.xyz/minimove-2/txs/${txHash}",
      "account_page": "https://scan.initia.xyz/minimove-2/accounts/${accountAddress}"
    }
  ],
  "images": [
    {
      "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.png",
      "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.svg"
    }
  ],
  "logo_URIs": {
    "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.png",
    "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.svg"
  },
  "metadata": {
    "op_bridge_id": "2",
    "op_denoms": ["uinit"],
    "ibc_channels": [
      {
        "chain_id": "mahalo-2",
        "port_id": "transfer",
        "channel_id": "channel-0",
        "version": "ics20-1"
      },
      {
        "chain_id": "mahalo-2",
        "port_id": "nft-transfer",
        "channel_id": "channel-1",
        "version": "ics721-1"
      }
    ],
    "assetlist": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/assetlist.json",
    "minitia": {
      "type": "minimove",
      "version": "v0.2.3"
    }
  }
}
```

## Assetlists

Asset Lists are inspired by the [Token Lists](https://tokenlists.org/) project on Ethereum which helps discoverability of ERC20 tokens by providing a mapping between erc20 contract addresses and their associated metadata.

Asset lists are a similar mechanism to allow frontends and other UIs to fetch metadata associated with Cosmos SDK denoms, especially for assets sent over IBC.

This standard is a work in progress. You'll notice that the format of assets in the assetlist.json structure is a strict superset json representation of the banktypes.DenomMetadata from the Cosmos SDK. This is purposefully done so that this standard may eventually be migrated into a Cosmos SDK module in the future, so it can be easily maintained on chain instead of on Github.

The assetlist JSON Schema can be found here.

An example assetlist json contains the following structure:

```json
{
  "$schema": "../../assetlist.schema.json",
  "chain_name": "minimove",
  "assets": [
    {
      "description": "The native token of Initia",
      "denom_units": [
        {
          "denom": "l2/2588fd87a8e081f6a557f43ff14f05dddf5e34cb27afcefd6eaf81f1daea30d0",
          "exponent": 0
        },
        {
          "denom": "INIT",
          "exponent": 6
        }
      ],
      "base": "l2/2588fd87a8e081f6a557f43ff14f05dddf5e34cb27afcefd6eaf81f1daea30d0",
      "display": "INIT",
      "name": "Initia Native Token",
      "symbol": "INIT",
      "coingecko_id": "",
      "images": [
        {
          "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.png",
          "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.svg"
        }
      ],
      "logo_URIs": {
        "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.png",
        "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/INIT.svg"
      }
    },
    {
      "description": "The fake USDC",
      "denom_units": [
        {
          "denom": "ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5",
          "exponent": 0
        },
        {
          "denom": "USDC",
          "exponent": 6
        }
      ],
      "base": "ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5",
      "display": "USDC",
      "name": "USDC",
      "symbol": "USDC",
      "coingecko_id": "",
      "images": [
        {
          "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/USDC.png",
          "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/USDC.svg"
        }
      ],
      "logo_URIs": {
        "png": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/USDC.png",
        "svg": "https://raw.githubusercontent.com/initia-labs/initia-registry/main/devnets/minimove/images/USDC.svg"
      }
    }
  ]
}
```

## IBC Data

The metadata contained in these files represents a path abstraction between two IBC-connected networks. This information is particularly useful when relaying packets and acknowledgments across chains.

This schema also allows us to provide helpful info to describe open channels.

Note: when creating these files, please ensure the chains in both the file name and the references of `chain-1` and `chain-2` in the json file are in alphabetical order. Ex: `Achain-Zchain.json`. The chain names used must match name of the chain's directory here in the chain-registry.

An example ibc metadata file contains the following structure:

```json
{
  "$schema": "../../ibc_data.schema.json",
  "chain_1": {
    "chain_name": "initia",
    "client_id": "07-tendermint-0",
    "connection_id": "connection-0"
  },
  "chain_2": {
    "chain_name": "minimove",
    "client_id": "07-tendermint-0",
    "connection_id": "connection-0"
  },
  "channels": [
    {
      "chain_1": {
        "channel_id": "channel-0",
        "port_id": "transfer"
      },
      "chain_2": {
        "channel_id": "channel-0",
        "port_id": "transfer"
      },
      "ordering": "unordered",
      "version": "ics20-1",
      "tags": {
        "status": "live",
        "preferred": true
      }
    }
  ]
}
```