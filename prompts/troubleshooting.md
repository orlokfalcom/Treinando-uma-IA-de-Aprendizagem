# ⚠️ Resolução de Problemas (Troubleshooting) em IA Financeira

Integrar modelos de linguagem (LLMs) em sistemas de produção bancários e transacionais exige cuidados especiais. Este guia mapeia falhas comuns de arquitetura de IA em finanças e como resolvê-las.

---

## 💥 1. Falta de Explicabilidade e Rastreabilidade (Auditoria e Legal)

*   **Sintoma:** Um agente de IA executou uma tarefa (como negar um reembolso ou aprovar um perfil de empréstimo), mas a equipe de auditoria ou compliance não consegue identificar o motivo da decisão.
*   **Risco:** Sanções regulatórias do Banco Central ou processos judiciais por recusa injustificada de serviços.
*   **Solução (Traceability Architecture):**
    *   **Auditoría de Pensamento:** Grave o fluxo de raciocínio (Chain-of-Thought) da IA em banco de dados estruturado e imutável (ex: PostgreSQL/Oracle com chaves de auditoria). Salve o prompt exato enviado, o contexto retornado do RAG e o JSON final de saída do modelo.
    *   **Strict Temperature:** Mantenha a `temperatura = 0.0` para que, diante do mesmo contexto e pergunta, a resposta seja determinística e passível de reprodução exata em testes de auditoria.

---

## 💥 2. Latência Excessiva em Operações de Pagamento Síncronas (Pix/Cartões)

*   **Sintoma:** O uso de LLMs em APIs síncronas de pagamento estoura o tempo limite (SLA de liquidação do Pix do Banco Central, que geralmente é de pouquíssimos segundos).
*   **Causa:** APIs de LLMs em nuvem pública sofrem de oscilação de rede e o tempo de geração de tokens (Time to First Token - TTFT) é inerentemente alto.
*   **Solução (Optimization & Asynchrony):**
    *   **Processamento Assíncrono:** Mantenha o LLM fora do caminho crítico da liquidação síncrona. Use a IA para gerar propostas de forma assíncrona (via Kafka/RabbitMQ) e envie o resultado para uma fila transacional de aprovação.
    *   **Modelos Especializados e Menores:** Se a operação exigir síncronidade (ex: assistente de chat que calcula extrato), use modelos menores (ex: LLaMA 3 8B ou Mistral 7B) hospedados na própria infraestrutura bancária otimizados com motores de inferência rápida (como **vLLM** ou **TensorRT-LLM**).
    *   **Cache Semântico:** Implemente cache de queries semânticas usando Redis. Se a intenção do cliente for a mesma já resolvida recentemente, retorne a resposta salva em menos de 10ms.

---

## 💥 3. Quebra de Schemas JSON em APIs do Open Finance

*   **Sintoma:** O LLM falha ao gerar saídas em formato JSON válido, enviando campos de tipos incorretos (ex: mandando uma string em um campo que devia ser int) ou incluindo textos em markdown (como ` ```json `), travando a integração com APIs do Open Finance.
*   **Causa:** Pequenas variações de comportamento e falta de tipagem estrita nos modelos de texto tradicionais.
*   **Solução (Strict Validation & Auto-healing):**
    *   **Validação Pydantic:** Use bibliotecas como `Instructor` ou `Outlines` que forçam o LLM a obedecer a um modelo Pydantic, rejeitando qualquer token fora do padrão de tipos.
    *   **Loop de Auto-correção (Auto-healing):** Implemente um validador de schema no backend. Se a resposta da IA quebrar o schema:
        1. Capture a mensagem de erro do parser JSON.
        2. Reenvie o JSON com erro e o stacktrace de erro de volta para a IA com a instrução: *"Você gerou um JSON inválido com este erro: [stacktrace]. Corrija-o imediatamente preservando os dados."*
        3. Realize no máximo uma tentativa de autocorreção antes de acionar um fallback seguro.

---

## 💥 4. Vazamento de Dados Sensíveis nos Logs da Nuvem (Data Leakage)

*   **Sintoma:** Dados de cartões (número PAN, CVV) ou dados pessoais de clientes (CPF, saldos) vazaram para logs de monitoramento da nuvem do LLM (AWS CloudWatch, Datadog ou console da OpenAI).
*   **Causa:** Falha na sanitização de dados no pipeline de dados que alimenta a IA.
*   **Solução (PII Shielding):**
    *   **DLP (Data Loss Prevention):** Crie uma regra ativa no gateway de rede impedindo o tráfego de dados que correspondam a padrões de números de cartões (validando pelo algoritmo de Luhn) ou CPF/CNPJ.
    *   **PII Masking Gateway:** Implemente e valide unitariamente a camada de anonimização (como visto em [arquitetura-com-ia.md](file:///E:/documentos/GitHub/Treinando-uma-IA-de-Aprendizagem/resumos/arquitetura-com-ia.md)) antes de qualquer requisição de prompt sair da rede segura do banco.
