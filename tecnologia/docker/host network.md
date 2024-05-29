Host network é uma configuração que permite que um container compartilhe a pilha de rede host. Isso significa que o container não terá sua própria interface de rede isolada e sim que ele usará diretamente a rede do computador/máquina virtual/cloud que executou o comando `docker run`, como se fosse um processo nativo rodando no host.

Deve ser usando quando deseja-se ter:
* **Desempenho de rede**: quando você precisa de um desempenho de rede superior, evitando a sobrecarga de virtualização de rede.
* **Acesso direto a serviços do host**: quando o container precisa acessar serviços locais no host diretamente sem passar pelo NAT (network address translation)
* **Configurações simples de rede**: quando você quer simplificar a configuração de rede, evitando a necessidade de expor e mapear portas entre o host e o container.

### Necessário levar em consideração que o driver host só funciona em sistemas operacionais baseados em linux.

## Como funciona?

Para criar e executar um container usando o driver de rede host você pode usar o comando `dokcer run -d --name my-container --network host` 

### Exemplo de uso

Arquivo dockerfile para servidor web usando NGINX
```
FROM nginx:apline
COPY index.html /usr/share/nginx/html/index.html
```

Arquivo HTML 
```
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Servidor Web no Docker</title>
</head>
<body>
    <h1>Olá, Mundo!</h1>
    <p>Este é um servidor web rodando em um container Docker com rede host.</p>
</body>
</html>
```

Construindo a imagem docker
`docker build -t meu-servidor-web .`

Executando o container com rede host
`docker run --network host meu-servidor-web`

Nesse caso, o servidor web dentro do container está usando NGINX e porta padrão desse serviço é a 80. Sendo assim, podemos acessar o servidor web usando o enderço `http://localhost:80`

