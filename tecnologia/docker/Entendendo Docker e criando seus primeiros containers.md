## Entendendo Docker

`Docker é uma tecnologia que permite empacotar e executar aplicativos de maneira isolada em contêineres.` 

Essa é a explicação mais simples e direta sobre o que é Docker. Eu acho que essa explicação é um pouco simplista e pode gerar muitos questionamentos. Irei usar uma analogia para tentar explicar o que é Docker e alguns de seus conceitos.

Para construir um condomínio é necessário que um arquiteto pense em como serão os apartamentos desse prédio e também é necessário que ele faça alguns documentos capazes de explicar detalhadamente quais são as características de cada tipo de apartamento (leve em consideração que num condomínio existem apartamentos de 1 quarto, 2 quartos, 1 banheiro, 2 banheiros e assim por diante).

Trazendo essa analogia para o mundo de Docker, podemos pensar que o condomínio é a tecnologia Docker em si que permite criar e rodar aplicações utilizando containers que nesse caso são como os apartamentos.

Como dito anteriormente, o arquiteto precisa criar um documento para explicar detalhadamente quais são as características de um apartamento. Nesse documento ele precisa deixar explicito algumas informações sobre o imóvel como: a fundação, as instalações (hidráulica, elétrica e de gás) a planta baixa (layout que mostra a disposição dos ambientes). No mundo de Docker, existe um documento, o qual chamamos de dockerfile, que possui a mesma função desse documento feito pelo arquiteto. Nesse caso, a fundação de um documento Docker seria onde especificamos a imagem base que será utilizada. Especificamos da seguinte maneira: `FROM image:tag`.  As instalações de um apartamento pode se relacionar com as dependências necessárias para a execução da imagem Docker. Ou seja, assim como um apartamento tem dependências essenciais para a utilização do mesmo (água, energia elétrica e gás), uma aplicação pode ter N dependências fundamentais para que seja possível executá-la. A planta baixa numa imagem Docker seria a descrição do diretório de trabalho, ou seja, a disposição das pastas dentro da imagem que especificamos usando `WORKDIR /path/to/your/app`.

O que chamamos de container, pode-se relacionar com a ideia de ser um apartamento. Digo isso porque para que uma família possa habitar dentro de um apartamento, é necessário que o ambiente tenha algumas coisas como: sofá, cama, água, energia elétrica e etc. Dessa mesma maneira, é necessário que um container Docker possua todos os requisitos necessários para rodar uma aplicação. 


## Motivos pelos quais é interessante usar Docker

* **Consistência**: 
* **Isolamento**:
* **Portabilidade**: 
* **Escalabilidade**:

## Criando primeira imagem docker e rodando

## Integrando a imagem criada com banco de dados