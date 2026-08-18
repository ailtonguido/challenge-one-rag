# Challenge ONE RAG

Projeto desenvolvido como parte da formação Oracle Next Education (ONE).

## Objetivo

Construir um agente de Inteligência Artificial utilizando arquitetura RAG (Retrieval-Augmented Generation), capaz de responder perguntas com base em documentos PDF fornecidos pelo usuário.

## Arquitetura RAG

Os PDFs são fragmentados em chunks, transformados em embeddings, armazenados no pgvector e recuperados semanticamente pelo agente antes da resposta do Gemini.

## Tecnologias

- n8n (Self-Hosted)
- Docker
- Telegram Bot
- Banco Vetorial
- Embeddings
- Amazon Web Services (AWS) — EC2 + PostgreSQL + pgvector, Google Gemini e Cloudflare Tunnel.
- Git & GitHub

## Roadmap

- [x] Ambiente Docker
- [x] Chatbot Telegram
- [x] Ingestão de PDFs
- [x] Banco Vetorial
- [x] Implementação RAG
- [x] Deploy AWS
- [x] Documentação Final

## 🌐 Deploy e acesso público

A aplicação foi implantada em uma instância **Amazon EC2 (AWS)** utilizando **Docker Compose**, responsável pela execução dos containers do **n8n** e **PostgreSQL com pgvector**.

Para permitir que o **Telegram** acesse o webhook do n8n através de uma URL HTTPS pública, foi utilizado o **Cloudflare Tunnel**.

Nesta versão do projeto, está sendo utilizado um **Cloudflare Quick Tunnel**, que gera uma URL HTTPS temporária no domínio `trycloudflare.com` e encaminha as requisições para o n8n executado na porta `5678` da instância EC2.

Fluxo de acesso:

Telegram
    ↓
Cloudflare Quick Tunnel (HTTPS)
    ↓
AWS EC2
    ↓
Docker Compose
    ├── n8n
    └── PostgreSQL + pgvector
            ↓
        Google Gemini

### ⚠️ Observação sobre o Cloudflare Tunnel

O endereço fornecido pelo **Cloudflare Quick Tunnel é temporário** e pode ser alterado quando o túnel é reiniciado.

Por esse motivo, a URL gerada pelo túnel **não é armazenada neste repositório**. Sempre que um novo túnel é criado, a variável `WEBHOOK_URL` deve ser atualizada localmente no arquivo `.env` da instância EC2.

Exemplo:

WEBHOOK_URL=https://.trycloudflare.com

Após a alteração, o container do n8n deve ser recriado para carregar a nova configuração:

docker compose up -d --force-recreate n8n

Para um ambiente de produção, a evolução recomendada é utilizar um **Cloudflare Tunnel permanente associado a um domínio próprio**, evitando a necessidade de atualização manual da URL do webhook.

## 🔐 Segurança

Dados sensíveis não são versionados no repositório.

O arquivo `.env` é ignorado pelo Git e concentra configurações específicas do ambiente, enquanto credenciais como:

- Token do Telegram Bot
- API Key do Google Gemini
- Credenciais do PostgreSQL

são configuradas diretamente no ambiente de execução e/ou no gerenciador de credenciais do n8n.
