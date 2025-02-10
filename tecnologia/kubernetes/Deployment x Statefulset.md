# Deployment

Deployment é um recurso do kubernetes que, de forma declarativa, você informa quantas réplicas de um Pod devem estar em execução, qual imagem de container utilizar, quais variáveis de ambiente configurar.
Deve se levar em consideração que deployment é ideal para aplicações stateless, como servidores web, APIs e serviços que podem ser escalados horizontalmente sem depender de uma identidade única ou armazenamento persistente associado a cada instância.
## Principais pontos:

* **Gerenciamento Declarativo**: 
	No Deployment, você declara o estado desejado da sua aplicação, definindo, por exemplo, quantas réplicas de um Pod devem estar em execução, qual imagem de container utilizar, quais variáveis de ambiente configurar, entre outros detalhes. O Kubernetes então se encarrega de garantir que o estado atual do cluster se ajuste ao estado declarado.
	
* **Uso de ReplicaSets**:
	Ao criar um Deployment, ele automaticamente gera um **ReplicaSet** para gerenciar os Pods. Esse ReplicaSet é responsável por manter o número especificado de réplicas sempre ativo. Se algum Pod falhar, o ReplicaSet criará um novo para repor a falha.
	
* **Atualizações e Rollbacks**: 
	Uma das grandes vantagens do Deployment é a capacidade de realizar **rolling updates** (atualizações progressivas) sem causar interrupções no serviço. Se uma nova versão da aplicação é lançada, o Deployment gradualmente substitui os Pods antigos pelos novos. Além disso, se algo der errado durante a atualização, você pode fazer um rollback para a versão anterior de forma simples e rápida.

# StatefulSet
**StatefulSet** é um recurso do Kubernetes que, de forma declarativa, você informa quantas réplicas de um Pod devem estar em execução, qual imagem de container utilizar e quais configurações de ambiente aplicar.
Diferente do **Deployment**, o **StatefulSet** é ideal para aplicações que precisam manter uma identidade única entre réplicas e que geralmente dependem de armazenamento persistente.
Isso é importante para bancos de dados, sistemas distribuídos e qualquer aplicação que precise que cada instância (Pod) tenha um nome fixo, um volume específico e uma ordem de inicialização e desligamento.

## Principais pontos:

* I**dentidade Estável dos Pods:**  
	Cada Pod gerenciado por um StatefulSet recebe um nome único e previsível (por exemplo, `minhaapp-0`, `minhaapp-1`, etc.). Essa identidade estável é crucial para aplicações que precisam se reconhecer ou se comunicar de forma ordenada, como bancos de dados ou sistemas de mensageria.*
	
* **Ordem de Criação e Atualização:**  
	O StatefulSet garante uma ordem específica tanto para a criação quanto para a exclusão dos Pods. Por exemplo, durante a criação, o Pod `minhaapp-0` será criado e estará pronto antes do `minhaapp-1`. Essa ordem é importante para manter a integridade de aplicativos distribuídos que dependem de uma sequência correta para inicialização.
	
* **Persistência de Dados com VolumeClaimTemplates:**  
	Um dos pontos fortes do StatefulSet é a capacidade de associar volumes persistentes a cada Pod individualmente, utilizando _VolumeClaimTemplates_. Dessa forma, mesmo que um Pod seja reiniciado ou reimplantado, o volume associado (que armazena os dados) permanece, garantindo a continuidade dos dados. Essa abordagem é fundamental para bancos de dados, caches e outros serviços que exigem armazenamento duradouro.
	
* **Cenário de Uso:**  
	O StatefulSet é recomendado para aplicações que necessitam de armazenamento persistente e que requerem que cada instância mantenha uma identidade única. Exemplos típicos incluem bancos de dados como PostgreSQL, MySQL, MongoDB, sistemas de armazenamento de chave-valor e aplicações que formam clusters onde a ordem e a persistência são essenciais.