No kubernetes, um pod é a menor parte da ferramenta. Ele representa um conjunto de um ou mais containers que compartilham os mesmos recursos (como rede e armazenamento).
Os pods não são permanentes, isso significa que quando um pod falha ou é encerrado, um novo pod pode ser criado pelo kubernetes.


# Tipos de pods
1.  **Pod com um único container**: Esse é o pod mais comumente usado. 
	Deve ser usado quando: 
	 - Os containers são independentes, ou seja, não dependem diretamente de nenhum outro para sua existência.
	 - Os containers precisam escalar de forma independente
	 - Os containers não precisam compartilhar a rede e volumes
2. **Pod com múltiplos containers**: Esse tipo de pod é utilizado em casos específicos.
	Deve ser usado quando: 
	- Todos os containers compartilham a mesma rede, assim eles podem se comunicar usando localhost.
	  Exemplo: 
		  O container principal executa uma API, enquanto o container secundário (sidecar) executa uma funcionalidade complementar como colegar logs da API e enviar para um serviço externo como Prometheus.
	- Quando dois processos precisam estar sempre juntos e compartilhar dados diretamente.
	  Exemplo: 
		  Um container executa um **banco de dados em memória (Redis, SQLite)**, enquanto outro container usa esse banco diretamente.

# Como criar um pod?

1. - O usuário cria um Pod através de um **YAML Manifest** ou com comandos como `kubectl run`.
2. O **Kubelet** (agente do Kubernetes rodando nos nodes) recebe a instrução para rodar o Pod.
3. O **Scheduler** decide em qual Node esse Pod será executado.
4. O **Container Runtime** (como Docker, containerd ou CRI-O) executa os containers dentro do Pod.
5. O Kubernetes mantém o estado do Pod conforme especificado no deployment (pode recriar se necessário).

Exemplo de YAML:
``` YAML
apiVersion: v1
kind: Pod
metadata:
  name: meu-pod
  labels:
    app: meu-app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

Comandos para rodar o YAML acima
1. kubectl apply -f meu-pod.yaml
2. kubectl get pods
3. kubectl logs meu-pod