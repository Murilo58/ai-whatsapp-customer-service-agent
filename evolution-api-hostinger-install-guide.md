# 🚀 Evolution API v2 + n8n + Hostinger VPS

Instalação completa da Evolution API v2 utilizando Docker, PostgreSQL e Redis em uma VPS Hostinger, integrada ao n8n para construção de agentes inteligentes de atendimento via WhatsApp.

![Hostinger](https://img.shields.io/badge/Hostinger-VPS-673DE6)

![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)

![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-E95420?logo=ubuntu&logoColor=white)

![n8n](https://img.shields.io/badge/n8n-AI%20Automation-FF6D5A)

![Evolution API](https://img.shields.io/badge/Evolution%20API-v2-green)

---

# 📋 Visão Geral

Este projeto documenta todo o processo de instalação, configuração e integração da Evolution API v2 em ambiente VPS Linux.

A arquitetura foi utilizada para construção de agentes inteligentes capazes de:

* Atender clientes via WhatsApp
* Classificar solicitações automaticamente
* Registrar clientes em Google Sheets
* Agendar reuniões no Google Calendar
* Enviar confirmações por e-mail
* Utilizar Inteligência Artificial (Gemini)
* Integrar com n8n

---

# 🏗️ Arquitetura da Solução

```text
WhatsApp
    │
    ▼
Evolution API
    │
    ▼
Webhook
    │
    ▼
n8n
    │
 ┌──┼─────────────┐
 │  │             │
 ▼  ▼             ▼
IA  Sheets      Calendar
 │
 ▼
Gmail
```

---

# 🛠️ Tecnologias Utilizadas

* Evolution API v2
* Docker
* Docker Compose
* PostgreSQL 15
* Redis 7
* Ubuntu 24.04
* n8n
* Google Gemini
* Google Sheets
* Google Calendar
* Gmail
* Hostinger VPS

---

# 📌 Pré-requisitos

Antes de iniciar, certifique-se de possuir:

* VPS Linux (Ubuntu 24.04 recomendado)
* Acesso Root
* Docker instalado
* Docker Compose instalado
* Porta 8080 liberada

---

# 🐳 Instalação do Docker

Atualizar sistema:

```bash
apt update && apt upgrade -y
```

Instalar Docker:

```bash
curl -fsSL https://get.docker.com | bash
```

Validar instalação:

```bash
docker --version
```

---

# 📁 Criando Estrutura do Projeto

```bash
mkdir -p /opt/evolution

cd /opt/evolution
```

---

# 📦 Docker Compose

Crie o arquivo:

```bash
nano docker-compose.yml
```

Conteúdo:

```yaml
services:

  evolution-postgres:
    image: postgres:15
    container_name: evolution-postgres
    restart: always
    environment:
      POSTGRES_DB: evolution
      POSTGRES_USER: evolution
      POSTGRES_PASSWORD: evolution123

  evolution-redis:
    image: redis:7-alpine
    container_name: evolution-redis
    restart: always

  evolution-api:
    image: atendai/evolution-api:v2.3.6
    container_name: evolution-api
    restart: always
    ports:
      - "8080:8080"
```

---

# 🚀 Subindo os Containers

```bash
docker compose up -d
```

Verificar status:

```bash
docker ps
```

Exemplo:

```text
CONTAINER ID   NAME                 STATUS
xxxxxxxxxxxx   evolution-api        Up
xxxxxxxxxxxx   evolution-postgres   Up
xxxxxxxxxxxx   evolution-redis      Up
```

---

# 📊 Verificando Logs

```bash
docker logs evolution-api -f
```

---

# 🔑 Obtendo a API Key

Em algumas instalações o arquivo `.env` não fica disponível diretamente.

Utilize:

```bash
docker exec evolution-api printenv
```

Ou:

```bash
docker exec evolution-api printenv | grep AUTHENTICATION_API_KEY
```

Exemplo:

```text
AUTHENTICATION_API_KEY=xxxxxxxxxxxxxxxx
```

---

# 🌐 Acessando o Painel

Acesse:

```text
http://IP_DA_VPS:8080
```

Exemplo:

```text
http://123.123.123.123:8080
```

---

# 📱 Criando uma Instância

1. Acessar o painel
2. Criar nova instância
3. Informar nome
4. Gerar QR Code
5. Conectar WhatsApp

---

# 🔗 Configurando Webhook

Exemplo:

```text
http://SEU_N8N/webhook/whatsapp
```

A Evolution enviará todos os eventos para esse endpoint.

---

# 🤖 Integração com n8n

Exemplo de arquitetura utilizada:

```text
Webhook
   ↓
Tratamento dos Dados
   ↓
Agente IA
   ↓
Classificação
   ↓
Google Sheets
   ↓
Google Calendar
   ↓
Gmail
```

---

# 📤 Exemplo de Envio de Mensagem

Endpoint:

```http
POST /message/sendText
```

Body:

```json
{
  "number": "5511999999999",
  "text": "Olá! Esta é uma mensagem enviada pela Evolution API."
}
```

---

# 🧠 Casos de Uso Implementados

## Atendimento Comercial

* Identificação automática
* Registro do cliente
* Direcionamento ao responsável

## Atendimento Financeiro

* Segunda via de boleto
* Cobranças
* Faturas

## Atendimento Suporte

* Problemas técnicos
* Erros
* Dúvidas operacionais

## Agendamento de Reuniões

* Integração Google Calendar
* Confirmação automática

---

# 📄 Registro em Google Sheets

Campos armazenados:

| Campo     | Descrição                        |
| --------- | -------------------------------- |
| Nome      | Nome do cliente                  |
| Telefone  | Número WhatsApp                  |
| Assunto   | Motivo do contato                |
| Atendente | Responsável                      |
| E-mail    | Cliente                          |
| Categoria | Comercial, Financeiro ou Suporte |

---

# 📧 Envio de E-mail

Fluxo implementado:

```text
Cliente
   ↓
Agendamento
   ↓
Google Calendar
   ↓
Gmail
   ↓
Confirmação Automática
```

---

# 🧠 Uso de Memória com Redis

A memória Redis foi utilizada para:

* Manter contexto das conversas
* Histórico por usuário
* Bufferização de mensagens
* Agrupamento de mensagens enviadas em sequência

Exemplo:

```text
Mensagem 1
Mensagem 2
Mensagem 3

↓

Resposta única da IA
```

---

# 🔧 Troubleshooting

## Erro: device_removed

### Sintoma

WhatsApp desconectado.

### Solução

Reconectar utilizando QR Code.

---

## Erro: count:0

### Sintoma

Webhook não recebe mensagens.

### Solução

Verificar:

* Webhook
* Instância conectada
* Logs da Evolution
* Firewall

---

## Erro: Could not connect with these settings

### Sintoma

n8n não conecta na Evolution.

### Solução

Validar:

* URL da Evolution
* Porta 8080
* API Key
* Firewall da VPS

---

## Erro: Authentication Failed

### Sintoma

Requisições retornam erro 401.

### Solução

Verificar:

```bash
docker exec evolution-api printenv | grep AUTHENTICATION_API_KEY
```

---

# 📈 Resultado Final

Ao término da instalação temos:

✅ Evolution API operacional

✅ PostgreSQL persistente

✅ Redis configurado

✅ WhatsApp conectado

✅ Webhooks funcionando

✅ Integração com n8n

✅ Integração com Google Sheets

✅ Integração com Google Calendar

✅ Integração com Gmail

✅ Agentes de IA operacionais

---

# 📚 Melhorias Futuras

* HTTPS com Nginx
* Domínio próprio
* Multiatendimento
* Dashboard analítico
* CRM integrado
* OpenAI GPT
* RAG com Base de Conhecimento
* Integração com ERP

---

# 👨‍💻 Autor

**Murilo Guimarães Costa**

PMP® | Mentor PMI | Especialista em Projetos | Automação com IA

LinkedIn:
https://www.linkedin.com/in/murilogcosta/

GitHub:
https://github.com/Murilo58

---

⭐ Se este projeto foi útil, considere deixar uma estrela no repositório.
