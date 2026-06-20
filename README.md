# 🚀 📘 Caderno Temático Inteligente: IA Generativa em Sistemas Bancários

### 💡 Estudo avançado de Inteligência Artificial Generativa aplicada ao Desenvolvimento de Software e Arquitetura Transacional Financeira

---

## 🧭 Visão Geral

Este repositório documenta uma jornada estruturada de aprendizado e aplicação prática de **IA Generativa** no desenvolvimento e na arquitetura de **Sistemas Bancários e Meios de Pagamento**. A curadoria aborda os desafios específicos do setor de missão crítica: conformidade regulatória (BACEN, LGPD), sigilo bancário, mitigação de latência transacional, engenharia de prompts avançada e migração de sistemas legados de core banking.

---

## 🎯 Objetivos do Projeto

*   **⚡ Construir Entendimento Sólido:** Dominar o ciclo de vida de LLMs (Pré-treino, SFT, RLHF/DPO) voltado ao contexto financeiro.
*   **🔒 Arquitetar Soluções Seguras:** Projetar integrações de IA que respeitem o sigilo bancário através de Gateways de Privacidade (PII Redaction) e RAG com RBAC.
*   **🛠️ Automatizar e Otimizar Engenharia:** Aplicar IA na migração de código legado (COBOL para Java/Go) e na geração de suítes de testes transacionais (Pix/Contas).
*   **📈 Engenharia de Prompts de Alta Precisão:** Desenvolver prompts determinísticos e estruturados (JSON Mode, Pydantic) para APIs do Open Finance.
*   **🛡️ Mitigação de Riscos Sistêmicos:** Implementar controle transacional rígido com aprovação humana (Human-in-the-Loop - HITL) e auditoria de decisões agênticas (XAI).

---

## 🧩 Stack de Conhecimento Bancário

*   **🧠 IA Generativa & LLMs:** Modelos comerciais e de nuvem privada (Azure OpenAI, AWS Bedrock, vLLM local).
*   **🔄 Transformers:** Mecanismo de Self-Attention aplicado à análise semântica de regulamentos e contratos.
*   **🔒 Segurança e Conformidade:** LGPD, Resoluções do Banco Central (BACEN), PCI-DSS e IA Explicável (XAI).
*   **🏗️ Padrões de Integração:** RAG (Retrieval-Augmented Generation) com filtros de RBAC e Gateways de PII.
*   **⚙️ Core Banking Software:** Migração de Mainframes, APIs do Open Finance e concorrência transacional (antigasto duplo).

---

## 📁 Estrutura do Projeto

```text
caderno-ia-generativa
│
├── 📚 fontes/          → Papers científicos (cópia local), documentação oficial e links úteis
│   ├── attention_is_all_you_need.pdf  → Paper clássico da arquitetura Transformer
│   └── links.md                       → Curadoria de fontes de referência e documentações
│
├── 💬 prompts/        → Templates estruturados e guia de resolução de falhas em produção
│   ├── prompts-basicos.md     → Categorização de faturas e triagem de atendimento (Few-shot)
│   ├── prompts-avancados.md   → Geração de código Spring Boot transacional e auditoria BACEN
│   └── troubleshooting.md     → Mitigação de alucinações, latência Pix e quebras de JSON
│
├── 🧠 resumos/        → Artigos detalhados e conceitos arquiteturais e teóricos
│   ├── resumo-ia-generativa.md  → Funcionamento de LLMs vs IA Preditiva antifraude clássica
│   ├── llms-explicacao.md       → Pipeline de treino financeiro e deploy em redes privadas
│   ├── aplicacoes-software.md   → Casos práticos: COBOL -> Java, testes unitários e segurança
│   └── arquitetura-com-ia.md    → RAG seguro, PII Redaction e fluxo agêntico com HITL
│
└── 📖 glossario/      → Terminologias cruciais detalhadas
    └── glossario.md   → Termos de IA aplicados a finanças (RBAC, HITL, PII, XAI, Embeddings)
```

---

## 📚 Curadoria de Fontes Fundamentais

### 📄 Base Científica e Técnica
*   **Attention Is All You Need:** A base da arquitetura Transformer. [Paper Local](./fontes/attention_is_all_you_need.pdf).
*   **ReAct Paper (Reasoning & Acting):** Padrão de raciocínio lógico em agentes financeiros. [Link Oficial](https://arxiv.org/abs/2210.03629).

### 🛠️ Documentações de Plataformas
*   **OpenAI Cookbook & Docs:** Guias de estruturação de parâmetros de geração determinísticos (`Temp = 0.0`). [Acessar Docs](https://platform.openai.com/docs).
*   **Anthropic Claude Docs:** Padrões de prompts para análise de longos contratos de financiamento. [Acessar Docs](https://docs.anthropic.com).
*   **Hugging Face:** Utilização e deploy de modelos Open Source locais para nuvens privadas de bancos. [Acessar Hub](https://huggingface.co).

---

## 💬 Engenharia de Prompts Financeiros

*   **🟢 Prompts Básicos ([prompts-basicos.md](./prompts/prompts-basicos.md)):**
    *   *Categorização de Faturas:* Limpeza e categorização semântica de descrições sujas de compras de cartão de crédito.
    *   *Triagem de Suporte (Few-shot):* Classificação de intenções de atendimento (extratos, contestação de Pix, bloqueio de cartão).
*   **🔴 Prompts Avançados ([prompts-avancados.md](./prompts/prompts-avancados.md)):**
    *   *Desenvolvedor Sênior Spring Boot:* Geração de código de transferência seguro com `@Transactional`, controle de concorrência contra gasto duplo e mascaramento de logs.
    *   *Auditor de Conformidade BACEN:* Validação de termos de abertura de conta contra as regulamentações oficiais vigentes do Banco Central.
    *   *Arquiteto de Software Pix:* Prompt ativo para desenho de pipelines assíncronos e tolerantes a falhas.

---

## ⚠️ Cicatrizes de Aprendizado (Troubleshooting em Produção)

*   **💥 Alucinações de Dados Financeiros:** Mitigado zerando a temperatura (`Temp = 0.0`) e aplicando RAG para embasar as respostas da IA exclusivamente em manuais vigentes do banco.
*   **💥 Vazamento de PII nos Logs da Nuvem:** Resolvido implementando um **PII Redaction Gateway** local que anonimiza os dados do cliente antes do envio para APIs públicas e os reidrata no retorno do backend.
*   **💥 Estouro do SLA de Latência no Pix:** Resolvido movendo o processamento pesado de IA para filas de processamento assíncrono (Kafka/RabbitMQ) e utilizando cache semântico (Redis) para diminuir o tempo de resposta síncrona.
*   **💥 Quebra de Schemas JSON em APIs:** Mitigado enforcando a geração de JSON estruturado com esquemas rígidos de validação (Pydantic/Instructor) e loop de autocorreção (auto-healing).

---

## 📘 Miniguia de Estudo Financeiro

### 🧩 Termos Essenciais
1.  **PII Masking:** Anonimização de dados pessoais e transacionais de clientes.
2.  **Explainable AI (XAI):** Rastreabilidade e explicabilidade das decisões autônomas do modelo para auditoria.
3.  **Human-in-the-Loop (HITL):** Etapa de aprovação por senha ou biometria em fluxos financeiros gerados por IA.
4.  **RBAC em Bancos Vetoriais:** Filtragem de buscas semânticas para respeitar as permissões de acesso do cargo do colaborador.

### 📌 Aplicações Reais no SDLC Bancário
*   **Geração de Massa de Testes:** Cobertura de edge cases em cálculos de amortização de parcelas, juros e finais de semana.
*   **Migração COBOL para Java/Go:** Redução drástica do custo operacional herdado de mainframes corporativos tradicionais.
*   **Varredura PCI-DSS:** Impedir código gerado por IA de armazenar dados brutos de cartão de crédito.

---

## 📈 Evolução Contínua

Este caderno de estudos é um sistema vivo 🧬 que evolui com:
*   Novas regras de segurança contra Prompt Injection em sistemas financeiros.
*   Padrões de design de APIs atualizados com as diretrizes do Open Finance Brasil.
*   Novas resoluções regulatórias do BACEN e práticas de auditoria automática.
*   Testes de desempenho de inferência local (vLLM) de modelos financeiros.

---

## 🪪 Licença e Uso

Material didático aberto e de referência para engenheiros de software, arquitetos de sistemas e profissionais de segurança que integram IA Generativa em plataformas de missão crítica do setor financeiro.