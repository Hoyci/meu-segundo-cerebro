# Volume
Volumes são recursos que permitem o armazenamento e a persistência dos dados utilizados pelos containers. Diferentemente do armazenamento de um container que perde todos os seus dados armazenados quando é reiniciado ou destruído, os volumes servem para que você possa persistir e compartilhar os dados entre containers e pods.

# Tipos de volumes
* **EmptyDir**: Cria um volume vazio quando o pod é agendado e persiste os dados enquanto o pod estiver rodando. Esse tipo é útil para quando é necessário fazer armazenamento temporário, cache ou compartilhar dados entre containers do mesmo pod.
* **hostPath**: Monta um diretório ou arquivo no sistema de arquivos do host, vulgo a máquina/node que está rodando o pod. Esse tipo é normalmente utilizado para tarefas de diagnóstico ou logs.
* **nfs (Network File System):** Permite montar um compartilhamento NFS, possibilitando que vários Pods, possivelmente em nós diferentes, acessem os mesmos dados. Ideal para armazenamento compartilhado entre múltiplos Pods e para persistência de dados.
* **persistentVolume (PV) e persistentVolumeClaim (PVC):**
	Os dois são usados em conjunto e normalmente são utilizados para fazer armazenamento e persistência de dados de bancos de dados como postgres, mongodb, mysql e etc.
	-  **PersistentVolume (PV):** É um recurso de armazenamento no cluster que foi provisionado diretamente no cluster ou dinamicamente via StorageClass. Dessa maneira, faz sentido pensar como se você estivesse plugando um HD/SSD dentro do seu cluster para que seja possível armazenar e persistir os dados. 
		- **Storage Class**: Trabalhando com ambientes de nuvem (como AWS, GCP ou Azure),  um StorageClass abstrai a complexidade de lidar com um hardware físico como HD/SDD para que você não tenha que se preocupar com detalhes como o tipo de disco ou sua localização física. Você pode usar EBS na AWS ou Persistent Disk no GCP.
	- **PersistentVolumeClaim (PVC):** é o pedido para utilizar uma determinada quantidade de espaço de armazenamento. Ou seja, ao inves de se preocupar em selecionar manualmente um volume específico, você simplesmente declara quanto espaço e que tipo de acesso (por exemplo, leitura e escrita) você precisa para sua aplicação.

Exemplo prático de um volume:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-com-volume
spec:
  volumes:
    - name: meu-volume
      emptyDir: {}   # Aqui estamos usando o tipo emptyDir
  containers:
    - name: app-container
      image: nginx
      volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: meu-volume
```
