# Secret
**Secret** é utilizado para armazenar informações sensíveis, como senhas, tokens, chaves de API e certificados. Como essas informações são confidenciais, o Kubernetes trata os Secrets com mais cuidado.
Embora os dados sejam codificados em Base64 (o que não é uma forma de criptografia), eles não ficam expostos de forma direta em arquivos de configuração.
Em ambientes de produção, é comum utilizar mecanismos adicionais para proteger os Secrets, como integrações com ferramentas de gerenciamento de chaves (ex.: HashiCorp Vault) ou configurar o Kubernetes para armazenar Secrets de forma criptografada no etcd.

Exemplo prático de secret:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: minha-senha
type: Opaque
data:
  username: dXNlcm5hbWU=   # "username" codificado em Base64
  password: c2VuaGFzZW1h   # "senhasema" codificado em Base64
```