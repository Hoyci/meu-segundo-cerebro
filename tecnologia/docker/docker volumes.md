Docker volumes são uma maneira de persistir e compartilhar dados entre containers e o host. Em resumo, volumes são usados para armazenar dados que precisam sobreviver ao ciclo de vida dos containers, ou seja, dados que não devem ser perdidos quando um container é removido ou recriado.

## Tipos de volumes
* **Volume nomeado**: Criado e gerenciado pelo docker com um nome específico
* **Bind mounts**:: Monta um diretório específico do sistema de arquivos do host no container.


## Criando um volume nomeado

Criar um volume:
```bash
docker volume create meu-volume
```

Usar o volume em um container:
```bash
docker run -d --name meu-container -v meu
```