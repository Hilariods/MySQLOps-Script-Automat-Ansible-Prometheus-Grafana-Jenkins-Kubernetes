
## Documentação de Nível DBA Sênior

### Visão Geral do Projeto

O objetivo deste projeto é configurar e operar uma aplicação utilizando MySQL, integrando tecnologias como Ansible para automação de backup/recuperação, Prometheus e Grafana para monitoramento, Jenkins para automação de deploy, e Kubernetes para garantir alta disponibilidade e escalabilidade.

## Configuração de MySQL em Docker

### Passos:

#### docker-compose.yml:

Utilizamos o Docker Compose para definir e configurar o ambiente do MySQL. O arquivo `docker-compose.yml` especifica a versão do Docker Compose e configura os serviços necessários para executar o MySQL. Definimos variáveis de ambiente como `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER` e `MYSQL_PASSWORD` para configurar o banco de dados. Utilizamos volumes Docker para persistência de dados, garantindo que os dados do MySQL sejam mantidos mesmo após a reinicialização do contêiner.

#### População do Banco de Dados:

Criamos um script SQL (`init.sql`) para inicializar o esquema do banco de dados e popular com dados iniciais. Utilizamos o comando `docker exec` para executar o script SQL dentro do contêiner MySQL e popular o banco de dados com dados de exemplo.

## Backup e Recuperação com Ansible

### Passos:

#### backup.yml:

Criamos um playbook Ansible (`backup.yml`) para automatizar o processo de backup do MySQL. Utilizamos o módulo `mysql_db` para realizar o dump do banco de dados para um arquivo `.sql`.

#### restore.yml:

Criamos um playbook Ansible (`restore.yml`) para automatizar a recuperação do MySQL a partir de um backup. Utilizamos novamente o módulo `mysql_db` do Ansible para importar o arquivo `.sql` de backup para o banco de dados MySQL.

## Monitoramento com Prometheus e Grafana

### Passos:

#### prometheus.yml:

Configuramos o Prometheus para coletar métricas do MySQL. Definimos no arquivo de configuração `prometheus.yml` o job `mysql` com o endpoint para scraping das métricas do MySQL.

#### Configuração do Grafana:

Configuramos o Grafana para visualizar as métricas coletadas pelo Prometheus. Criamos dashboards personalizados no Grafana para monitorar o desempenho e a saúde do MySQL, incluindo gráficos de uso de CPU, memória, operações de leitura e gravação, entre outros.

## Automação de Deploy com Jenkins

### Passos:

#### Configuração do Job no Jenkins:

Configuramos um job freestyle no Jenkins para automatizar o processo de deploy da aplicação. Configuramos a integração com o repositório Git (por exemplo, GitHub) para buscar o código fonte da aplicação.

#### Pipeline de Deploy:

Definimos os estágios do pipeline no Jenkins para compilar, testar e implantar a aplicação no Kubernetes. Utilizamos o plugin Kubernetes do Jenkins para interagir com o cluster Kubernetes e aplicar os manifests de deployment.

## Alta Disponibilidade com Kubernetes

### Passos:

#### deployment.yaml:

Criamos um manifesto Kubernetes (`deployment.yaml`) para definir a configuração de implantação da aplicação. Especificamos o número de réplicas (`replicas`) para garantir alta disponibilidade da aplicação.

#### Implantação no Kubernetes:

Utilizamos o comando `kubectl apply` para aplicar o manifesto `deployment.yaml` e implantar a aplicação no cluster Kubernetes. Configuramos estratégias de replicação e balanceamento de carga para distribuir o tráfego entre as réplicas da aplicação e garantir a escalabilidade horizontal.

## Conclusão

Este projeto abrange desde a configuração inicial do banco de dados MySQL até a implantação da aplicação em um ambiente Kubernetes, passando por automação de backup/recuperação com Ansible, monitoramento com Prometheus/Grafana e automação de deploy com Jenkins. Cada passo foi desenhado para garantir a operação eficiente, segura e escalável da aplicação utilizando tecnologias modernas.
```
