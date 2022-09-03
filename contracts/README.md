# MerkleClaimERC20

ERC20 token claimable by members of a [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree). Useful for conducting Airdrops. Utilizes [Solmate ERC20](https://github.com/Rari-Capital/solmate/blob/main/src/tokens/ERC20.sol) for modern ERC20 token implementation.

## Test
import { HardhatUserConfig } from 'hardhat/config';
import '@nomiclabs/hardhat-ethers';
import '@nomiclabs/hardhat-waffle';
import '@nomiclabs/hardhat-solhint';
import 'hardhat-typechain';
import "@nomiclabs/hardhat-etherscan";

import * as dotenv from 'dotenv';
dotenv.config();

const alchemyAPIKey = process.env.ALCHEMY_API_KEY;
const deployerPrivateKey = process.env.DEPLOYER_PRIVATE_KEY;

const config: HardhatUserConfig = {
  defaultNetwork: 'hardhat',
  solidity: {
    version: '0.8.4',
    settings: {
      optimizer: {
        enabled: true,
        runs: 2000
      }
    }
  },
  typechain: {
    outDir: 'ts-types/contracts',
    target: 'ethers-v5'
  },
  networks: {
    rinkeby: {
      url: `http://eth-rinkeby.alchemyapi.io/v2/${alchemyAPIKey}`,
      accounts: [deployerPrivateKey],
    },
    mainnet: {
      url: `https://eth-mainnet.alchemyapi.io/v2/${alchemyAPIKey}`,
      accounts: [deployerPrivateKey],
    },
    polygonMumbai: {
      url: `https://polygon-mumbai.g.alchemy.com/v2/${alchemyAPIKey}`,
      accounts: [deployerPrivateKey],
    },
  },
  etherscan: {
    apiKey: {
        mainnet: "YOUR_ETHERSCAN_API_KEY",
        ropsten: "YOUR_ETHERSCAN_API_KEY",
        rinkeby: "YOUR_ETHERSCAN_API_KEY",
        goerli: "YOUR_ETHERSCAN_API_KEY",
        kovan: "YOUR_ETHERSCAN_API_KEY",
       
        // polygon
        polygon: "5GT5IQNDSN2FNJ56KSZNXJ97B3E7Z4K4GW",
        polygonMumbai: "5GT5IQNDSN2FNJ56KSZNXJ97B3E7Z4K4GW",
    }
  }
};

export default config;
Tests use [Foundry: Forge](https://github.com/gakonst/foundry).

Install Foundry using the installation steps in the README of the linked repo.

### Run tests

```bash
# Go to contracts directory, if not already there
cd contracts/

# Get dependencies
forge update

# Run tests
forge test --root .
# Run tests with stack traces
forge test --root . -vvvv
```

## Deploy

Follow the `forge create` instructions ([CLI README](https://github.com/gakonst/foundry/blob/master/cli/README.md#build)) to deploy your contracts or use [Remix](https://remix.ethereum.org/).

You can specify the token `name`, `symbol`, `decimals`, and airdrop `merkleRoot` upon deploy.

## Credits

- [@brockelmore](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/issues?q=is%3Apr+author%3Abrockelmore) for [#1](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/pull/1)
- [@transmissions11](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/issues?q=is%3Apr+author%3Atransmissions11) for [#2](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/pull/2)
- [@devanonon](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/issues?q=is%3Apr+author%3Adevanonon) for [#3](https://github.com/Anish-Agnihotri/merkle-airdrop-starter/pull/8)
