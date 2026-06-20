# ⚠️ Guia de Resolução de Problemas (Troubleshooting) com LLMs

Trabalhar com modelos de linguagem generativos introduz desafios únicos devido à sua natureza probabilística e não-determinística. Este guia detalha problemas comuns em integrações com LLMs e como solucioná-los.

---

## 💥 1. Respostas Genéricas, Vagas ou Irrelevantes

*   **Sintoma:** O modelo gera respostas muito superficiais, ignorando restrições específicas do seu problema.
*   **Causa:** Falta de contexto ou papel (persona) mal definido.
*   **Solução:**
    *   **Definição de Papel (Roleplay):** Sempre inicie o prompt dizendo quem a IA deve ser (ex: *"Você é um revisor de segurança de código Python"*).
    *   **Grounding (Aterramento):** Forneça documentos, códigos ou dados específicos no prompt e instrua o modelo a responder *exclusivamente* com base neles.
    *   **Uso de Delimitadores:** Use tags XML (ex: `<codigo> ... </codigo>`) para isolar os dados e evitar confusões com as instruções.

---

## 💥 2. Alucinação (Geração de Fatos ou APIs Falsas)

*   **Sintoma:** O modelo inventa uma biblioteca de código que não existe, inventa um parâmetro fictício ou afirma fatos incorretos com convicção.
*   **Causa:** O modelo preenche lacunas de conhecimento gerando a combinação de palavras mais provável sintaticamente, sem validação lógica.
*   **Solução:**
    *   **Reduza a Temperatura:** Configure a temperatura para `0.0` ou próximo disso para diminuir a criatividade e incentivar respostas factuais e reproduzíveis.
    *   **Opção de Escape:** Adicione uma instrução explícita como: *"Se você não tiver certeza ou se a informação não estiver presente no contexto fornecido, diga 'Não sei'. Não invente fatos."*
    *   **Grounding via RAG:** Nunca dependa puramente do conhecimento de treinamento da IA para dados dinâmicos ou específicos da empresa; recupere os dados de um banco vetorial primeiro.

---

## 💥 3. Respostas JSON Inválidas (Estrutura Quebrada em APIs)

*   **Sintoma:** O backend tenta fazer o parser de uma resposta do LLM e ocorre falha porque o modelo esqueceu de fechar uma chave `}`, usou aspas incorretas, ou encapsulou a resposta em blocos de código Markdown (como ```json ... ```).
*   **Causa:** Os LLMs são geradores de texto livre por padrão e nem sempre seguem a sintaxe JSON perfeitamente.
*   **Solução:**
    *   **JSON Mode:** Habilite o parâmetro de "JSON Mode" ou "Structured Outputs" na API oficial da IA (OpenAI, Gemini e Claude suportam essa opção nativamente).
    *   **Few-shot Examples:** Forneça no prompt um exemplo exato do formato JSON que você espera receber.
    *   **Bibliotecas de Enforcamento de Schema:** Utilize bibliotecas que geram prompts e validam retornos automaticamente usando Pydantic ou esquemas de gramática (como `Instructor` em Python ou `Outlines`).

---

## 💥 4. Loops de Repetição de Texto

*   **Sintoma:** O modelo fica "preso" e começa a repetir a mesma frase ou parágrafo indefinidamente na resposta.
*   **Causa:** A probabilidade dos tokens que formam aquela frase repetida tornou-se excessivamente alta devido ao histórico imediato.
*   **Solução:**
    *   **Ajuste Penalidades:** Aumente o parâmetro `presence_penalty` ou `frequency_penalty` para valores entre `0.1` e `0.5`. Isso penaliza o modelo por escolher palavras repetidas.
    *   **Temperatura:** Aumente ligeiramente a temperatura para quebrar o determinismo do loop.

---

## 💥 5. Limites de Janela de Contexto Estourados

*   **Sintoma:** A API retorna um erro de código HTTP 400 informando que o limite de tokens da janela de contexto foi ultrapassado.
*   **Causa:** A conversa está muito longa ou o contexto inserido (arquivos/documentos) é grande demais.
*   **Solução:**
    *   **Estratégias de Resumo (Summarization):** À medida que a conversa avança, peça para o modelo resumir as mensagens anteriores e passe apenas o resumo no histórico.
    *   **Janela Deslizante (Sliding Window):** Mantenha apenas as últimas $N$ interações do chat na memória da API.
    *   **Relação de busca (Retrieval):** Em vez de enviar o arquivo de código inteiro, quebre-o em funções relevantes e faça buscas vetoriais para enviar apenas o trecho que está sendo editado ou discutido.
