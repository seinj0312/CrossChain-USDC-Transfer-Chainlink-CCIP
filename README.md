# Cross-Chain Tokens Using Chainlink CCIP

Explore the integration of Chainlink to conduct USDC transfers between Avalanche Fuji and Ethereum Sepolia networks. This repository includes detailed instructions on setting up wallets, adding tokens, and deploying a contract to facilitate the cross-chain transfer of USDC using Chainlink's CCIP.

## Table of Contents

1. [Setup](#setup)
2. [Adding LINK and USDC Tokens](#adding-link-and-usdc-tokens)
3. [Smart Contract Deployment](#smart-contract-deployment)
4. [Interacting with the Contract](#interacting-with-the-contract)
5. [Monitoring Transactions](#monitoring-transactions)

## Step 1: Setup

### Avalanche Fuji and Ethereum Sepolia
- **MetaMask Configuration**:
  - Ensure MetaMask is installed and set up for both Avalanche Fuji and Ethereum Sepolia.
    - [Add Fuji to MetaMask](https://chainlist.org/chain/43113)
    - Sepolia details are available at [Chainlink Documentation](https://docs.chain.link/resources/link-token-contracts#sepolia-testnet).

### Remix IDE
- Access the Remix IDE for smart contract deployment: [Remix](https://remix.ethereum.org/)
  - Set the environment to `Injected provider - MetaMask` and confirm connection to the Fuji network.

## Adding LINK and USDC Tokens

### Add Tokens to MetaMask
- **LINK Token**:
  - Avalanche Fuji: [LINK on Fuji](https://docs.chain.link/resources/link-token-contracts#fuji-testnet)
  - Ethereum Sepolia: [LINK on Sepolia](https://docs.chain.link/resources/link-token-contracts#sepolia-testnet)
- **USDC Token**:
  - Add USDC on Avalanche Fuji following instructions from [Circle Developers](https://developers.circle.com/stablecoins/docs/usdc-on-test-networks)

### Faucets
- Obtain LINK and AVAX for Fuji at [Chainlink Faucets](https://faucets.chain.link/)
- Additional LINK can be acquired from [AllThatNode Faucet](https://www.allthatnode.com/faucet/avalanche.dsrv)

## Step 2: Smart Contract Deployment

### TransferUSDCBasic.sol
- **Contract Creation**:
  - In Remix, use the "FILE EXPLORER" to create a new file named `TransferUSDCBasic.sol`.
  - Copy the contract code from the provided snippet into this file.

### Deployment
- Compile and deploy the contract on the Avalanche Fuji network using MetaMask.

## Step 3: Interacting with the Contract

### Approving USDC
To allow the `TransferUSDCBasic` contract to manage your USDC, you have two options for approval:

#### Option 1: Using the Snowtrace Write Contract Interface
- Navigate to the [Snowtrace Write Contract page](https://testnet.snowtrace.io/token/0x5425890298aed601595a70ab815c96711a31bc65/contract/writeProxyContract).
- Connect your wallet.
- Under the `approve` function, enter:
  - **spender**: Your `TransferUSDCBasic.sol` contract address.
  - **value**: 100000 (equivalent to 0.1 USDC).
- Click "Write" to submit the transaction.

#### Option 2: Using Remix with the IERC20 Interface
- In Remix, ensure your `TransferUSDCBasic.sol` contract is deployed.
- From the "Deploy & Run Transactions" panel:
  - Select "IERC20" from the dropdown under "Contracts".
  - Paste the USDC contract address (0x5425890298aed601595a70ab815c96711a31bc65) into the "At Address" field and click "At Address". **Note: Do not deploy**.
- Expand the contract methods and find the `approve` function:
  - **spender**: Address of your `TransferUSDCBasic.sol` contract.
  - **value**: 100000 (0.1 USDC).
- Execute the transaction by clicking "Transact".

After approval, proceed with the USDC transfer:

### Transfer USDC
- Navigate back to your deployed `TransferUSDCBasic.sol` contract in Remix.
- Call the `transferUsdcToSepolia` function with the parameters:
  - **_receiver**: Your wallet address on the Ethereum Sepolia network.
  - **_amount**: 100000 (0.1 USDC).
- Monitor the transaction in Remix and on the CCIP Explorer to ensure successful execution.

## Step 4: Monitoring Transactions

### CCIP Explorer
- Track the transaction ID and status using the [CCIP Explorer](https://ccip.chain.link/).

### Check Balances
- Verify USDC balances on both networks to confirm the transfer was successful.

## Common Issues and Solutions

While interacting with the `TransferUSDCBasic` contract and executing transactions, you might encounter several issues. Below are some common problems along with troubleshooting tips:

### Issue: Transaction Fails on Approval or Transfer
- **Symptoms**: Transactions for approving or transferring USDC fail without executing.
- **Potential Causes and Solutions**:
  - **Insufficient Gas Fees**: Ensure that your wallet has enough AVAX to cover the gas fees on the Avalanche Fuji testnet. You can obtain AVAX from [Fuji faucets](https://faucets.chain.link/fuji).
  - **Incorrect Contract Permissions**: Double-check that the contract address used in the `approve` function is correct. Ensure that the `TransferUSDCBasic` contract address is entered correctly.

### Issue: USDC Not Showing Up After Transfer
- **Symptoms**: After executing the `transferUsdcToSepolia` function, the USDC does not appear in the destination wallet.
- **Potential Causes and Solutions**:
  - **Network Delays**: Transactions across networks may experience delays. Wait a few minutes and check again.
  - **Block Explorer Issues**: Use a reliable block explorer like [Snowtrace for Fuji](https://testnet.snowtrace.io/) and [Sepolia Etherscan](https://sepolia.etherscan.io/) to verify the transactions and balances.

### Issue: CCIP Explorer Does Not Show Transaction
- **Symptoms**: After initiating a cross-chain transaction, the CCIP Explorer does not display any details about the transaction.
- **Potential Causes and Solutions**:
  - **Transaction Not Yet Indexed**: Sometimes, transactions take a while to be indexed by explorers. Refresh the page or check back later to see if the transaction appears.
  - **Incorrect Transaction ID**: Ensure you copied the correct transaction ID from Remix after executing the function.

### Issue: Incorrect LINK or USDC Balances
- **Symptoms**: The balances displayed in Remix or on blockchain explorers do not reflect recent transactions or expected values.
- **Potential Causes and Solutions**:
  - **Failed Transactions**: Check your wallet and block explorer histories to confirm that previous transactions (fund transfers, approvals) were successful.
  - **Refresh Data**: Sometimes, interfaces do not update promptly. Refresh your wallet or the page of the blockchain explorer you are using.

### Issue: Errors in Contract Execution
- **Symptoms**: Errors pop up when trying to execute functions in the Remix IDE.
- **Potential Causes and Solutions**:
  - **Smart Contract Bugs**: Review the contract code for any potential errors that could affect execution.
  - **Remix IDE Errors**: Ensure that Remix is connected to the correct network and that the contract is properly deployed and verified on the network.

## Additional Resources

- [Chainlink Documentation](https://docs.chain.link/)
- [Avalanche Fuji Block Explorer](https://testnet.snowtrace.io/)
- [Ethereum Sepolia Block Explorer](https://sepolia.etherscan.io/)

## Watch the Tutorial

Watch our [tutorial on YouTube](https://www.youtube.com/watch?v=Of5pf2qYUtE) for a step-by-step project walkthrough.