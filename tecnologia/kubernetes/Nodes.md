Um node no contexto de kubernetes é uma máquina física ou virtual que compõe o cluster e fornece recurso (CPU, memória, rede) para executar os [[pods]]. 
Essa máquina roda um sistema operacional que pode variar de acordo com a infraestrutura e as necessidades, mas a maioria dos clusters usam distribuições linux.

Deve-se ter em mente que quando instalamos o K3s numa máquina física, essa máquina acaba desempenhando o papel de master (vulgo control panel) e worker (Node que executa os pods)  para simplificar a implantação.
Mas em cenários maiores, como ambientes de produção de grandes empresas, você pode ter um nodes dedicados ao control panel e outros que funcionam apenas como workers.

Um node hospeda os componentes essenciais como **kubelet** e o **kube-proxy**

Para ter um cluster kubernetes de alta disponibilidade, faz sentido que você possua 4 máquinas (EC2 ou máquinas físicas) sendo:
* **Control Plane (Masters)**:
	3 nós dedicados ao control plane (masters) sendo:
	*  1 para o **ETCD** que é um banco de dados que armazena o estado do cluster
	* 2 para os nodes master para que caso um venha a falhar o outro entre em ação para manter a disponibilidade 
* **Worker Nodes**:
	Em um ambiente de produção, é comum ter vários nós workers para distribuir a carga e garantir a escalabilidade e resiliência. Então sendo assim, você pode ter quantos nodes você quiser a depender da carga que seu sistema demanda.
