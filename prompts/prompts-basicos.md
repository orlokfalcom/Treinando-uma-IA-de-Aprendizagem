# 🟢 Engenharia de Prompts: Nível Básico

Esta seção apresenta técnicas básicas de Engenharia de Prompts estruturadas com exemplos reutilizáveis, práticos e explicações de por que funcionam.

---

## 1. Instrução Direta e Específica

Para obter boas respostas, evite perguntas vagas. Diga claramente o que você quer, quem o modelo deve ser, como deve formatar o resultado e o tom da resposta.

### 📋 Template:
```text
Atue como um [papel/persona].
Explique o conceito de [tema] para um público de [nível de conhecimento].
Sua resposta deve ser estruturada em [formato: tópicos/parágrafos] e ter no máximo [limite] palavras.
```

### 💬 Exemplo Real:
```text
Atue como um Engenheiro de Software Sênior especializado em Sistemas Distribuídos.
Explique o conceito de "Eventual Consistency" (Consistência Eventual) para um desenvolvedor júnior.
Sua resposta deve ser estruturada em até 3 tópicos curtos e didáticos.
```

---

## 2. Few-shot Prompting (Prompting com Exemplos)

Quando você quer que a IA aprenda um padrão de formatação ou um estilo de classificação que é difícil de explicar apenas com regras, você fornece alguns exemplos de entrada e saída.

### 📋 Template:
```text
Você é um classificador de [categoria].
Siga o padrão dos exemplos abaixo para classificar a última entrada:

Entrada: [Exemplo 1 - Entrada]
Saída: [Exemplo 1 - Saída]

Entrada: [Exemplo 2 - Entrada]
Saída: [Exemplo 2 - Saída]

Entrada: [Nova Entrada do Usuário]
Saída:
```

### 💬 Exemplo Real (Classificação de Sentimentos de Commits):
```text
Você é um bot que analisa mensagens de commit e classifica o tipo de alteração (Feature, Bugfix, Refactor, Docs).
Siga o padrão dos exemplos abaixo:

Entrada: "feat: add OAuth2 authentication endpoint"
Saída: FEATURE

Entrada: "fix: resolve memory leak on user database connection pool"
Saída: BUGFIX

Entrada: "docs: update API endpoints table in README"
Saída: DOCS

Entrada: "refactor: simplify calculateSalary business logic"
Saída: REFACTOR

Entrada: "fix: catch null pointer exception in user profile parser"
Saída:
```

---

## 3. Delimitadores de Contexto

Utilize delimitadores como aspas triplas `"""`, crases triplas ` ``` `, tags XML `<contexto></contexto>` ou tags Markdown para separar claramente o texto de contexto das instruções. Isso ajuda a evitar que o modelo se confunda com o texto que deve analisar.

### 📋 Template:
```text
Resuma o texto fornecido abaixo dentro das tags <texto>.
A resposta deve conter apenas uma frase curta resumindo o ponto principal.

<texto>
[Cole seu texto aqui]
</texto>
```

### 💬 Exemplo Real:
```text
Corrija quaisquer erros gramaticais e de digitação do trecho de código SQL dentro do bloco abaixo. Retorne apenas o SQL corrigido.

```sql
SELECT user_id, name, email FROM users WHERRE active = 1 AND create_date > '2023-01-01'
```
```
