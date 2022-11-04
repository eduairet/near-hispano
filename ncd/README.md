# NEAR Certified Developer

## Requirements

-   Instalar `node.js` localmente
-   Instalar NEAR CLI `npm -g install near` localmente
-   Crear una cuenta en la testnet de NEAR

## Web2 -> Web3

|                      | web2                                             | web3                                                          |
| -------------------- | ------------------------------------------------ | ------------------------------------------------------------- |
| Topología            | cliente-servidor                                 | ciente-(servidor+blockchain)                                  |
| _Tech stack_         | JS frontend, diferentes tecnologías en _backend_ | JS frontend, Rust y Assembly Script en NEAR                   |
| Seguridad            | Cuentas: usuario/contraseña, oAuth               | Cuentas: Par de llaves con encriptación asimétrica            |
|                      | Servidores: AWS / GCP / Azure                    | Servidores: AWS / GCP / Azure + Consenso (PoW, PoS, etcétera) |
| Comportamiento clave | rápido, barato, los datos son nativos            | no repudiable, permanente, el dinero es «nativo»              |

## _Fullstack_ NEAR DApp

-   Una aplicación _fullstack_ de NEAR permite interactuar con la _blockchain_ utilizando un _frontend_ desarrollado con JavaScript que interactua con el _backend_ que son contratos que modifican el estado de la red o permiten consultas de los datos almacenados en la misma

    -   Comúnmente el _tree_ de una DApp se vería de la siguente manera
        ```Bash
        .
        ├── contract # Directorio con contratos
        ├── frontend # Frontend de la DApp
        ├── integration-tests # Tests
        └── package.json # Instrucciones y paquetes
        ```

## _Frontend_

-   El frontend necesita comunicarse con la API de NEAR importando elementos de diversas librerías de NEAR

    ```JSX
    // React
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './App';

    // NEAR
    import { HelloNEAR } from './near-interface';
    import { Wallet } from './near-wallet';

    // When creating the wallet you can optionally ask to create an access key
    // Having the key enables to call non-payable methods without interrupting the user to sign
    const wallet = new Wallet({ createAccessKeyFor: process.env.CONTRACT_NAME })

    // Abstract the logic of interacting with the contract to simplify your flow
    const helloNEAR = new HelloNEAR({ contractId: process.env.CONTRACT_NAME, walletToUse: wallet });

    // Setup on page load
    window.onload = async () => {
        const isSignedIn = await wallet.startUp()

        ReactDOM.render(
            <App isSignedIn={isSignedIn} helloNEAR={helloNEAR} wallet={wallet} />,
            document.getElementById('root')
        );
    }
    ```

-   [Crear una subcuenta](https://docs.near.org/tools/near-cli#near-send) para el contrato
    - Es buena prác

- El archivo `.wasm` es el archivo que contiente el contrato compilado
