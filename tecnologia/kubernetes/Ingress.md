# Ingress
**Ingress** é um objeto de API que expõe rotas HTTP e HTTPS e define regras para gerenciar o acesso externo aos serviços do cluster.
Ele serve para que ao invés de expor cada serviço individualmente com um IP fixo ou um balanceador de carga separado, atue como uma porta de entrada única, onde você pode configurar regras baseadas em nomes de domínio ou caminhos de URL para redirecionar o tráfego para os serviços internos corretos.

**Exemplo:** 
Imagine que você tem dois serviços, sendo uma API e um servidor Web.
Você pode configurar o ingress para que todas as requisições para o endereço https://meu-app.com/api seja redirecionada para o serviço responsável pela sua API, enquanto requisições feitas para o endereço https://meu-app.com/ sejam redirecionadas para o serviço responsável pela sua interface web.

![[ingress-chart.png]]
**Exemplo prático de Ingress:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: meu-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  tls:
  - hosts:
    - exemplo.dominio.com
    secretName: tls-secret
  rules:
  - host: exemplo.dominio.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: meu-servico-api
            port:
              number: 80
	  - path: /
        pathType: Prefix
        backend:
          service:
            name: meu-servico-web
            port:
              number: 81

```

# Ingress controller

**Ingress controller** é o componente que implementa as regras criada no ingress e atua como um proxy reverso para direcionar as requisições para os serviços internos.
Além disso, ele pode lidar com as conexões SSL/TLS para poder processar os certificados digitais e converter conexões HTTPS em HTTP para os serviços internos, simplificando a configuração de segurança.