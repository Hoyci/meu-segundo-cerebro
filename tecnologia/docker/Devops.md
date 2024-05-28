# Fase 1: Docker Básico

* O que é [[docker]]? O que é um [[container]]? O que é uma [[imagem]]?
* [[Arquitetura de docker]]: O que é [[docker engine]]? O que é[[ Docker hub]]? O que é [[docker CLI]]? O que é [[docker compose]]?
* Comandos básicos de docker e o que fazem?: `docker run`, `docker build`, `docker pull`, `docker push`, `docker-compose up`
* Entender a estrutra e as instruções usada em um dockerfile
## Projeto

Criar um dockefile para uma simples aplicação web utilizando NGINX.  Build, rode e envie a imagem para o docker hub.

# Fase 2: Networking e Volumes 

* O que é [docker networks](https://docs.docker.com/network/)? o que são brides networks? o que são host networks? o que são overlay networks? Como criar e gerenciar networks com docker? 
* O que são [docker volumes](https://docs.docker.com/storage/volumes/)? O que são bind mounts, suas diferenças e casos de uso? Como persistir data com docker?

## Projeto

Criar um arquivo docker compose para uma aplicação multi-container (backend e banco de dados) implementando custom networking e persistência de dados entre volumes

# Fase 3: Docker compose e orquestração

* O que é [docker compose](https://docs.docker.com/compose/)? qual a sintaxe de um arquivo docker compose? Como definir serviços, networks e volumes?
* O que é [docker swarm](https://docs.docker.com/engine/swarm/)? Como configurar um swarm cluster? Como fazer deploy de serviços? Como escalar aplicações? Como gerenciar stacks?

## Projeto
Construa um docker compose contendo multiplos serviços interconectados (front, back e banco de dados)


# Fase 4: Segurança com Docker

* Quais são as boas práticas de segurança para containers? 
* Rodando como usuário não-root
* Como gerenciar secrets?
* Como verificar vulnerabilidades de uma imagem? 
* O que é signing images?
* O que é docker content trust?

## Projeto

Adicione o conhecimento dessa fase na aplicação da fase 3.

# Fase 5: CI/CD com Docker
* O que é [continuos delivering](https://docs.docker.com/ci-cd/)?
*  O que é [continuous integration](https://docs.docker.com/ci-cd/)? 

## Projeto

Adicione um pipeline CI/CD na aplicação da fase 3 utilizando serviços como Github Actions para buildar, testar e deployar os containers docker.

# Fase 6: Introdução a Kubernetes

* O que é kubernetes? Qual a sua arquitetura? Quais são seus principais conceitos (pods, service, deployment) e para o que servem?
* Como fazer deploy de aplicações dockerizadas no kubernetes?

## Projeto
Faça deploy da aplicação da fase 3 utilizando um cluster local de kubernetes com [Minikube](https://kubernetes.io/pt-br/docs/tutorials/hello-minikube/) ou algo semelhante
# Fase 7: Monitoramento

* Como [coletar métricas](https://prometheus.io/docs/introduction/overview/) sobre a performance, uso de recursos e outros aspectos importantes da aplicação?
* Como [capturar logs ](https://www.elastic.co/pt/elastic-stack/) como mensagens de erro, avisos e mensagens de informação?
* O que é tracing? como adicionar Jaeger para aplicações? O que é [Jaeger](https://www.jaegertracing.io/)?
* O que é [alerting](https://prometheus.io/docs/alerting/latest/alertmanager/)? 
* O que é [Grafana](https://grafana.com/docs/grafana/latest/dashboards/)?