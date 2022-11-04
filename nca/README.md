# NEAR NCA

## Certificación de analista NEAR

> -   Ethereum es el ecosistema más grande para desarrollo de aplicaciones de Web3
> -   NEAR ayuda a escalar el desarrollo de aplicaciones Web3

## Conceptos básicos:

-   **Blockchain:** Es un grupo de bloques enlazados, inmutable y asegurados con criptografía
-   **Contrato inteligente:** Protocolo de transacción computarizado, barato y autoejecutable, que se encarga de que se cumplan las condiciones del mismo.
    -   No se presta a interpretaciones, solo se ejecuta
    -   Puede traer información del mundo real por medio de oráculos aunque mientras más subjetiva sea esta más compleja será la implementación
-   **Transacción:**

    -   Una transacción es la unidad mínima de trabajo (cómputo)
    -   Es una colección de acciones que describe lo que tiene que hacerse en el receptor
    -   Información contenida en una transacción:
        -   Origen
        -   Receptor
        -   Timestamp
        -   Hash único
    -   Las acciones de una transacción son unidades componibles y son las siguientes:
        -   `CreateAccount` hacer una nueva cuenta
        -   `DeleteAccount` borrar una cuenta (transferir balance a una cuenta beneficiaria)
        -   `AddKey` añadir una llave a una cuenta _(FullAccess / FunctionCall)_
        -   `DeleteKey` borrar una llave existente de una cuenta
        -   `Transfer` enviar _tokens_ de una cuenta a otra
        -   `Stake` hacerse un validador (en la próxima oportunidad disponible)
        -   `DeployContract` despliegue de contrato
        -   `FunctionCall` llamado a un método en un contrato (incluye un presupuesto para cómputo y almacenamiento)
    -   Recibos:
        -   Mensaje pagado que se ejecuta en cierto destino
        -   Es una solicitud externa para crear un recibo
        -   Hay varias maneras de generarlos:
            -   Emitir una transacción
            -   Regresar una promesa (llamadas cruzadas entre contratos)
            -   Emitir un reembolso
    -   Atomicidad:
        -   La ejecución de recibos es atómica -> Todo o nada se ejecuta
        -   Una transacción de `functionCall` puede generar un número indefinido de recibos atómicos donde el éxito o fracaso de un recibo no afecta necesariamente el estado de otros recibos generados por la misma transacción
    -   **Ciclo de vida de la transación:**

        -   **RPC** es la puerta de entrada a la _blockchain,_ para que se procesen las transacciones
        -   La transacción entra y se corre en la máquina virtual esperando a ser validada
        -   **Gas:** Este es un monto que se añade a la transacción y sirve para pagar al validador por aprobar transaciones
            -   El gas se cobra en la moneda nativa de la red, que es el NEAR
            -   **Gas Units:** Unidad que determina el costo del gas y encapsula el cómputo, banda, tiempo y almacenamiento usado por el contrato
            -   **Gas Price:** Las _gas units_ se multiplican por el precio para determinal el costo final
                -   El precio se recalcula de acuerdo al tráfico de la red

    -   **Estado**
        -   Muestra el estado, los resultados y los recibos generados por la transacción
        -   El campo de estado es un objeto con una llave simple y hay cuatro tipos de llave:
            -   `SucceessValue`
                -   El recibo ha sido ejecutado exitosamente
                -   El valor de la llave es el valor del `return` (solo puede ser `nonempty` cuando es resultado de un recibo `functionCall`)
            -   `SuccessReceiptld`
                -   La transacción puede o ser exitosamente convertida a un recibo o un recibo es exitosamente procesado y ha generado otro recibo
                -   El valor de esta llave es el id del nuevo recibo generado
            -   `Failure`
                -   La transacción o recibo ha fallado durante la ejecución
            -   `Unknown`
                -   La transacción o recibo ha no ha sido procesada aún.
    -   **Finalidad:**
        -   Consulta simple a la transacción que revisa que todos los hashes de las transacciones y recibos generados son finales

## NEAR:

-   Es una Layer1, _Proof of Stake_[^2] (prueba de participación), construida para ser simple y escalable para todos por medio de _sharding_[^1]
-   El PoS puede ser corrompido si alguien tiene la mayoría de los datos de la red
-   El protocolo de NEAR es un protocolo para la web abierta, PoS, con escalamiento basado en _sharding_ y con una visión a ser **developer friendly.**
-   Con el sharding se pueden multiplicar las transacciones de la _blockchain_(aproximadamente 100,000 por segundo)
-   Near permite manejar nuestra identidad mediante dapps, tokens, y alojar o ejecutar contratos inteligentes
-   Tipos de cuentas:
    -   **Top Level Accounts:** Cuentas principales o raíz en NEAR `minombre.near` o `0x13a...` ligados a tu llave privada por medio de un contrato (uno solo por cuenta)
        -   Permite el uso de separadores `. - _`
        -   Debe tener de 2 a 64 caracteres
        -   No puede tener 2 separadores continuos ni comenzar con un separador
        -   Las cuentas solo pueden tener caracteres alfanuméricos
    -   **Sub Accounts:** Similar a los subdominios de sitios web. Permite desplegar contratos y manejar assets `contrato.minombre.near`
        -   Solo se puede crear subdominios un nivel hacia arriba
            -   `hola.soy.near` solo podría crear `hey.hola.soy.near`
    -   **Testnet Accounts:** Cuentas que corren en la red testnet de NEAR
-   Wallets:

    -   [Mainnet](https://wallet.near.org)
    -   [Testnet](https://wallet.testnet.near.org)
    -   Diferencias con Ethereum

        |                       | Ethereum                                 | NEAR                                        |
        | --------------------- | ---------------------------------------- | ------------------------------------------- |
        | Identificador Público | _Public Key_ (0xa...)                    | Account ID (xxxx.near o 0xa...)             |
        | Identificador Privado | _Private Key_ (0xa...)                   | Multiples _Keypairs_ con permisos           |
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

## Sesión 2

-   **Web 3.0:** No es el futuro, pero es una tecnología muy importante, es una bifurcación del internet (un branch del protocolo)

    -   Una ideología de la privacidad y la descentralización

-   **Identidad:**
    -   En Web 2.0 usamos nuestra identidad e información como moneda de cambio
        -   Propicia el mal uso de la información
    -   En la Web 3.0 la identidad está más protegida
        -   La identidad se protege ya que no debes dar tus datos personales

### Los 3 grandes de la descentralización en NEAR

-   **NFTs y FTs:** Son los tokens de las redes, los fungibles (tokens nativos y de utilidad) que se pueden dividir e intercambiar y los no fungibles que no se pueden dividir (representan objetos del mundo real o digital, se representan en un _smart contract_ no se pueden repetir).
    -   Mercados de NFTs en ejemplo: `Mintbase` `Paras` `Nativo NFT`
-   **DeFi:** Finanzas descentralizadas que se ejecutan en _smart contracts_ dentro de una _blockchain_
    -   Ejemplos de DeFi: `Ref finance` `Meta pool` `Aurora`
-   **DAOs:** Organizaciones Autónomas Descentralizadas que utilizan _blockchain_ y _smart contracts_ para la organización y distribución de riqueza de manera transparente, inmutable, autónoma y segura.
    -   Astro DAO y Sputnik DAO son las principales DAOs de NEAR

### Redes de NEAR

    -   Mainnet:
        -   Producción
        -   Persistencia garantizada
    -   Testnet:
        -   Pruebas previas a despliegue
        -   Emula el comportamiento de la mainnet
        -   Selección predeterminada en `near-cli`
    -   Betanet:
        -   Red pública para pruebas del nearcore, se reinicia constantemente
        -   Busca probar estabilidad y compatibilidad
        -   Tiene funciones que aún no han sido estabilizadas
        -   El estado no está garantizado
    -   Localnet:
        -   Dirigido a desarrolladores, tú generas los nodos (como EVM London de Remix)
        -   Es local y te da control total sobre el comportamiento de la red

-   Las redes se exploran en los exploradores de bloques de cada red
-   Yocto es la unidad mínima de medida de un near (como un satoshi o un wei)

### Herramientas de desarrollo

-   La más importante es la [NEAR CLI](https://docs.near.org/tools/near-cli)
-   Se puede usar el SDK de [JavaScript](https://docs.near.org/tools/near-sdk-js) o [Rust](https://docs.near.org/sdk/rust/introduction)

### Aurora

-   Un smart contract que permite trabajar con la EVM
-   Es un ecosistema que permite usar el ecosistema de Ethereum usando las ventajas de NEAR
-   Aurora+ es el programa para usar Aurora con 50 transacciones gratuitas al mes

### Rainbow Bridge

-   Permite tener interoperabilidad entre diversas _blockchains,_ permitiendo iniciar sesión desde cualquier _blockchain_
-   Para usar Aurora se necesita Solidity, en NEAR el más utilizado es Rust

## Sesión 4

### Proyectos en NEAR

-   Una de las más completas páginas de consulta de las DApps de NEAR es [awesomenear](https://awesomenear.com)
-   El _marketing_ en Web3 es más difícil porque es privado
-   El código de las DApps es libre
    -   Las auditorías son muy caras pero necesarias para validar tu proyecto
    -   Muchos proyectos que han sido atacados se convierten en la base de nuevos proyectos
-   Contratos:

    -   El contrato se encuentra en `lib.rs` por convención
    -   En la web3 se deben hacer siempre tests
    -   Rust no es un lenguaje orientado a objetos
    -   Ejemplos:

        ```Rust
        #[payable] // Public - People can attach money
        pub fn donate(&mut self) -> U128 {
        // Get who is calling the method
        // and how much $NEAR they attached
        let donor: AccountId = env::predecessor_account_id();
        let donation_amount: Balance = env::attached_deposit();

        let mut donated_so_far = self.donations.get(&donor).unwrap_or(0);

        let to_transfer: Balance = if donated_so_far == 0 {
            // Registering the user's first donation increases storage
            assert!(donation_amount > STORAGE_COST, "Attach at least {} yoctoNEAR", STORAGE_COST);

            // Subtract the storage cost to the amount to transfer
            donation_amount - STORAGE_COST
        }else{
            donation_amount
        };

        // Persist in storage the amount donated so far
        donated_so_far += donation_amount;
        self.donations.insert(&donor, &donated_so_far);

        log!("Thank you {} for donating {}! You donated a total of {}", donor.clone(), donation_amount, donated_so_far);

        // Send the money to the beneficiary
        Promise::new(self.beneficiary.clone()).transfer(to_transfer);

        // Return the total amount donated so far
        U128(donated_so_far)
        }
        ```

    -   Almacenamiento de los contratos:
        -   Toda la información se almacena en la _blockchain de NEAR_ usando pares de `key/value`
        -   Estos datos almacenados se pueden consultar por medio de los métodos disponibles en las SDKs disponibles para NEAR
            -   [JavaScript](https://github.com/near/near-sdk-js)
            -   [Rust](https://github.com/near/near-sdk-rs)
            -   [AssemblyScript](https://github.com/near/near-sdk-as)
        -   **_Storage Staking (State Staking)_**
            -   Cada contrato desplegado en la red tiene un costo por almacenamiento
            -   La cuenta que poseé el contrato debe bloquear un monto de tokens equivalente a la cantidad de datos que posee el contrato (1 MB -> 10 NEARS)
                -   Más caro que el almacenamiento tradicional
                -   Los datos se almacenan criptográficamente y son inmutables
                -   Los tokens se liberan cuando los datos se borran
    -   Funciónalidad de los contratos:
        -   Los contratos son el backend de la aplicación
        -   En NEAR se compilan con [WebAssembly](https://webassembly.org) (WASM)
    -   Epoch:
        -   Un **epoch** es una unidad de tiempo cuando los validadores de la red permanecen constantes
        -   La duración del epoch en _testnet_ y _mainnet_ es de ~12 horas o 43,200 segundos
    -   Indexer:
        -   Es una librería incluida con [nearcore](https://github.com/near/nearcore)
        -   Es un nodo en la red que escucha el stream de datos conforme es escrito en la _blockchain_
        -   Este stream de datos puede ser escrito después en una base de datos permanentes para análisis usando un lenguaje de _queries_ como SQL

---

## Documentación

-   [NEAR Docs](https://docs.near.org/)
-   [Aurora](https://doc.aurora.dev)

[^1]: Se abrevia PoS
[^2]: Los nodos se dividen en piezas más pequeñas llamadas _chunks (Nightshade)_
