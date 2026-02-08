# 📊 AWL Monitoring - Prometheus & Grafana System

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=docker,prometheus,grafana,linux,github" />
  </a>
</p>

Este repositório contém o setup de monitoramento da infraestrutura **Astral Wave Label**, focado inicialmente na coleta de métricas da **LoginHub API**. O objetivo é garantir backup configurável e alta disponibilidade dos painéis de métricas.

## 🚀 Tecnologias Utilizadas

* **Prometheus**: Coleta e armazenamento de métricas de séries temporais.
* **Grafana**: Visualização de dados e dashboards interativos.
* **Docker & Docker Compose**: Orquestração e isolamento do ambiente.

## 🛠️ Como Instalar e Rodar

### 1. Pré-requisitos

Certifique-se de ter o Docker e o Docker Compose instalados.

### 2. Configuração da Rede

Crie a rede externa necessária para a comunicação entre os containers:

```bash
docker network create awl_network
```

### 3. Configuração de Ambiente

Crie um arquivo `.env` baseado no exemplo abaixo:

```ini
# .env
GRAFANA_USER=admin
GRAFANA_PASSWORD=sua_senha_secreta
PROMETHEUS_VER=v2.50.1
GRAFANA_VER=10.3.3
GF_SERVER_DOMAIN=grafana.astralwavelabel.com
```

### 4. Executando o Projeto

Suba os containers em modo *detached*:

```bash
docker compose up -d
```

## 📁 Estrutura do Projeto

```
.
├── docker-compose.yml   # Orquestração dos containers (vias variáveis .env)
├── prometheus.yml       # Configurações de jobs e targets do Prometheus
├── .env.example         # Exemplo de variáveis de ambiente
└── .gitignore           # Proteção para não subir dados sensíveis
```

## 🔒 Segurança (Backup)

Este repositório foi configurado para ser um backup seguro. Os arquivos de dados (volumes) e as senhas reais estão ignorados pelo `.gitignore`. Em caso de restauração, preencha o arquivo `.env` com as credenciais originais.

<p align="center"> Desenvolvido para <b>Astral Wave Label</b> 🌊 </p>