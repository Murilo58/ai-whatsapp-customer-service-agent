# Arquitetura da Solução

## Visão Geral

O Agente Inteligente de Atendimento via WhatsApp foi desenvolvido para automatizar o atendimento inicial de clientes utilizando WhatsApp, IA Generativa e automações construídas com n8n.

A solução é responsável por receber solicitações de clientes, identificar a intenção da mensagem, classificar a demanda, registrar informações, realizar agendamentos e enviar confirmações de forma automática.

---

## Arquitetura Geral

![Arquitetura da Solução](../images/cover.png)

---

## Componentes da Solução

### WhatsApp

Canal principal de comunicação com os clientes.

Responsável por:

* Receber mensagens dos usuários;
* Permitir interação em tempo real;
* Enviar respostas automáticas.

---

### Evolution API

Responsável pela integração entre WhatsApp e n8n.

Funções:

* Receber eventos do WhatsApp;
* Encaminhar mensagens para o webhook;
* Enviar respostas automatizadas;
* Gerenciar a sessão da instância.

---

### n8n

Motor principal de automação.

Funções:

* Receber mensagens;
* Extrair dados do cliente;
* Aplicar regras de negócio;
* Orquestrar integrações;
* Acionar a IA Generativa.

---

### IA Generativa

Responsável pela interpretação e classificação das solicitações.

Categorias suportadas:

* Comercial
* Financeiro
* Suporte

---

### Google Sheets

Base de registro dos atendimentos.

Informações armazenadas:

* Nome
* Telefone
* E-mail
* Categoria
* Assunto
* Atendente responsável

---

### Google Calendar

Responsável pelo agendamento de reuniões.

Permite:

* Criar compromissos;
* Registrar participantes;
* Gerar links de reunião;
* Organizar agendas.

---

### Gmail

Responsável pelo envio automático de confirmações.

Exemplos:

* Confirmação de reunião;
* Informações complementares;
* Comunicações automáticas.

---

## Fluxo de Atendimento

### 1. Recepção da Mensagem

O cliente envia uma mensagem pelo WhatsApp.

### 2. Processamento

A Evolution API recebe a mensagem e envia o evento para o n8n.

### 3. Extração de Dados

O fluxo identifica informações relevantes do cliente.

### 4. Classificação

A IA Generativa classifica automaticamente a solicitação.

### 5. Registro

Os dados são armazenados no Google Sheets.

### 6. Agendamento

Caso necessário, uma reunião é criada no Google Calendar.

### 7. Confirmação

Um e-mail é enviado automaticamente ao cliente.

### 8. Resposta

O cliente recebe retorno pelo WhatsApp.

---

## Tecnologias Utilizadas

* n8n
* Evolution API
* WhatsApp
* IA Generativa
* Google Sheets
* Google Calendar
* Gmail
* JavaScript
* PostgreSQL
* Redis
* Docker

---

## Segurança

Este repositório contém apenas informações demonstrativas.

Não são disponibilizados:

* Tokens;
* Credenciais;
* URLs privadas;
* Dados reais de clientes;
* Configurações sensíveis.

---

## Status do Projeto

✅ Projeto funcional e validado em ambiente self-hosted.

Ambiente utilizado:

* VPS Linux
* Docker
* Evolution API
* PostgreSQL
* Redis
* n8n
* Google Workspace
