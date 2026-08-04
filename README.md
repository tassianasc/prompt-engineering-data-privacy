# 🔒 Desafio de IA: Engenharia de Prompt e Privacidade de Dados (LGPD)

> **Projeto de Governança de IA & Data Privacy:** Pipeline em Python para identificação, anonimização e tratamento de Dados Pessoais Sensíveis (PII) antes da integração com Grandes Modelos de Linguagem (LLMs).

---

## 📌 Sumário
- [Visão Geral](#-visão-geral)
- [Arquitetura do Pipeline de Privacidade](#-arquitetura-do-pipeline-de-privacidade)
- [Validação e Anonimização de PII](#-validação-e-anonimização-de-pii)
- [Resumo Agregado dos Dados](#-resumo-agregado-dos-dados)
- [Engenharia de Prompt Segura](#-engenharia-de-prompt-segura)
- [Resultado Obtido da IA](#-resultado-obtido-da-ia)
- [Revisão Crítica e Reflexão LGPD](#-revisão-crítica-e-reflexão-lgpd)
- [Como Executar o Projeto](#-como-executar-o-projeto)

---

## 🎯 Visão Geral

O objetivo principal deste projeto é demonstrar como analisar *feedbacks* de clientes utilizando Inteligência Artificial **sem violar diretrizes de privacidade (LGPD/GDPR)**. 

### 🚫 O Risco
Enviar planilhas brutas contendo nomes, e-mails, endereços IP e textos livres para IAs públicas expõe PII (*Personally Identifiable Information*).

### ✅ A Solução
Utilizar **Python** localmente para higienizar, tokenizar, generalizar e agregar os dados. Apenas o **resumo estatístico e anônimo** é enviado como contexto para o modelo de IA.

---

## 🛠️ Arquitetura do Pipeline de Privacidade

```text
[ Base Bruta (CSV) ] 
       │
       ▼
[ 1. Detecção via Regex ] ────► Identificação de PIIs e Padrões (Email, IP, Tel)
       │
       ▼
[ 2. Higienização & Redação ] ──► Substituição por Tokens ([EMAIL_REMOVIDO], Cliente001)
       │
       ▼
[ 3. Validação de Segurança ] ──► Auditoria automatizada (Garantia de 0 PIIs restantes)
       │
       ▼
[ 4. Agregação Estatística ] ───► Agrupamento por Notas, Categorias e Frequência
       │
       ▼
[ 5. Prompting Seguro para IA ] ──► Envio exclusivo de resumos agregados
