# Kubernetes

Kubernetes é um ferramenta open-source para orquestração de containers [[docker]] desenvolvida pelo Google.
Orquestração nesse caso significa que Kubernetes ajuda a gerenciar aplicações que são construída a partir de dezenas, centenas ou milhares de containers em diferentes ambientes (Máquinas físicas, máquinas virtuais ou ambientes de Clouds).
# Quais problemas Kubernetes Resolve?

Primeiro é necessário explicar que o crescimento do uso da arquitetura de microsserviços causou o aumento do uso da tecnologia de containers porque eles oferecem o ambiente perfeito para aplicações pequenas e independentes. E como nessa arquitetura são utilizados centenas, ou até mesmo milhares, de aplicações (com ambientes e tecnologias diferentes) que juntas formam um sistema, surgiu a necessidade de algo para orquestrar o funcionamento de todas essas pequenas partes como uma única coisa.
Além da orquestração, o Kubernetes resolve outro problema muito comum nesse tipo de arquitetura que é a garantia de resiliência. Isso significa que, a ferramenta é capaz de fazer: 
* **Self-healing da aplicação**: Reinicia os[[ container]]s/pods que falham, substituí os nós não responsivos e garante que o estado desejado da aplicação seja mantido.
* **Escalabilidade sob demanda**: Automaticamente a ferramenta ajusta o número de containers/pods com base na demanda, podendo ser de CPU, memória ou outras métricas.
* **Gestão de secrets**: Centraliza dados sensíveis (como senhas) de forma segura, separando-os do código da aplicação.
* **Rollouts e rollbacks automatizados**: Permite atualizações graduais e reversão imediata em caso de falhas, garantindo alta disponibilidade.
# Arquitetura do Kubernetes 

O cluster do Kubernetes é compose pelo control panel e pelos worker nodes. 
O control panel, que pode ser constituído por um ou mais master nodes, inclui os seguintes componentes: 
* **API Server**: Ponto central de comunicação onde todos comandos do kubernetes (exemplo: kubectl logs ...) são recebidos e validados.
* **Scheduler**: Responsável por designar os pods aos worker nodes com base em critérios de recursos e restrições.
* **Controller Manager**: Monitora o estado do cluster e gerencia os controladores que asseguram que o estado atual se aproxime ao máximo do estado desejado.

Já os worker nodes são os nós onde as aplicações realmente rodam. E cada worker node executa as seguinte coisas:
* **Kubelet**: Agente que garante que os [[container]]s estão executando conforme definido nos pods e comunica o status ao control panel
* **Container runtime**: Responsável por baixar as imagens e executar os containers, normalmente sendo utilizado com docker mas pode ser utilizado com containerd ou CRI-O
* **Kube-Proxy**: Coordena o tráfego de rede entre os pods e os serviços para garantir a comunicação interna do cluster.

Nos worker nodes, as aplicações são executadas dentro de **pods**. Essa estrutura permite que as aplicações sejam facilmente escaláveis e que a carga de trabalho seja distribuída de forma eficiente entre os nós.

Além disso, o Kubernetes adota uma abordagem declarativa para a configuração, permitindo que o estado desejado do sistema seja definido por meio de arquivos de manifesto (YAML/JSON). Isso facilita a automação, o versionamento e a recuperação de falhas, além de suportar práticas de CI/CD e infra as code.