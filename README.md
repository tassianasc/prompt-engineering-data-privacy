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
```

### 🧪 Validação e Anonimização de PII
Durante o processo de higienização, foram aplicadas as seguintes técnicas:

Tokenização de Clientes: Alice Johnson ➔ Cliente001

Redação / Mascaramento: alice.johnson@example.com ➔ [EMAIL_REMOVIDO]

Generalização de Rede: 192.168.1.10 ➔ 192.168.xxx.xxx

Higienização de Texto Livre: Filtro por Regex no comentário para prevenir dados ocultos.

### Resultado da Auditoria Interna (Célula 8)
Métrica Auditada	Quantidade Restante	Status de Segurança
Nomes originais restantes	0	✅ Aprovado
E-mails originais restantes	0	✅ Aprovado
IPs completos restantes	0	✅ Aprovado
E-mails no texto livre	0	✅ Aprovado
IPs no texto livre	0	✅ Aprovado
### 📊 Resumo Agregado dos Dados
Estatísticas geradas via Python no Colab utilizadas na contextualização do prompt:

Volume Total de Registros: 15

Avaliação Média: 4.0 / 5.0 (Mínima: 2.0 | Máxima: 5.0)

Distribuição por Categoria:

Alta (Notas 4 e 5): 10 clientes

Média (Nota 3): 4 clientes

Baixa (Nota 2): 1 cliente

Média por Tema Identificado:

Produto: 5.00

Valor e processo: 4.50

Atendimento: 4.20

Geral: 3.75

Prazo e resposta: 3.33 (Gargalo operacional identificado)

Palavras mais Frequentes (Nuvem de termos): experience, satisfied, service, time, excellent, support, helpful, staff.

### 🤖 Engenharia de Prompt Segura
O prompt foi construído com atribuição de persona, tarefas bem delimitadas, formato tabular de saída e instrução explícita para evitar alucinações.

```plaintext
Atue como analista de experiência do cliente.

Tarefa:
1. Identifique três tendências sustentadas pelos dados.
2. Explique a importância de cada tendência.
3. Sugira três melhorias práticas para o negócio.

Restrições:
- Use somente o resumo agregado fornecido.
- Não invente causas, percentuais ou informações ausentes.
- Diferencie evidência de hipótese.
- Informe limitações decorrentes do pequeno volume de dados.

Formato:
Apresente uma tabela com as colunas: Evidência | Interpretação | Recomendação | Limitação.

Resumo agregado:
[Dados estatísticos anonimizados]
```

### 📋 Resultado Obtido da IA
Abaixo está a resposta gerada pelo modelo de linguagem com base unicamente no contexto seguro fornecido:

Evidência	Interpretação	Recomendação	Limitação
Média por tema "Prazo e resposta" é a menor (3.33)	Clientes estão insatisfeitos com a velocidade do suporte e tempo de entrega.	Implementar SLAs mais rígidos e respostas automáticas iniciais no suporte.	Amostra reduzida (apenas 3 registros no tema 'Prazo e resposta').
Distribuição concentra 66,6% das notas na categoria Alta	A percepção geral de valor e qualidade do produto/atendimento é bastante positiva.	Manter os padrões do produto e treinar equipe focando em retenção e upsell.	Viés de amostragem pelo pequeno volume total (15 registros).
Palavras frequentes focam em "support", "staff" e "helpful"	O atendimento humano é o ponto forte da experiência do cliente.	Criar um programa de reconhecimento para a equipe de linha de frente.	Palavras isoladas não indicam o tom exato sem análise de sentimento completa.

### 🧠 Revisão Crítica e Reflexão LGPD
Checklist de Validação do Prompt (Item 15)
Fidelidade aos dados: A IA utilizou estritamente os números fornecidos, sem inventar percentuais operacionais.

Reconhecimento de Limitações: O modelo explicitou em todas as recomendações que o volume de dados (N=15) exige cautela antes de grandes investimentos.

Ausência de Alucinações: Não houve invenção de causas externas que não estivessem respaldadas nos agregados.

Reflexão sobre Privacidade e Governança
Eficácia da Anonimização: A combinação de Regex com mascaramento estruturado eliminou o risco de exposição de PIIs diretas e indiretas.

Limitações da Análise: A anonimização em bases pequenas pode reduzir a capacidade da IA de capturar contextos específicos de nicho, exigindo um equilíbrio entre privacidade e utilidade analítica.

Cuidados com IA: Dados Pessoais Sensíveis jamais devem ser transmitidos em sua forma bruta para modelos LLMs terceirizados. A agregação estatística prévia é a estratégia mais recomendada para manter conformidade total com a LGPD e o GDPR.

### 🚀 Como Executar o Projeto
Clone o repositório:

```bash
git clone [https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git](https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git)
```
Abra o arquivo notebook.ipynb no Google Colab ou Jupyter Notebook.

Execute todas as células sequencialmente.

O arquivo anonymised_customer_feedback.csv será gerado automaticamente.

### 💻 Tecnologias Utilizadas
As principais tecnologias e bibliotecas utilizadas neste projeto são:

Linguagem principal: Python (3.10+)

Manipulação e análise de dados: Pandas

Processamento de texto e expressões regulares: re (Regex)

Contagem e agregação de dados: collections (Counter)

Gerenciamento de arquivos e caminhos: pathlib (Path)

Ambiente de execução: Google Colab (com suporte ao pacote google.colab)
