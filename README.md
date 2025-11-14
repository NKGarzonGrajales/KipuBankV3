                                            💰 KipuBankV3

<p align="center"> Smart Contract DeFi que simula una banca descentralizada con depósitos, retiros, oráculo y roles avanzados. Desarrollado en <strong>Solidity 0.8.24</strong> y desplegado en <strong>Ethereum Sepolia</strong>. </p>

---

⚙️ Descripción General

KipuBankV3 es una versión avanzada de un sistema bancario DeFi que permite manejar ETH y tokens ERC20 dentro de un esquema seguro, con:

Roles jerárquicos (AccessControl)

Depósitos y retiros multiactivo

Integración con oráculo Chainlink

Swap interno estilo AMM

Seguridad con ReentrancyGuard

Verificación pública en Etherscan (JSON Input)

---

🧠 Objetivos del Proyecto

Implementar jerarquía de roles administrativos.

Manejar depósitos/retiros en ETH y tokens ERC20.

Añadir módulo de swap interno AMM.

Aplicar seguridad: ReentrancyGuard + SafeERC20.

Verificar el contrato completo en Etherscan.

---

🧩 Parámetros de Despliegue

Parámetro	Descripción	Valor
_oracle	Chainlink ETH/USD	0x694AA1769357215DE4FAC081bf1f309aDC325306
_bankCapUsedETH	Cap inicial	0
_initialEthBankCap	Cap global ETH	1550000000000000000
_initialEthWithdrawCap	Máx retiro/tx	20000000000000000

---

⚙️ Funciones Principales
-depositETH()
-depositToken(address,uint256)
-withdrawETH(uint256)
-withdrawToken(address,uint256)
-grantRole(bytes32,address)
-hasRole(bytes32,address)
-rescueETH(uint256,address)
-rescueERC20(address,uint256,address)
-swapVaultTokens(...)

---

👥 Roles y Cuentas Utilizadas

Tipo	Dirección	Descripción
Cuenta A (Admin / Deployer)	0xEFCD678F3E8Ba831787b6eb41ea8A618674B1dd8	DEFAULT_ADMIN_ROLE
Cuenta B (Usuario)	0xc89edce46B30416268E33fb181616f3f90580d71	BANK_ADMIN_ROLE

---
💵 Tokens Mock Vinculados

Token	Dirección	Descripción
MockUSDC	0xCF27A9f700835895648EA5EfA6914074557c7b80	ERC20 (6 decimales)
MockDAI	0xbBf03149d20B205000c048308CF2d17c2341BfF7	ERC20 (18 decimales)

---

🧪 Pruebas Realizadas


🔹 Asignación de Roles

-grantRole() ejecutado desde Cuenta A hacia Cuenta B.

-hasRole() verificó resultado true.

🔹 Depósitos

-ETH depositado vía depositETH() desde B.

-Depósitos de MockDAI y MockUSDC realizados con approve() previo.

🔹 Retiros

-withdrawETH() y withdrawToken() desde B → éxito.

🔹 Rescates (Admin)

-rescueETH() ejecutado desde A → confirmado en Etherscan.

---

📊 Resultados en Etherscan (On-chain Results)


totalDepositedPerToken(MockUSDC) → 1000000000000000000

totalDepositedPerToken(MockDAI) → 1000000000000000000

hasRole(BANK_ADMIN_ROLE, cuenta B) → true

rescueETH() → Confirmado en bloque 9615136

---

🔄 Swap Interno Estilo AMM

Se añadió:

swapVaultTokens(tokenIn, tokenOut, amountIn, minAmountOut)

**

Resultados verificados:

Antes:

1 DAI (18 decimales)

4 USDC (6 decimales)

Swap:

swapVaultTokens(MockDAI, MockUSDC, 1e18, 0)


Después:

DAI → 0

USDC → 5

✔ Manejo correcto de decimales
✔ Liquidez comprobada
✔ Sin reentrancia
✔ Funcionalidad completa

---

🔗 Contratos Verificados

Contrato	Red	Dirección
KipuBankV3	Sepolia	https://sepolia.etherscan.io/address/0x9db4f934df129e959f9f205f3dd5cd8dcbe86a05#code

MockUSDC	Sepolia	https://sepolia.etherscan.io/address/0xCF27A9f700835895648EA5EfA6914074557c7b80

MockDAI	Sepolia	https://sepolia.etherscan.io/address/0xbBf03149d20B205000c048308CF2d17c2341BfF7

---

🧱 Decisiones Técnicas

AccessControl (OpenZeppelin)

ReentrancyGuard

Chainlink Price Feed

AMM interno sin DEX externa

Compatibilidad EVM Shanghai

---

🛠️ Herramientas Utilizadas

Remix IDE

MetaMask

Etherscan (Standard JSON Input)

OpenZeppelin 5.x

Chainlink Feeds

---

👩‍💻 Autora

N.K.G.G.
Full Stack & Blockchain Developer

<p align="center"> <sub>© 2025 N.K.G.G. – Proyecto KipuBankV3. Desarrollado con Solidity y verificado públicamente en Etherscan.</sub> </p>


