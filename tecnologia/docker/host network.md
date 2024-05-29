Host network é uma configuração que permite que um container compartilhe a pilha de rede host. Isso significa que o container não terá sua própria interface de rede isolada e sim que ele usará diretamente a rede do computador/máquina virtual/cloud que executou o comando `docker run`, como se fosse um processo nativo rodando no host.

Deve ser usando quando deseja-se ter:
* **Desempenho de rede**: quando você precisa de um desempenho de rede superior, evitando a sobrecarga de virtualização de rede.
* **Acesso direto a serviços do host**: quando o container precisa acessar serviços locais no host diretamente sem passar pelo NAT (network address translation)
* **Configurações simples de rede**: quando você quer simplificar a configuração de rede, evitando a necessidade de expor e mapear portas entre o host e o container.

## Como funciona?

Para criar e executar um container usando o driver de rede host você pode usar o comando `dokcer run -d --name my-container --network host` 

