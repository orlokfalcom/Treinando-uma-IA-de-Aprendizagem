# 🟢 Engenharia de Prompts Bancários: Nível Básico

Esta seção apresenta técnicas e templates de prompts básicos adaptados para resolver problemas comuns de sistemas bancários e atendimento ao cliente.

---

## 1. Classificação Semântica de Faturas de Cartão (Instrução Direta)

Bancos geram extratos com descrições sujas provenientes das adquirentes (ex: "UBER *TRIP HELP", "IFOOD *RESTAURANTE"). A IA ajuda a categorizar esses gastos em grupos claros para o cliente.

### 📋 Prompt / Template:
```text
Atue como um motor de classificação de despesas de cartão de crédito.
Sua tarefa é analisar a descrição de uma transação e classificá-la em uma das seguintes categorias:
[Alimentação, Transporte, Saúde, Supermercado, Lazer, Educação, Combustível, Outros]

Regras:
- Retorne apenas a categoria correspondente em letras maiúsculas.
- Não inclua nenhuma explicação ou pontuação.

Descrição da Transação: """[Descrição da Transação]"""
Categoria:
```

### 💬 Exemplos Reais de Execução:
*   *Input:* `UBER *TRIP HELP SAN FRANCISCO` $\rightarrow$ *Output:* `TRANSPORTE`
*   *Input:* `IFOOD *RUSTIC BURGER CURITIBA` $\rightarrow$ *Output:* `ALIMENTAÇÃO`
*   *Input:* `POSTO IPIRANGA JACAREI` $\rightarrow$ *Output:* `COMBUSTÍVEL`
*   *Input:* `DROGASIL FILIAL 102` $\rightarrow$ *Output:* `SAÚDE`

---

## 2. Classificação de Intenção de Suporte (Few-shot Prompting)

Em canais de atendimento digital (WhatsApp/App), classificar com precisão o que o cliente deseja ajuda a direcionar a conversa para a API correta de autoatendimento ou para a fila humana adequada.

### 📋 Prompt / Template:
```text
Você é o assistente inteligente de triagem do Banco.
Classifique a mensagem do usuário em uma das seguintes categorias de intenção:
- BLOQUEIO_CARTAO (se o cliente perdeu, foi roubado ou quer inativar o cartão)
- DUVIDA_PIX (se tem dúvidas ou problemas em transações Pix)
- SEGUNDA_VIA_BOLETO (solicitação de faturas ou boletos de empréstimo)
- SALDO_EXTRATO (consulta de valores em conta)
- CONTESTACAO_COMPRA (relato de compras não reconhecidas)
- OUTROS (qualquer assunto fora dos tópicos acima)

Use os exemplos abaixo como referência de classificação:

Entrada: "perdi minha carteira na rua e preciso cancelar meu cartão urgente"
Saída: BLOQUEIO_CARTAO

Entrada: "não estou conseguindo fazer uma transferência pix, dá erro de limite"
Saída: DUVIDA_PIX

Entrada: "me manda o PDF da fatura que vence amanhã por favor"
Saída: SEGUNDA_VIA_BOLETO

Entrada: "quero ver quanto sobrou na minha conta hoje"
Saída: SALDO_EXTRATO

Entrada: "apareceu uma compra de R$ 300 reais no meu cartão que eu não fiz"
Saída: CONTESTACAO_COMPRA

Entrada: "[Nova Mensagem do Usuário]"
Saída:
```

### 💬 Exemplo de Uso Real:
*   *Input:* "alguém clonou meu cartão e passou uma compra de madrugada" $\rightarrow$ *Output:* `CONTESTACAO_COMPRA`

---

## 3. Delimitação de Dados em Logs de Suporte

Ao lidar com transcrições de chat ou áudio para análise de qualidade, use tags XML para garantir que a IA processe apenas a transcrição do cliente, ignorando comandos intrusivos.

### 📋 Prompt / Template:
```text
Analise a transcrição de atendimento bancário contida dentro das tags <transcricao>.
Gere um resumo em formato JSON contendo os seguintes campos:
- "assunto_principal": Breve descrição do problema do cliente.
- "sentimento_cliente": Classifique em (Positivo, Neutro, Irritado).
- "resolvido": (true ou false).

<transcricao>
Atendente: Olá, como posso te ajudar?
Cliente: Oi, eu tentei pagar uma conta de luz usando o leitor de código de barras, mas o aplicativo fechou sozinho duas vezes e não sei se o pagamento foi concluído.
Atendente: Vou verificar no sistema. Qual o seu CPF?
Cliente: É o 000.111.222-33.
Atendente: Consta aqui que o pagamento foi liquidado com sucesso às 14:32. O comprovante já está no seu e-mail.
Cliente: Ah, que ótimo! Fiquei com medo de pagar duas vezes. Muito obrigado pelo retorno rápido!
Atendente: Por nada, posso ajudar em algo mais?
Cliente: Só isso, tchau.
</transcricao>
```
