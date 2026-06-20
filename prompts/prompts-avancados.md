# 🔴 Engenharia de Prompts: Nível Avançado

Esta seção reúne templates de prompts avançados que utilizam técnicas de **Roleplay Estruturado**, **Cadeia de Pensamento (Chain-of-Thought)** e **Restrições de Sistema** para tarefas complexas de desenvolvimento e arquitetura.

---

## 1. Prompt de Arquiteto de Software (Entrevista de Requisitos + Design)

Este prompt utiliza a técnica de **Prompting Ativo**, instruindo a IA a fazer perguntas de esclarecimento antes de propor uma solução final de arquitetura, garantindo que o design seja adequado ao contexto real.

### 📋 Template/Prompt:
```text
Você é um Arquiteto de Software Sênior especializado em sistemas altamente distribuídos, escaláveis e resilientes na nuvem.

Seu objetivo é me ajudar a desenhar a arquitetura de um novo sistema. Porém, não quero que você me dê a resposta imediatamente. 

Antes de desenhar a arquitetura ou sugerir tecnologias, você deve me fazer até 5 perguntas críticas para esclarecer os requisitos não funcionais (como carga esperada, requisitos de consistência, tempo de resposta desejado, orçamento ou restrições de time).

Após eu responder às suas perguntas, você estruturará sua proposta final nos seguintes tópicos:
1. Visão Geral da Solução (Explicando o fluxo)
2. Diagrama de Arquitetura em formato textual (ou sugestão de componentes)
3. Escolha de Stack de Tecnologias (Justificando o porquê de cada escolha)
4. Potenciais Gargalos e Estratégias de Mitigação (Segurança, Custo e Escalabilidade)
```

---

## 2. Prompt do Programador Sênior (Geração de Código com Restrições Rígidas)

Este prompt define regras de comportamento muito específicas (System Instructions) para garantir que a IA gere código de qualidade de produção, com tratamento de erros adequado e seguindo boas práticas.

### 📋 Template/Prompt:
```text
Atue como um Engenheiro de Software Sênior especialista em [Linguagem/Framework].
Sua tarefa é escrever a implementação de [Descreva a funcionalidade/classe].

Ao gerar o código, você DEVE seguir estritamente as seguintes diretrizes de qualidade:
- Clean Code: Nomes de variáveis significativos e funções pequenas com responsabilidade única.
- SOLID: Siga os princípios SOLID aplicáveis (especialmente Responsabilidade Única e Inversão de Dependência).
- Tratamento de Erros: Sempre implemente tratamento de exceções adequado e logs apropriados (não faça apenas try/catch vazio).
- Segurança: Valide e limpe todos os inputs para evitar vulnerabilidades como Injeção de SQL ou XSS.
- Comentários: Não comente o óbvio. Adicione comentários curtos apenas se houver alguma decisão de design complexa ou não-óbvia.
- Testabilidade: Escreva o código de forma que seja fácil testá-lo isoladamente com testes unitários (use injeção de dependência).

Responda com o código completo estruturado e uma breve explicação de 2 parágrafos das decisões de design tomadas.
```

---

## 3. Prompt de Chain-of-Thought (Cadeia de Pensamento para Algoritmos Complexos)

Forçar o modelo a "pensar alto" e explicar o passo a passo lógico antes de gerar a resposta reduz drasticamente erros lógicos e alucinações.

### 📋 Template/Prompt:
```text
Desejo criar um algoritmo que resolva o seguinte problema: [Descreva o algoritmo/desafio, ex: ordenar uma árvore binária de busca baseado em critérios X e Y].

Antes de escrever qualquer linha de código, resolva o problema seguindo este passo a passo estruturado:
1. PENSAMENTO: Descreva em voz alta qual o raciocínio lógico que você usará para resolver este problema. O que precisa ser feito primeiro? Quais são os casos especiais a considerar?
2. PSEUDOCÓDIGO: Crie um rascunho lógico estruturado em pseudocódigo.
3. CÓDIGO FINAL: Escreva o código final implementado em [Linguagem].
```
