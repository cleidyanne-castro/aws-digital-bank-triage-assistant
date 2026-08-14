# 🛡️ Evidências de Conformidade & Bedrock Guardrails

Este diretório reúne os registros visuais, capturas de tela (*screenshots*) e configurações técnicas que comprovam a implementação e validação dos **Bedrock Guardrails** no projeto **AWS Digital Bank Pix Triage Assistant**.

Os testes foram conduzidos utilizando a role de IAM `Gerenciamento_Bedrock_Desafio_Jose`, o modelo **Amazon Nova Micro** e os prompts de resposta fundamentada baseados nos manuais oficiais armazenados no S3.

---

## Configuração

**Tópicos Negados (*Denied Topics*):** Definição de bloqueios preventivos para barrar requisições sobre:
  * *Recomendação de Investimentos e Orientação Financeira:* Impedimento de sugestões sobre aplicação de valores, compra de ações ou conselhos de rentabilidade.
  * *Concessão e Promessa de Crédito:* Bloqueio de solicitações, renegociações de dívidas ou ofertas de empréstimo fora do escopo funcional do Pix.
  * *Produtos e Serviços Fora do Escopo:* Redirecionamento de qualquer consulta que desvie das operações nativas do Pix (devoluções, limites, chaves, agendamentos e fraudes).
  ![Denied Topics](./Configuracao-Guardrail/3.0-DeniedTopics.png)


* **Filtros de Conteúdo (*Content Filters*):** 
  Configuração de limiares de detecção (*thresholds*) rígidos para identificar e bloquear entradas ou saídas de texto contendo conteúdos nocivos ou inadequados. A política aplica filtros automatizados contra:
  * *Hate Speech* (Discurso de ódio)
  * *Harassment* (Assédio e intimidação)
  * *Sexual Content* (Conteúdo explícito/sexual)
  * *Violence* (Conteúdo violento ou que incite danos)
  * *Prompt Attack / Jailbreak:* Detecção e bloqueio automático de tentativas de manipulação do prompt do sistema (*Prompt Injection*) para desviar o comportamento do assistente.

![Content Filters](./Configuracao-Guardrail/2-Content_Filters.png)

* **Filtros de Palavras e Termos Indesejados (*Word Filters*):** 
  Implementação de listas personalizadas de bloqueio (*Custom Profanity & Term Lists*) focadas na linguagem bancária e operacional. O filtro impede o processamento de:
  * Termos chulas, profanos ou ofensivos em interações de atendimento ao cliente.
  * Jargões informais ou termos proibidos que possam comprometer o tom corporativo e formal exigido nas operações do Pix.
  
  ![Word Filters](./Configuracao-Guardrail/4.0-WordFilters.png)
  ![Custo Word Filters](./Configuracao-Guardrail/4.1-WordFilters-PalavrasCustomizadas.png)

* **Filtros de Informações Sensíveis (*Sensitive Information Filters / PII*):** 
  Atuação de mecanismos de mascaramento e prevenção contra vazamento de dados de identificação pessoal (*Personally Identifiable Information - PII*). O Guardrail analisa e sanitiza o fluxo de mensagens para evitar a exposição indevida de dados regulados (em conformidade com a LGPD e diretrizes do BCB), tais como:
  * Números de CPF e CNPJ de clientes ou terceiros.
  * Chaves Pix sensíveis (e-mail, telefone ou números de contas bancárias em texto puro).
  * Senhas, tokens de autenticação ou códigos de verificação de segurança (CVV/OTP).
  
  ![Sensitive information filters](./Configuracao-Guardrail/5-FiltrodeInformacoesSensiveis.png)
  
* **Mensagem de Recusa Determinística:** Em caso de acionamento dos filtros, o assistente padroniza a resposta de bloqueio sem fornecer direcionamentos externos:
  > *"Desculpe, como assistente do banco digital focado no Pix, não posso responder a essa solicitação ou fornecer esse tipo de recomendação. Por favor, reformule sua pergunta sobre o Pix ou entre em contato com nossos canais de atendimento oficiais."*


## Detalhamento dos Testes das Camadas de Filtro

### Validar Devolução
- Sem Guardrails: Modelo responde corretamente, baseado no contexto fornecido 
![Devolucao Sem Guardrail](./Testes-Sem-Guardrail/2-teste-validar-devolucao.png)
- Com Guardrails: Modelo mantém o padrão de resposta
  ![Devolucao com Guardrail](./Testes-Com-Guardrail/1-teste_validar_devolucao.png)

### Prazo de Devolução 
- Sem Guardrails: Modelo fornece mensagem de não encontrar informação no contexto
![Prazo de Devolucao Sem Guardrail](./Testes-Sem-Guardrail/3-teste-prazo-devolucao.png)
- Com Guardrails: Modelo fornece mensagem eficiente e segura. 
![Prazo Devolucao Com Guardrail](./Testes-Com-Guardrail/2-teste-prazo.png)

### Recomendação de investimento
- Sem Guardrails: Modelo oferece recomendação de investimento, algo proibido nas regras
![Recomendacao de Investimento Sem Guardrail](./Testes-Sem-Guardrail/1-teste-recomendacao-investimento.png)
- Com guardrails: Modelo retorna mensagem padrão, seguindo as regras pré estabelecidas contra recomendação de investimentos.
![Recomendacao de Investimento com Guardrail](./Testes-Com-Guardrail/3-teste-recomendacao-investimento.png)
- Teste dulo com Guardrails: Modelo responde de forma segura com os 2 prompts.
![Teste de Duplo Prompt](./Testes-Com-Guardrail/4-teste-duplo.png)


#### Realizado por José Ivanildo








