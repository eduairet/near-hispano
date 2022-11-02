# NEAR Certified Developer

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

