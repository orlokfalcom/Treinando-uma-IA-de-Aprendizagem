# 📖 Glossário de IA Generativa e Engenharia de Prompts

Este glossário reúne e explica detalhadamente os principais termos técnicos utilizados no universo da Inteligência Artificial Generativa e no desenvolvimento de sistemas auxiliados por LLMs.

---

### 🧠 Conceitos Fundamentais e Arquitetura

#### 1. Inteligência Artificial Generativa (GenAI)
Ramo da inteligência artificial focado no desenvolvimento de modelos capazes de gerar novos conteúdos (como texto, imagens, áudio, vídeo ou código) com base em padrões aprendidos a partir de dados de treinamento.

#### 2. LLM (Large Language Model)
Modelos de linguagem de grande escala baseados em aprendizado profundo (Deep Learning). São treinados em volumes massivos de dados textuais para prever a próxima palavra (ou token) em um contexto, sendo capazes de compreender e gerar linguagem natural de forma altamente fluida.

#### 3. Transformer
Arquitetura de rede neural introduzida no paper *"Attention Is All You Need"* (2017) que revolucionou o processamento de linguagem natural. Utiliza conexões paralelas para processar dados de texto sequenciais, permitindo capturar o contexto de longo alcance em frases e parágrafos de forma muito mais eficiente que as arquiteturas anteriores (como RNNs e LSTMs).

#### 4. Mecanismo de Atenção (Self-Attention)
Componente central dos Transformers que permite ao modelo calcular a importância de diferentes palavras (tokens) em uma frase em relação a uma palavra específica, independentemente da distância entre elas. Isso ajuda a IA a entender o contexto completo de uma sentença.

#### 5. Token
A unidade básica de processamento dos modelos de linguagem. Um token não equivale necessariamente a uma palavra inteira; pode ser uma palavra, um caractere, parte de uma palavra (sufixo/prefixo) ou até espaços. Em média, 100 tokens correspondem a cerca de 75 palavras em inglês.

#### 6. Janela de Contexto (Context Window)
A quantidade máxima de dados (medida em tokens) que um modelo pode processar de uma única vez em uma única requisição (incluindo o prompt do usuário e a resposta gerada). Se a conversa exceder esse limite, as informações mais antigas começam a ser "esquecidas" pela IA.

---

### 💬 Engenharia de Prompts e Interação

#### 7. Prompt
A instrução, pergunta ou texto de entrada que você fornece a um modelo de IA para orientar sua resposta ou execução de tarefa.

#### 8. Engenharia de Prompts (Prompt Engineering)
A prática de estruturar, formular e refinar prompts sistematicamente para obter as respostas mais precisas, consistentes e úteis possíveis de um modelo de linguagem.

#### 9. System Prompt / Instrução do Sistema
Instruções de alto nível configuradas antes da conversa para definir o comportamento persistente da IA, seu tom, personalidade, regras de segurança, restrições e o escopo de atuação.

#### 10. Zero-shot vs. Few-shot Prompting
*   **Zero-shot:** Pedir à IA para realizar uma tarefa sem fornecer nenhum exemplo de resposta esperada.
*   **Few-shot:** Fornecer um ou mais exemplos estruturados de entrada e saída dentro do prompt para ensinar a IA o padrão de resposta que se deseja obter.

#### 11. Alucinação (Hallucination)
Fenômeno no qual o modelo de linguagem gera informações factualmente incorretas, inexistentes ou absurdas de maneira muito confiante e plausível. Geralmente ocorre por falta de dados reais sobre o assunto no treinamento ou por prompts ambíguos.

---

### ⚙️ Ajuste e Parâmetros de Configuração

#### 12. Fine-Tuning (Ajuste Fino)
Processo de pegar um modelo base já treinado e continuar seu treinamento em um conjunto de dados menor e específico para torná-lo especialista em uma tarefa, domínio ou estilo particular.

#### 13. RLHF (Reinforcement Learning from Human Feedback)
Aprendizado por Reforço com Feedback Humano. Método de alinhamento de LLMs onde revisores humanos avaliam e classificam as respostas da IA. O modelo é então treinado para maximizar as respostas preferidas pelos humanos, tornando-o mais seguro, prestativo e menos propenso a gerar conteúdos nocivos.

#### 14. Temperatura (Temperature)
Parâmetro de configuração que controla a criatividade e a aleatoriedade das respostas da IA. Valores baixos (perto de 0.0) tornam a IA determinística e factual (focando nos tokens mais prováveis), enquanto valores altos (perto de 1.0 ou mais) tornam as respostas mais criativas, variadas e imprevisíveis.

#### 15. Top-p (Nucleus Sampling)
Controla a diversidade de palavras consideradas pela IA ao acumular as opções mais prováveis até atingir uma probabilidade acumulada `p` (por exemplo, `p=0.9` avalia apenas as palavras que compõem 90% da probabilidade de ocorrência). Funciona como uma alternativa ou complemento à Temperatura.

---

### 🏗️ Integração e Arquitetura de Sistemas

#### 16. Embeddings
Representações matemáticas de palavras, frases ou parágrafos em vetores numéricos de alta dimensão. Textos com significados semanticamente semelhantes são mapeados para posições geometricamente próximas no espaço vetorial, permitindo que computadores comparem conceitos.

#### 17. Banco de Dados Vetorial (Vector Database)
Banco de dados especializado em armazenar e realizar buscas rápidas de proximidade em embeddings de alta dimensão. É essencial para sistemas de busca semântica e RAG.

#### 18. RAG (Retrieval-Augmented Generation)
Geração Aumentada de Recuperação. Arquitetura que estende as capacidades de um LLM buscando informações atualizadas ou privadas em uma base de dados externa (usando busca semântica em banco vetorial) e inserindo essas informações no prompt da IA para que ela responda com base em fatos reais e auditáveis.

#### 19. Agente de IA (AI Agent)
Um sistema de software que usa um LLM como cérebro central para planejar, decidir e executar tarefas complexas de forma autônoma. O agente decide quais ferramentas chamar e como prosseguir iterativamente até alcançar o objetivo estabelecido.

#### 20. Chamada de Função (Function Calling / Tool Use)
Capacidade do modelo de reconhecer quando uma tarefa exige acesso a informações externas ou ações do sistema (ex: consultar um banco de dados, enviar um e-mail ou fazer contas) e retornar um JSON formatado indicando qual função chamar e com quais argumentos.
