💰 KipuBankV3
<p align="center"> Smart Contract DeFi que simula una banca descentralizada con depósitos, retiros, oráculo y roles avanzados. Desarrollado en **Solidity 0.8.24** y desplegado en **Ethereum Sepolia**. </p>



⚙️ Descripción General

KipuBankV3 es una versión avanzada de un sistema bancario DeFi que permite manejar ETH y tokens ERC20 dentro de un esquema seguro con:

Control de acceso basado en Roles (AccessControl).

Límites globales y por transacción.

Integración con oráculo Chainlink ETH/USD.

Soporte multi-token y swap interno estilo AMM.

Verificación pública en Etherscan usando JSON Standard Input.

El proyecto fue desarrollado en Remix IDE, conectado a MetaMask en la red Sepolia, y probado con múltiples cuentas.

---

🧠 Objetivos del Proyecto

Implementar jerarquía de roles administrativos.

Manejar depósitos/retiros en ETH y tokens ERC20.

Añadir módulo de swap interno (estilo Uniswap).

Aplicar seguridad: ReentrancyGuard + SafeERC20.

Verificar el contrato completo en Etherscan.

---

🧩 Parámetros de Despliegue

| Parámetro                | Descripción                 | Valor                                        |
| ------------------------ | --------------------------- | -------------------------------------------- |
| `_oracle`                | Chainlink ETH/USD (Sepolia) | `0x694AA1769357215DE4FAC081bf1f309aDC325306` |
| `_bankCapUsedETH`        | Cap en USD (8 decimales)    | `0`                                          |
| `_initialEthBankCap`     | Cap global ETH              | `1550000000000000000`                        |
| `_initialEthWithdrawCap` | Límite retiro/tx            | `20000000000000000`                          |

---

⚙️ Funciones Principales

depositETH()                          // Depósito en ETH
depositToken(address,uint256)         // Depósito ERC20
withdrawETH(uint256)                  // Retiro en ETH
withdrawToken(address,uint256)        // Retiro ERC20
grantRole(bytes32,address)            // Asignar rol
hasRole(bytes32,address)              // Verificar rol
rescueETH(uint256,address)            // Rescate ETH (admin)
rescueERC20(address,uint256,address)  // Rescate ERC20 (admin)
swapVaultTokens(...)                  // Swap interno estilo AMM

---


👥 Roles y Cuentas Utilizadas

| Tipo                              | Dirección                                    | Descripción                |
| --------------------------------- | -------------------------------------------- | -------------------------- |
| **Cuenta A (Admin / Deployer)**   | `0xEFCD678F3E8Ba831787b6eb41ea8A618674B1dd8` | Tiene `DEFAULT_ADMIN_ROLE` |
| **Cuenta B (Usuario autorizado)** | `0xc89edce46B30416268E33fb181616f3f90580d71` | Recibió `BANK_ADMIN_ROLE`  |


Roles principales:

-DEFAULT_ADMIN_ROLE → Acceso total

-BANK_ADMIN_ROLE → Gestión bancaria

---

💵 Tokens Mock Vinculados

| Token        | Dirección                                    | Descripción           |
| ------------ | -------------------------------------------- | --------------------- |
| **MockUSDC** | `0xCF27A9f700835895648EA5EfA6914074557c7b80` | ERC20 de 6 decimales  |
| **MockDAI**  | `0xbBf03149d20B205000c048308CF2d17c2341BfF7` | ERC20 de 18 decimales |

---

🧪 Pruebas Realizadas

🔹 Asignación de Roles

grantRole() desde Cuenta A hacia Cuenta B.

Verificado con hasRole() → true.

🔹 Depósitos

depositETH() desde Cuenta B.

Depósitos MockDAI y MockUSDC con approve() previo.

🔹 Retiros

withdrawETH() y withdrawToken() ejecutados sin errores.

🔹 Funciones de Rescate

rescueETH() ejecutado desde Cuenta A → éxito.

---

📊 Resultados en Etherscan (On-chain Results)

totalDepositedPerToken(MockUSDC) → 1000000000000000000

totalDepositedPerToken(MockDAI) → 1000000000000000000

hasRole(BANK_ADMIN_ROLE, cuenta B) → true

rescueETH() → Confirmado en bloque 9615136

---

🔄 Swap Interno Estilo AMM

Se añadió la función: 

swapVaultTokens(tokenIn, tokenOut, amountIn, minAmountOut)

Prueba realizada:

Saldo previo:

Cuenta B: 1 DAI (18d) y 4 USDC (6d)

Ejecución:

swapVaultTokens(
  MockDAI,
  MockUSDC,
  1e18,
  0
)


Resultado:

MockDAI → 0

MockUSDC → 5

✔ Manejo correcto de decimales
✔ Liquidez suficiente
✔ Protección anti-reentrancia
✔ Swap AMM funcional

---

🔗 Contratos Verificados

| Contrato       | Red     | Dirección                                                                                                                                                          |
| -------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **KipuBankV3** | Sepolia | [https://sepolia.etherscan.io/address/0x9db4f934df129e959f9f205f3dd5cd8dcbe86a05] |
| **MockUSDC**   | Sepolia | [https://sepolia.etherscan.io/address/0xCF27A9f700835895648EA5EfA6914074557c7b80] |
| **MockDAI**    | Sepolia | [https://sepolia.etherscan.io/address/0xbBf03149d20B205000c048308CF2d17c2341BfF7] |

---

🧱 Technical Decisions

OpenZeppelin AccessControl

SafeERC20 managed transfers

ReentrancyGuard protection

Chainlink oracle integration

AMM-style swap logic

Shanghai EVM

---

🛠️ Tools Used

Remix IDE

MetaMask (Sepolia)

Etherscan Verification

OpenZeppelin Contracts 5.x

Chainlink Feeds

----

👩‍💻 Author

N.K.G.G.
Full Stack & Blockchain Developer

<p align="center"> <sub>© 2025 N.K.G.G. – KipuBankV3 Project. Developed in Solidity with public Etherscan verification.</sub> </p>


