## Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```

# Project README

## Check Updates

To check versions of Forge, Cast, and Avnil, use the following commands:

```bash
Forge --version
Cast --version
Avnil --version
```

## Foundry Initialization

Initialize the Forge project with:

```bash
forge init
```

## Compilation

After writing the smart contract code, compile it using the following commands:

```bash
forge compile --force
```

After compilation, a JSON file will be generated.

**RESULT:** Compiler run successful!

## Local Blockchain

Start the Anvil local blockchain and connect with Metamask using the "add network" option.

```bash
anvil
```

## Deployment of Contract without Scripts

Deploy a contract using the following command:

```bash
forge create SimpleStorage --rpc-url http://127.0.0.1:8545 --private-key 0xac09a…974b
```

**RESULT:**

```
Deployer: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Deployed to: 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
Transaction hash: 0xb6867eaecf2335d70c61ff7c0a204cd1acb55dd811f6282543c077c66aee06d0
```

## Deployment of Contract with Scripts

Write the script first, then run the deployment script using one of the following commands:

```bash
forge script script/DeploySimpleStorage.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --private-key 0xac0….2ff80
```

OR

```bash
forge script script/DeploySimpleStorage.s.sol --fork-url $RPC_URL --broadcast --private-key $PRIVATE_KEY
```

**RESULT:** Script ran successfully.

```
Gas used: 338569
== Return ==
0: contract SimpleStorage 0x90…98A1
…
ONCHAIN EXECUTION COMPLETE & SUCCESSFUL.
Total Paid: 0.001428352 ETH (357088 gas * avg 4 gwei)
```

## Help

For help on Forge and related commands, use the following:

```bash
forge --help
forge create --help
cast --help
```

## Convert Gas Fee (Hex to Dec)

To convert the gas fee from hex to decimal, use the following command:

```bash
cast --to-base 0x714e1 dec
```

## Use Functions of the Smart Contract

### For Writing in Contract

```bash
cast send 0xCf7….Fc9 "store(uint256)" 123 --rpc-url http://127.0.0.1:8545 --private-key 0xac….ff80
```

**RESULT:**

```
blockHash               0x8d….83c
…
type                    2
```

### For Reading the Contract

```bash
cast call 0xCf7…0Fc9 "retrieve()" --rpc-url http://127.0.0.1:8545 --private-key 0xac09…f80
```

**RESULT:** `0x07b`

To convert the result to decimal:

```bash
cast --to-base 0x07b dec
```

**RESULT:** `123`

## Smart Contract Auto Format

Auto format the smart contract code using the following command:

```bash
forge fmt
```
# Project Readme

## Environment Setup

Before running the smart contract tests, make sure to set up the environment as follows:

1. Check your environment variables:
   ```bash
   Checking ENV
   source .env
   ```

2. Confirm the SEPOLIA_URL is correctly set:
   ```bash
   echo $SEPOLIA_URL
   ```

## Smart Contract Testing

To run smart contract tests, use the following commands:

1. Basic test:
   ```bash
   forge test -vvv --fork-url $SEPOLIA_URL
   ```

2. Specific test (e.g., testPriceFeedVersionIsAccurate):
   ```bash
   forge test -m testPriceFeedVersionIsAccurate -vvv --fork-url $SEPOLIA_URL
   ```

3. Coverage (for better test coverage):
   ```bash
   forge coverage --fork-url $SEPOLIA_URL
   ```

## Installation of Smart Contract Dependencies

Install smart contract dependencies using the following command:

```bash
forge install smartcontractkit/chainlink-brownie-contracts@0.8.0 --no-commit
```

## Checking Gas Fee and Storage

### Checking Gas Fee

To check the gas fee of a specific function using .gas-snapshot, follow these steps:

1. Create a snapshot for a test function (e.g., testfunctionname):
   ```bash
   forge snapshot -m testfunctionname
   ```

2. Example code snippet for gas usage:
   ```solidity
   uint256 public constant GAS_PRICE = 1;
   vm.txGasPrice(GAS_PRICE);
   uint256 gasStart = gasleft();
   vm.prank(fundMe.getOwner());
   fundMe.withdraw();
   uint256 gasEnd = gasleft();
   uint256 gasUsed = (gasStart - gasEnd) * tx.gasprice;
   console.log(gasUsed);
   ```

### Checking Storage

To inspect the storage layout of a contract variable (e.g., FundMe), use the following command:

```bash
forge inspect FundMe storageLayout
```

### Deploying Simple Storage Contract

To deploy a SimpleStorage contract script, execute the following command:

```bash
forge script script/DeploySimpleStorage.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --private-key 0xac0….2ff80
```

Take note of the deployed contract address (e.g., 0xfdj..sfjfo) for further operations.

### Casting Storage (For Indexing in Storage Array)

To cast storage for indexing in a storage array, use the following command:

```bash
forge cast-storage 0xfdj..sfjfo 2
```

Replace 0xfdj..sfjfo with the actual contract address and 2 with the desired index for storage array.
