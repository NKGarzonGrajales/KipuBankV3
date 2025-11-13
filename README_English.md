💰 KipuBankV3
<p align="center"> DeFi smart contract simulating a decentralized banking system with deposits, withdrawals, oracle integration, and hierarchical roles.<br> Built in <strong>Solidity 0.8.24</strong> and deployed on <strong>Ethereum Sepolia Testnet</strong>. </p>
⚙️ General Description

KipuBankV3 is an upgraded decentralized banking smart contract (DeFi) supporting ETH and ERC20 token deposits/withdrawals, role-based permissions, and secure public verification on Etherscan.

The project was developed using Remix IDE, connected to MetaMask (Sepolia), and tested with multiple accounts to validate roles, limits, balances, price feed behavior, and access-control restrictions.

🧠 Project Objectives

Implement a DeFi contract with hierarchical roles.

Simulate deposits and withdrawals in ETH and ERC20 tokens.

Apply security mechanisms such as ReentrancyGuard and AccessControl.

Test interactions between two accounts (admin & user).

Verify the complete contract using Standard JSON Input.

🧩 Deployment Parameters
| Parameter                | Description                            | Value                                        |
| ------------------------ | -------------------------------------- | -------------------------------------------- |
| `_oracle`                | Chainlink ETH/USD price feed (Sepolia) | `0x694AA1769357215DE4FAC081bf1f309aDC325306` |
| `_bankCapUsedETH`        | Initial bank usage cap (8 decimals)    | `0`                                          |
| `_initialEthBankCap`     | Global ETH cap (1.55 ETH)              | `1550000000000000000`                        |
| `_initialEthWithdrawCap` | Max withdrawal per tx (0.02 ETH)       | `20000000000000000`                          |

⚙️ Main Functions

depositETH()                          // ETH deposit
depositToken(address,uint256)         // ERC20 deposit
withdrawETH(uint256)                  // Withdraw ETH
withdrawToken(address,uint256)        // Withdraw ERC20
grantRole(bytes32,address)            // Assign role
hasRole(bytes32,address)              // Check role
rescueETH(uint256,address)            // Admin ETH rescue
rescueERC20(address,uint256,address)  // Admin ERC20 rescue

🧠 Implemented Roles

DEFAULT_ADMIN_ROLE → Full control of the contract

BANK_ADMIN_ROLE → Deposit & rescue permissions

ORACLE_DECIMALS → Precision parameter (8)

👥 Accounts and Roles Used

| Type                             | Address                                      | Description                 |
| -------------------------------- | -------------------------------------------- | --------------------------- |
| **Account A (Admin / Deployer)** | `0xEFCD678F3E8Ba831787b6eb41ea8A618674B1dd8` | Holds `DEFAULT_ADMIN_ROLE`. |
| **Account B (Tester)**           | `0xc89edce46B30416268E33fb181616f3f90580d71` | Assigned `BANK_ADMIN_ROLE`. |


Roles summary:

-DEFAULT_ADMIN_ROLE → total access

-BANK_ADMIN_ROLE → banking operations manager

| Token        | Address                                      | Purpose                                 |
| ------------ | -------------------------------------------- | --------------------------------------- |
| **MockUSDC** | `0xCF27A9f700835895648EA5EfA6914074557c7b80` | ERC20 used for deposit/withdraw tests   |
| **MockDAI**  | `0xbBf03149d20B205000c048308CF2d17c2341BfF7` | ERC20 compatible with banking functions |

🧪 Tests Performed
🔹 Role Assignment

From Account A, grantRole() assigned BANK_ADMIN_ROLE to Account B.

Confirmed with hasRole() → result: true.

🔹 Deposits

ETH deposit:

depositETH() executed from Account B

Confirmed on Etherscan

totalDepositedPerToken(token) = 1000000000000000000

ERC20 deposits executed after approve() allowance.

🔹 Withdrawals

Account B successfully executed:

withdrawETH()

withdrawToken()

Balances updated correctly.

🔹 Admin Rescue Tests

Admin executed rescueETH() successfully:

No user funds lost

Etherscan transaction confirmed

📊 Etherscan Results

-totalDepositedPerToken(MockUSDC) → 1000000000000000000

-totalDepositedPerToken(MockDAI) → 1000000000000000000

-hasRole(BANK_ADMIN_ROLE, Account B) → true

-rescueETH() → Successful execution (block 9615136)

🔗 Verified Contracts

| Contract       | Network | Address                                                                                                                                                            |
| -------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **KipuBankV3** | Sepolia | [https://sepolia.etherscan.io/address/0xd8d9e6a133981b9789849075c89dbe30a0bf05f1](https://sepolia.etherscan.io/address/0xd8d9e6a133981b9789849075c89dbe30a0bf05f1) |
| **MockUSDC**   | Sepolia | [https://sepolia.etherscan.io/address/0xCF27A9f700835895648EA5EfA6914074557c7b80](https://sepolia.etherscan.io/address/0xCF27A9f700835895648EA5EfA6914074557c7b80) |
| **MockDAI**    | Sepolia | [https://sepolia.etherscan.io/address/0xbBf03149d20B205000c048308CF2d17c2341BfF7](https://sepolia.etherscan.io/address/0xbBf03149d20B205000c048308CF2d17c2341BfF7) |


🧱 Technical Decisions

Access control using OpenZeppelin AccessControl

Protection against reentrancy using ReentrancyGuard

Integration with Chainlink price feed

Modular banking logic

Gas-optimized with Shanghai EVM

🛠️ Tools Used

Remix IDE

MetaMask (Sepolia)

Etherscan Contract Verification

OpenZeppelin Contracts 5.x

Chainlink Price Feeds

👩‍💻 Author

N.K.G.G.
Full Stack & Blockchain Developer
Module 4 – Solidity & DeFi Project

Verified on Etherscan, tested with two accounts, ERC20 tokens and Chainlink price feed.

<p align="center">
  <sub>© 2025 N.K.G.G. – KipuBankV3 Project  
  Developed in Solidity using Remix IDE with public verification on Etherscan.</sub>
</p>


