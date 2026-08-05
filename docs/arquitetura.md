# Arquitetura da Solução

## Objetivo

Construir um agente de Inteligência Artificial utilizando arquitetura RAG (Retrieval-Augmented Generation), capaz de responder perguntas com base em documentos PDF enviados pelo usuário.

## Arquitetura Geral

```text
                   GitHub
                      │
                      │
              Docker Compose
                      │
        ┌─────────────┴─────────────┐
        │                           │
      n8n                   PostgreSQL + pgvector
        │                           │
        └─────────────┬─────────────┘
                      │
                 Agente RAG
                      │
          OpenAI / Gemini / OCI GenAI
                      │
                 Embeddings
                      │
                 PDFs enviados
                      │
                Telegram Bot
                      │
                   Usuário
```

## Componentes

### n8n

Responsável pela orquestração dos fluxos de automação e execução do agente de IA.

### Banco Vetorial

Armazenará os embeddings dos documentos para permitir busca semântica.

### LLM

Modelo responsável por gerar a resposta utilizando o contexto recuperado do banco vetorial.

### Telegram

Interface utilizada pelo usuário para conversar com o agente.

### Docker

Responsável por executar toda a solução em containers.

### Oracle Cloud Infrastructure (OCI)

Ambiente onde a solução será publicada ao final do projeto.

## Roadmap

- [x] Estrutura do projeto
- [x] Docker
- [x] n8n Self Hosted
- [ ] GitHub
- [ ] Telegram
- [ ] Banco Vetorial
- [ ] Embeddings
- [ ] Agente RAG
- [ ] Deploy OCI