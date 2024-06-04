None network é uma configuração que desabilita completamente a conectividade de rede do container. Isso significa que o container não terá nenhuma interface de rede configurada e não poderá se comunicar com outros containers, host ou com a internet.

Deve ser usando quando deseja-se ter:
* **Isolamento completo**: Quandoo você precisa de um container que não deve ter nenhuma comunicação de rede.
* **Segurança**: Para aumentar a segurança, impedindo que o container acesse ou seja acessado por qualquer rede.
* **Testes**: Quando você está realizando testes que não necessitam de rede ou onde a rede pode interferir nos resultados.

## Como funciona?

Para criar e executar um container usando o driver de rede none você pode usar o comando `dokcer run -d --name isolated-container --network none` 
