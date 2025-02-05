# Service
**Service** é uma abstração que fornece um endereço de IP virtual que permanece estático independente das mudanças nos pods associados, haja vista que eles são temporários e mudam de endereço de IP quando recriados. 
# Como funciona?
Quando você cria um Service, você normalmente define um seletor (selector) que indica quais Pods devem ser associados a esse Service. Por exemplo, se os Pods tiverem uma _label_ `app: meu-app`, o Service pode usar um selector `app: meu-app` para englobar todos esses Pods.
Nesse sentido, o Kubernetes mantém uma lista de endpoints (os endereços IP e portas dos Pods) que correspondem ao seletor definido. Quando uma requisição chega ao Service, ela é redirecionada para um desses endpoints, de acordo com a política de balanceamento de carga, o que melhora a escalabilidade e a resiliência da aplicação.
Além disso, aplicações podem usar o Service para encontrar e se comunicar com outros componentes da aplicação, sem precisar conhecer detalhes de quais Pods estão em execução. Essa descoberta é feita por meio do DNS interno do Kubernetes ou das variáveis de ambiente injetadas nos Pods.
# Tipos de Service
* **ClusterIP (padrão):**
	Cria um endereço IP interno no cluster. Só é acessível de dentro do cluster. Ideal para comunicação interna entre Pods.
- **NodePort:**
	Abre uma porta em cada Node do cluster e redireciona o tráfego recebido nessa porta para o Service. Isso permite acesso externo ao Service, mas com algumas limitações e sem balanceamento de carga nativo entre Nodes (a menos que seja configurado externamente).
- **LoadBalancer:**
	Em ambientes de nuvem, esse tipo solicita automaticamente a criação de um balanceador de carga externo (por exemplo, AWS ELB, Google Cloud Load Balancer) que distribui o tráfego para os Nodes, que por sua vez encaminham para o Service. Essa é uma forma prática de expor um Service para a internet.
- **ExternalName:**
	Em vez de criar um proxy, esse Service mapeia um nome DNS para outro nome externo. É usado para integrar serviços externos ao cluster sem gerenciar um conjunto de endpoints manualmente.

Exemplo prático de um service:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: meu-app-service
spec:
  selector:
    app: meu-app
  ports:
    - protocol: TCP
      port: 80         # Porta do Service (acessível para os clientes)
      targetPort: 8080 # Porta no Pod onde a aplicação está rodando
  type: ClusterIP    # Tipo padrão, disponível apenas dentro do cluster
```