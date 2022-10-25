# NEAR NCA

## Certificación de analista NEAR

-   Ethereum es el ecosistema más grande para desarrollo de aplicaciones de Web3
-   NEAR ayuda a escalar el desarrollo de aplicaciones Web3

## Conceptos básicos:

-   **Blockchain:** Es un grupo de bloques enlazados, inmutable y asegurados con criptografía
-   **Contrato inteligente:** Protocolo de transacción computarizado, barato y autoejecutable, que se encarga de que se cumplan las condiciones del mismo.
    -   No se presta a interpretaciones, solo se ejecuta
    -   Puede traer información del mundo real por medio de oráculos aunque mientras más subjetiva sea esta más compleja será la implementación

## Intro:

-   Es una Layer1, _Proof of Stake_[^2] (prueba de participación), construida para ser simple y escalable para todos por medio de _sharding_[^1]
-   El PoS puede ser corrompido si alguien tiene la mayoría de los datos de la red
-   El protocolo de NEAR es un protocolo para la web abierta, PoS, con escalamiento basado en _sharding_ y con una visión a ser **developer friendly.**
-   Con el sharding se pueden multiplicar las transacciones de la _blockchain_(aproximadamente 100,000 por segundo)
-   Near permite manejar nuestra identidad mediante dapps, tokens, y alojar o ejecutar contratos inteligentes
-   Tipos de cuentas:
    -   **Top Level Accounts:** Cuentas principales o raíz en NEAR `minombre.near` para asignarlos a tu cuenta `0x13a...`
    -   **Sub Accounts:** Similar a los subdominios de sitios web. Permite desplegar contratos y manejar assets `contrato.minombre.near`
    -   **Testnet Accounts:** Cuentas que corren en la red testnet de NEAR
-   Wallets:

    -   [Mainnet](https://wallet.near.org)
    -   [Testnet](https://wallet.testnet.near.org)
    -   Diferencias con Ethereum

        |                       | Ethereum                                 | NEAR                                        |
        | --------------------- | ---------------------------------------- | ------------------------------------------- |
        | Identificador Público | _Public Key_ (0xa...)                    | Account ID (xxxx.near o 0xa...)             |
        | Identificador Privado | _Private Key_ (0xa...)                   | Multiples _Kevpairs_ con permisos           |
        |                       |                                          | {Pub, Priv} -> Full Access Key              |
        |                       |                                          | {Pub, Priv} -> Contract Access Key          |
        | Características       | Con la _Private Key_ tienes acceso total | Accesos basados en los _keypairs_           |
        |                       | La cuenta no se crea con una transacción | El _Account ID_ se crea con una transacción |

-   En NEAR tú controlas la identidad de tu cuenta y puedes dar distintos tipos de acceso a tu cuenta:
    -   Full Access: control completo de la cuenta (administrador)
    -   Function Call Keys: accesos limitados a métodos `non-payable`
-   NEAR construye contratos en RUST y JavaScript
-   Aurora: Es la EVM de NEAR y permite conectarse con Ethereum
-   Ambiente de desarrollo:
    -   Herramientas: `NEAR CLI` `NEAR Explorer` `NEAR RPC` `NEAR API JS`
    -   Indexers y oraculos: `NEAR Indexer Framework` `NEAR Lake Framework` `The Graph` `Chainlink` `Flux Protocol`

### Proyecto Final: ¿Cómo implementarían la tecnología de NEAR en un proyecto?

-   Ideas:
    -   Plataforma que mintea un NFT de cierto color de acuerdo al monto (oráculo)
-   Hacer una presentación

## Documentación

-   [NEAR Docs](https://docs.near.org/)
-   [Aurora](https://doc.aurora.dev)

[^1]: Se abrevia PoS
[^2]: Los nodos se dividen en piezas más pequeñas llamadas _chunks (Nightshade)_
