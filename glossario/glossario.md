# 📖 Glossário de IA Generativa em Sistemas Bancários e Financeiros

Este glossário reúne e explica detalhadamente os termos técnicos essenciais no desenvolvimento de sistemas financeiros integrados com IA Generativa, com foco em segurança, conformidade regulatória e engenharia de software.

---

### 🔒 Segurança, Conformidade e Sigilo Bancário

#### 1. Mascaramento de PII (Personally Identifiable Information)
Processo automatizado de anonimização ou substituição de dados sensíveis de clientes (como CPF, nome completo, número de conta corrente, dados de cartão de crédito e saldos) por valores fictícios ou tokens genéricos antes do envio para modelos de linguagem hospedados fora da rede do banco. Essencial para conformidade com a LGPD e o Sigilo Bancário.

#### 2. IA Explicável (XAI - Explainable AI)
Conjunto de processos e métodos que permite a auditores humanos compreender e confiar nos resultados gerados por modelos de IA. No setor bancário, é crucial para explicar por que uma IA recusou um limite de crédito ou por que sinalizou uma transação como potencial fraude, garantindo o direito à explicação previsto em leis financeiras.

#### 3. RAG com RBAC (Role-Based Access Control)
Arquitetura de busca semântica onde a recuperação de documentos e respostas do LLM respeita rigorosamente as permissões de acesso do usuário logado (ex: um atendente de agência não pode recuperar relatórios de auditoria interna restritos à diretoria por meio do chatbot do banco).

#### 4. PCI-DSS em Pipelines de IA
Adaptação das normas internacionais de segurança da indústria de cartões de pagamento (PCI-DSS) para garantir que números de cartões (PAN) e códigos de segurança não sejam armazenados em logs de chamadas de LLM, caches de prompts ou bancos de dados vetoriais de suporte ao cliente.

#### 5. Human-in-the-Loop (HITL) Financeiro
Mecanismo de controle que insere uma etapa obrigatória de aprovação por um operador humano (ou pelo próprio cliente do banco) antes que uma ação financeira sugerida por um agente de IA (como realizar uma transferência Pix ou contratar um empréstimo) seja de fato liquidada no core banking.

---

### 🧠 Conceitos Fundamentais e Arquitetura

#### 6. LLM (Large Language Model) Bancário
Modelos de linguagem ajustados finamente (Fine-tuning) com jargões financeiros locais, circulares do Banco Central e regulamentos de conformidade interna, sendo capazes de entender termos complexos como taxas de spread, portabilidade de crédito e tributação de fundos.

#### 7. Transformer
A arquitetura neural baseada no mecanismo de *Self-Attention* (Atenção Própria). No contexto bancário, sua capacidade de processar grandes sequências de texto paralelamente permite analisar rapidamente contratos longos de financiamento ou circulares regulatórias complexas de centenas de páginas.

#### 8. Token
A unidade fundamental de processamento do modelo. Em sistemas bancários, a tokenização correta de termos numéricos, taxas de juros (ex: "10,75% a.a.") e strings de JSON é crítica para que a IA não altere ou interprete incorretamente dados numéricos críticos.

#### 9. Janela de Contexto (Context Window)
O limite de memória operacional da IA em uma chamada. Útil para carregar regulamentos completos do Banco Central (BACEN) ou o histórico recente de faturas do cliente para que a IA possa responder a perguntas complexas contextualizadas.

---

### ⚙️ Integração e Termos Técnicos

#### 10. Grounding Transacional
Técnica de ancoragem que consiste em injetar dados reais, estruturados e auditados de transações financeiras (como extrato de conta em tempo real do banco de dados relacional SQL) diretamente no prompt da IA, impedindo que ela alucine valores ou transações inexistentes.

#### 11. Banco de Dados Vetorial (Vector DB)
Banco especializado em buscar trechos de regulamentos, manuais internos e termos de serviço usando semântica. No banco, os dados são armazenados na forma de **Embeddings** (vetores de alta dimensão).

#### 12. RAG (Retrieval-Augmented Generation)
Arquitetura usada para responder a perguntas de clientes ou analistas baseando-se exclusivamente nos manuais de crédito ou circulares regulatórias vigentes do banco, minimizando drasticamente o risco de alucinações.

#### 13. Agente de IA Financeiro
Sistemas de software que utilizam LLMs para tomar decisões complexas de forma autônoma (ex: analisar uma contestação de compra, verificar se o cliente cumpre regras de estorno e acionar a API de reembolso automaticamente).

#### 14. Chamada de Função (Function Calling / Tool Use)
Capacidade do LLM de traduzir a intenção do cliente em comandos estruturados para as APIs bancárias (ex: o cliente digita "quero bloquear meu cartão final 4321" e o modelo responde gerando um JSON que invoca o endpoint `/api/v1/card/block` com os argumentos corretos).

#### 15. Caching Semântico Bancário
Armazenamento local de respostas a perguntas comuns de clientes para reduzir custos e latência (ex: dúvidas frequentes sobre taxas do Pix), garantindo que as respostas sejam respondidas instantaneamente de forma segura.
