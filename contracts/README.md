# @dgrants/contracts

[hardhat](https://hardhat.org/getting-started/) is the environment used to compile, deploy, test and debug the dGrants contract.

## Usage

### Pre Requisites

Before running any command, make sure to install dependencies:

```sh
$ yarn install
```

### Compile

Compile the smart contracts with Hardhat:

```sh
$ yarn build
```

### TypeChain

Compile the smart contracts and generate TypeChain artifacts:

```sh
$ yarn typechain
```

### Lint Solidity

Lint the Solidity code:

```sh
$ yarn lint:sol
```

### Lint TypeScript

Lint the TypeScript code:

```sh
$ yarn lint:ts
```

### Test

Run the Mocha tests:

```sh
$ yarn test
```

### Coverage

Generate the code coverage report:

```sh
$ yarn coverage
```

### Report Gas

See the gas usage per unit test and average gas per method call:

```sh
$ REPORT_GAS=true yarn test
```

### Clean

Delete the smart contract artifacts, the coverage reports and the Hardhat cache:

```sh
$ yarn clean
```

### Deployment

To test deploying the contracts locally, first start a localhost hardhat network.

```sh
$ yarn app:node
```

Now, in another console, deploy the contracts to the local hardhat fork.

```sh
$ yarn deploy:poc --network localhost
```

You will now have a timestamped file in `./deploy-history` containing the log output of this deployment prefixed with `poc-localhost-`. You'll also see the `poc-localhost-latest.json` file. The `-latest.json` file for each network is overwritten each time the command runs. Deployments to localhost are ignored and should not be committed to the repo.

To deploy to a "real" network like mainnet or a testnet, replace the network name, as defined in `hardhat.config.ts`.

```sh
$ yarn deploy:poc --network mainnet
```

The log files created will follow the same pattern, but will be prefixed with `mainnet` as expected.
These files can and should be committed to the repo as artifacts of deployment history.

You must configure various deployment parameters on a per-network basis in the `./scripts/deploy-poc.config.ts` file.

You can configure the metadata that will be published and used for the Round by editing the `./scripts/grant-round-metadata.json`. The entire contents of the file are uploaded and published.

NOTE: Before deploying to the desired network, make sure `roundStartTime` in `scripts/config/deploy-poc.config.ts` is set to a start time in the future.

### Update Script

The repo contains a script which automates the update of a `GrantRound`'s metadata.

To test the metadata update locally, first start a localhost hardhat network.

```sh
$ yarn app:node
```

Now, in another console, run the deploy script to deploy the system.

```sh
$ yarn deploy:poc --network localhost
```

Now run the update script.

```sh
$ yarn update:round --network localhost
```

As with the deployment logging output described above, you will now have a timestamped file in `./deploy-history` containing the log output of this script's execution.

In the same way, you can configure this update script by editing the `./scripts/update-round.config.ts` file, and configure the metadata that will be published during the update by editing the `./scripts/grant-round-metadata.json`.

To update a round on a "real" network like mainnet or a testnet, replace the network name, as defined in `hardhat.config.ts`.

```sh
$ yarn update:round --network mainnet
```

### Hardhat console

To access the console once the hardhat network is running on your local machine.

```sh
$ npx hardhat console
```
