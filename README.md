# Bounty Submission

> Kindly find the link to the contract address deployed in the Axelar Testnet here: https://testnet.axelarscan.io/gmp/0x42000eb9ebe892081c8ce65d25e3a1c5c78564e2c27e100684c568184f814dee

---

## How to Run this Application:

- Clone the repo:

  In your terminal run the command `git clone https://github.com/midesofek/Axelar-CrossChain-Transfer-dApp.git`

- Install the Dependencies:

  run `yarn install`

- Compile the contracts:

  run `yarn hardhat compile`

- Setup a deployer key:

  Create a `.env` file & add your EVM private key.
  _Inside your `.env` file add your private key_
  `    EVM_PRIVATE_KEY = 'INSERT YOUR PRIVATE KEY'`

- Deploy locally:

  Spin up a local dev environment on your PC by running:
  `node scripts/createLocal`

  Then deploy your contracts locally:

  `node scripts/deploy examples/call-contract-with-token local`

- Run tests in your local environment:

  Test locally:

  Pass in the following parameters:

  `node scripts/test examples/call-contract-with-token [local|testnet] ${"source-chain"} ${"destination-chain"} ${amount} ${account} ${account2} ...`

  Run the test:

  `node scripts/test examples/call-contract-with-token local "Moonbeam" "Polygon" 100 0x1339514086Fc15C5e38AF4E0407C469Ca3911992 "Hello Fren"`

### Deploy & Test on a Live Testnet

- Deploy your contract on Testnets (provided in the `info/testnet.json` file):

  `node scripts/deploy examples/call-contract-with-token testnet`

> N.B: Ensure you have sufficient test tokens of each chain in your wallet

- Run the cross-chain transfer:

  Pass in the following parameters:

  `node scripts/test examples/call-contract-with-token [testnet] ${"source-chain"} ${"destination-chain"} ${amount} ${account} ${account2} `

  Run the test:

  `node scripts/test examples/call-contract-with-token testnet "Ethereum" "Polygon" 100 0x1339514086Fc15C5e38AF4E0407C469Ca3911992 "Hello Fren"`

> N.B: Ensure you have the specified amout of `aUSDC token` before triggering this function. You can get this token from [**Axelar-Discord**](https://discord.gg/axelar)

## Implementations & Modifications

Firstly, a hardhat project was setup and the necessary contracts ( under `call-contract-with-token`) and scripts were imported from the [**axelar-local-gmp-examples repo**](https://github.com/axelarnetwork/axelar-local-gmp-examples)

Then, the `sendToMany` function in the `DistributionExecutable.sol` solidity contract was modified to take an extra string parameter named `message`.

The message was encoded along with the receipient wallet address and parsed as bytes in the payload variable.

Also the `_executeWithToken` function, in the same contract, was modified to decode the address and the message.

Finally, to align the implementations , the `index.js` file under `examples/call-contract-with-token`was modified to reflect the changes made to the contract and to properly deploy the contract and run tests. In doing this, the new string `message` parameter was parsed as one of the arguments required in the `sendToMany` function.  

