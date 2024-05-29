Brigde network é a configuração padrão para containers docker. Quando você criar um container, ele é automaticamente coenctado a uma rede bridge, a menos que você especifique outra rede.

## Características

1. **Isolamento**: Cada container na rede brigde tem seu próprio endereço de IP
2. **Comunicação entre containers**: Containers da mesma rede bridge podem se comunicar usando os endereços de IP internos
3. **Exposição de portas**: Para que seja possível acessar o container fora da rede brigde é necessário mapear suas portas para as portas do host.

## Como funciona?

A rede bridge é uma rede internado no host docker que permite que os containers conectados a ela se comuniquem entre si. Essa rede é isolada da rede externa (como a internet ou a rede local do host), a menos que você exponha portas específicas.

## Comandos básicos

* Ver a rede bridge padrão
	`docker network ls` 
	