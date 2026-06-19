# 📊 AWL Server Monitoring - Prometheus & Grafana

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=docker,prometheus,grafana,linux,github" />
  </a>
</p>

Este repositório contém o setup central de monitoramento da infraestrutura do homelab **awlserver** (Astral Wave Label). 
Localizado em `/mnt/docker-services/server/grafana`, este ecossistema é o responsável pela coleta de métricas e visualização de dashboards de toda a infraestrutura, incluindo a **LoginHub API** e demais serviços do servidor.

## 🚀 Tecnologias Utilizadas

* **Prometheus**: Coleta e armazenamento de métricas de séries temporais (via rotas de `scrape`).
* **Grafana**: Visualização de dados, alertas e dashboards interativos.
* **Docker & Docker Compose**: Orquestração e isolamento do ambiente na rede interna `awl_network`.

## 🛠️ Como Instalar e Rodar

### 1. Configuração da Rede
Os containers utilizam a rede externa do servidor. Caso o servidor seja novo, crie a rede principal:
```bash
docker network create awl_network
```

### 2. Configuração de Ambiente
Crie ou configure o arquivo `.env` local na pasta com as credenciais do administrador e versões das imagens:
```ini
# .env
GRAFANA_USER=admin
GRAFANA_PASSWORD=sua_senha_secreta
PROMETHEUS_VER=v2.50.1
GRAFANA_VER=10.3.3
GF_SERVER_DOMAIN=grafana.astralwavelabel.com
```

### 3. Executando o Projeto (Deploy Padrão AWL)
Para subir ou atualizar os containers no servidor, navegue até o diretório oficial e execute:
```bash
cd /mnt/docker-services/server/grafana
docker compose up -d
/mnt/docker-services/documentacao/scripts/cleancachecloudflare.sh
```
> **Nota:** É obrigatório rodar o script de limpeza de cache do Cloudflare sempre que houver deploy ou alteração nos containers, conforme a política do `awlserver-devops`.

## 🌐 Acesso ao Grafana

O acesso externo é provido via **Cloudflare Tunnel**. O Grafana estará disponível em:
* **URL:** [https://grafana.astralwavelabel.com](https://grafana.astralwavelabel.com)

## 📁 Estrutura do Projeto

```text
/mnt/docker-services/server/grafana/
├── docker-compose.yml   # Configuração e orquestração dos serviços (Prometheus + Grafana)
├── prometheus.yml       # Configurações de jobs e targets do Prometheus (targets de scrape)
├── .env                 # Variáveis locais (Não comitado)
└── .gitignore           # Proteção contra commit de credenciais e volumes de dados
```

## 🔒 Segurança e Backups

Este repositório serve como a base de infraestrutura como código (IaC) do monitoramento. Os volumes (`grafana_data` e `prometheus_data`) contêm os dados persistentes (dashboards e métricas retidas) e não são versionados aqui. Eles fazem parte da rotina padrão de backup do `awlserver`. Em caso de restauração, basta preencher o `.env` e realizar o deploy padrão.

<p align="center"> Desenvolvido para <b>Astral Wave Label</b> 🌊 </p>