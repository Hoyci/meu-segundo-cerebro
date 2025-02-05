# ConfigMap

**ConfigMap** é uma forma de armazenar dados de configuração não sensíveis em formato de chave-valor. Ele permite separar as configurações da aplicação do próprio código, o que facilita a alteração dos parâmetros sem a necessidade de reconstruir a imagem do container.

Os dados salvos no configMap podem ser usados para: 
- **Variáveis de ambiente:** Injetando valores diretamente nos containers.
- **Argumentos de inicialização ou configurações de comando.**

Exemplo prático de configMap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: minha-config
data:
  APP_MODE: "production"
  LOG_LEVEL: "debug"
```