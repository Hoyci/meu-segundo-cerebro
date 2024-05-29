Container networks refere-se a habilidade que os containers possuem de se comunicarem entre si.

Containers possuem a capacidade de se conectar à internet e a outras redes por padrão. Isso significa que ele pode acessar sites, servidores, acessar uma API, baixar arquivos e outras coisas.

O container não possui a capacidade de saber em que tipo de rede está conectado. Com isso, quero dizer que ele não sabe se está conectado a uma rede local, na internet pública, se comunicando com outros containers Docker ou com servidores.

Um container consegue ver apenas informações como: 
* Endereço de IP
* Gateway
* Serviços DNS

Existem alguns tipos de drivers de rede que pode ser usado com docker:
* [[None]]
* Host
* Bridge



