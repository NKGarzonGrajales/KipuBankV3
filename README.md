<h1 align="center">💰 KipuBankV3</h1>

<p align="center" style="font-size:14px">
Smart Contract DeFi que simula una banca descentralizada con manejo de depósitos, retiros, oráculo y roles administrativos.  
Desarrollado en <strong>Solidity 0.8.24</strong> y verificado en la red de pruebas <strong>Ethereum Sepolia</strong>.
</p>

---

<h2 align="center">⚙️ Descripción General</h2>

**KipuBankV3** es un contrato inteligente que representa una versión avanzada de un sistema bancario descentralizado (DeFi).  
Permite depósitos y retiros en ETH y tokens ERC20 simulados, aplicando control de acceso por roles y verificación pública en Etherscan.

El proyecto fue implementado en **Remix IDE**, conectado a **MetaMask (Sepolia)**, y probado con múltiples cuentas para validar roles, límites y seguridad.

---

<h2 align="center">🧠 Objetivos del Proyecto</h2>

- Implementar un contrato DeFi con manejo de **roles jerárquicos**.  
- Simular **depósitos y retiros** de ETH y tokens ERC20.  
- Aplicar medidas de seguridad: **ReentrancyGuard** y **AccessControl**.  
- Probar interacción entre múltiples cuentas (admin y usuario).  
- Verificar el contrato completo mediante **JSON Standard Input** en Etherscan.  

---

<h2 align="center">🧩 Parámetros de Despliegue</h2>

| Parámetro | Descripción | Valor |
|------------|-------------|--------|
| `_oracle` | Dirección del oráculo Chainlink ETH/USD (Sepolia) | `0x694AA1769357215DE4FAC081bf1f309aDC325306` |
| `_bankCapUsedETH` | Cap de uso inicial (en 8 decimales) | `0` |
| `_initialEthBankCap` | Cap global del banco (1.55 ETH) | `1550000000000000000` |
| `_initialEthWithdrawCap` | Límite de retiro por transacción (0.02 ETH) | `20000000000000000` |

---

### ⚙️ **Funciones Principales**

```solidity
depositETH()                          // Depósito en ETH
depositToken(address,uint256)         // Depósito de tokens ERC20
withdrawETH(uint256)                  // Retiro en ETH
withdrawToken(address,uint256)        // Retiro de tokens ERC20
grantRole(bytes32,address)            // Asignar rol
hasRole(bytes32,address)              // Verificar rol
rescueETH(uint256,address)            // Rescate de fondos ETH
rescueERC20(address,uint256,address)  // Rescate de tokens ERC20

---

🧠 Roles Implementados

- DEFAULT_ADMIN_ROLE → Control total del contrato.

- BANK_ADMIN_ROLE → Permite depósitos y rescates.

- ORACLE_DECIMALS → Parámetro de precisión (8).

---

<h2 align="center">👥 Roles y Cuentas Utilizadas</h2>

| Tipo | Dirección | Descripción |
|------|------------|-------------|
| **Cuenta A (Admin / Deployer)** | `0xEFCD678F3E8Ba831787b6eb41ea8A618674B1dd8` | Desplegó el contrato y tiene el rol `DEFAULT_ADMIN_ROLE`. |
| **Cuenta B (Usuario autorizado)** | `0xc89edce46B30416268E33fb181616f3f90580d71` | Recibió `BANK_ADMIN_ROLE` para pruebas de depósitos, retiros y rescates. |

Roles principales:
- `DEFAULT_ADMIN_ROLE` → Acceso total.  
- `BANK_ADMIN_ROLE` → Gestión de operaciones del banco.

---

<h2 align="center">💵 Tokens Mock Vinculados</h2>

| Token | Dirección | Descripción |
|--------|------------|-------------|
| **MockUSDC** | `0xCF27A9f700835895648EA5EfA6914074557c7b80` | Token ERC20 simulado para pruebas de depósito y retiro. |
| **MockDAI** | `0xbBf03149d20B205000c048308CF2d17c2341BfF7` | Token ERC20 simulado compatible con las funciones del contrato. |

---

<h2 align="center">🧪 Pruebas Realizadas</h2>

#### 🔹 Asignación de Roles
- Desde la **cuenta A**, se ejecutó `grantRole()` para otorgar `BANK_ADMIN_ROLE` a la **cuenta B**.  
- Confirmado con `hasRole()` → Resultado: `true`.

#### 🔹 Depósitos
- Se ejecutó `depositETH()` desde la **cuenta B**.  
  - Resultado visible en Etherscan: transacción confirmada.  
  - Valor validado con `totalDepositedPerToken(address)` = `1000000000000000000`.
- Se realizaron depósitos con `MockDAI` y `MockUSDC`, con `allowance` previa aprobada.

#### 🔹 Retiros
- La **cuenta B** realizó `withdrawETH()` y `withdrawToken()` sin errores.  
- Los valores se actualizaron correctamente en el balance del contrato.

#### 🔹 Funciones de rescate (Admin)
- Desde la **cuenta A**, se probó `rescueETH()` con éxito.  
- Transacción confirmada sin pérdida de fondos de usuario.

---

<h2 align="center">📊 Resultados en Etherscan</h2>

- `totalDepositedPerToken(MockUSDC)` → `1000000000000000000`  
- `totalDepositedPerToken(MockDAI)` → `1000000000000000000`  
- `hasRole(BANK_ADMIN_ROLE, cuenta B)` → `true`  
- `rescueETH()` → Ejecución confirmada (block 9615136)

---

<h2 align="center">🔗 Contratos Verificados</h2>

| Contrato | Red | Dirección |
|-----------|-----|-----------|
| **KipuBankV3 (Principal)** | Sepolia | [0xd8d9e6a133981b9789849075c89dbe30a0bf05f1](https://sepolia.etherscan.io/address/0xd8d9e6a133981b9789849075c89dbe30a0bf05f1) |
| **MockUSDC** | Sepolia | [0xCF27A9f700835895648EA5EfA6914074557c7b80](https://sepolia.etherscan.io/address/0xCF27A9f700835895648EA5EfA6914074557c7b80) |
| **MockDAI** | Sepolia | [0xbBf03149d20B205000c048308CF2d17c2341BfF7](https://sepolia.etherscan.io/address/0xbBf03149d20B205000c048308CF2d17c2341BfF7) |

---

<h2 align="center">🧱 Decisiones Técnicas</h2>

- Uso de `AccessControl` (OpenZeppelin) para gestionar roles.  
- Seguridad reforzada con `ReentrancyGuard`.  
- Interacción con oráculo Chainlink ETH/USD.  
- Modularidad en las funciones de depósito, retiro y rescate.  
- Gas optimizado y versión EVM `Shanghai`.  

---

<h2 align="center">🛠️ Herramientas Utilizadas</h2>

- **Remix IDE (Web3)**  
- **MetaMask** – Red de prueba Sepolia  
- **Etherscan Verification (JSON Input)**  
- **OpenZeppelin Contracts 5.x**  
- **Chainlink Price Feeds**  

---

<h2 align="center">👩‍💻 Autora</h2>

**N.K.G.G.**  
Full Stack & Blockchain Developer  
Proyecto Módulo 4 - Solidity y DeFi  
> Verificado en Etherscan, probado con dos cuentas, tokens ERC20 y oráculo Chainlink.

---

<p align="center" style="font-size:12px; color:gray">
© 2025 N.K.G.G. - Proyecto KipuBankV3  
Desarrollado en Solidity con Remix IDE y verificación pública en Etherscan.
</p>

