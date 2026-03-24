# Tech Challenge Fase 2
Esse repositório tem como finalidade armazenar os códigos e as informações necessárias para a entrega do desafio proposto.

## analytics-service

## auth-service

## evaluation-service

Problema, causa e a solução aplicada evaluation-service

### Problema Encontrado: 
Ao tentar executar o microsserviço isoladamente na máquina host (Windows) utilizando o comando `go run .`, a aplicação retornava erros de `"connection refused"` ou `"host not found"` ao tentar se conectar ao Redis e ao Auth Service.

### Causa Raiz: 
O arquivo `.env` do microsserviço estava configurado com as URLs internas da rede do Docker (ex: REDIS_URL=redis://redis:6379 e AUTH_SERVICE_URL=http://auth-service:8001). O sistema operacional host não consegue resolver esses nomes de DNS internos dos contêineres.

### Solução Aplicada: 
O arquivo `docker-compose.yml` foi ajustado para expor as portas necessárias dos serviços de apoio para a máquina host. Em seguida, as variáveis de ambiente foram injetadas diretamente na sessão do terminal (PowerShell) apontando para o localhost antes da execução do código em Go


## flag-service

## targeting-service 

### **Erros encontrados:**

1. Biblioteca psycopg2-binary na versão 2.9.5 não é compatível com o python 3.14
2. Flask 2.2.2, ao baixar sua dependência werkzeug, baixa a versão mais recente, o que causou uma incompatibilidade entre as versões

### Soluções

1. Foi utilizado o python 3.9 conforme recomendado pelo `README.md`
2. Adicionado o Werkzeug em sua versão 2.2.3 no arquivo de requirements.txt para melhor compatibilidade com o Flask

## Kubernetes
A pasta kubernetes contém os manifests e configurações para rodar os microserviços no cluster, organizados por subpastas por serviço (analytics-service, auth-service, evaluation-service, flag-service, targeting-service). Em cada subpasta há recursos Kubernetes como Deployment, Service, Ingress, Namespace, Secret/ConfigMap e HPA quando aplicável; existem também manifests globais (namespaces, secrets, configMaps) para o conjunto do cluster. Em suma, esses arquivos descrevem como empacotar, expor e configurar os serviços no Kubernetes — e devem evitar armazenar segredos em texto plano, preferindo injeção via CI/GitHub Secrets, SealedSecrets ou um gerenciador de segredos.