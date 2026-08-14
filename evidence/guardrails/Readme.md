# 🛡️ Evidências de Conformidade & Bedrock Guardrails

Este diretório reúne os registros visuais, capturas de tela (*screenshots*) e configurações técnicas que comprovam a implementação e validação dos **Bedrock Guardrails** no projeto **AWS Digital Bank Pix Triage Assistant**.

Os testes foram conduzidos utilizando a role de IAM `Gerenciamento_Bedrock_Desafio_Jose`, o modelo **Amazon Nova Micro** e os prompts de resposta fundamentada baseados nos manuais oficiais armazenados no S3.

---

## Configuração

**Tópicos Negados (*Denied Topics*):** Definição de bloqueios preventivos para barrar requisições sobre:
  * *Recomendação de Investimentos e Orientação Financeira:* Impedimento de sugestões sobre aplicação de valores, compra de ações ou conselhos de rentabilidade.
  * *Concessão e Promessa de Crédito:* Bloqueio de solicitações, renegociações de dívidas ou ofertas de empréstimo fora do escopo funcional do Pix.
  * *Produtos e Serviços Fora do Escopo:* Redirecionamento de qualquer consulta que desvie das operações nativas do Pix (devoluções, limites, chaves, agendamentos e fraudes).
  ![alt text](image.png)


* **Filtros de Conteúdo (*Content Filters*):** 
  Configuração de limiares de detecção (*thresholds*) rígidos para identificar e bloquear entradas ou saídas de texto contendo conteúdos nocivos ou inadequados. A política aplica filtros automatizados contra:
  * *Hate Speech* (Discurso de ódio)
  * *Harassment* (Assédio e intimidação)
  * *Sexual Content* (Conteúdo explícito/sexual)
  * *Violence* (Conteúdo violento ou que incite danos)
  * *Prompt Attack / Jailbreak:* Detecção e bloqueio automático de tentativas de manipulação do prompt do sistema (*Prompt Injection*) para desviar o comportamento do assistente.

![alt text](image-1.png)

* **Filtros de Palavras e Termos Indesejados (*Word Filters*):** 
  Implementação de listas personalizadas de bloqueio (*Custom Profanity & Term Lists*) focadas na linguagem bancária e operacional. O filtro impede o processamento de:
  * Termos chulas, profanos ou ofensivos em interações de atendimento ao cliente.
  * Jargões informais ou termos proibidos que possam comprometer o tom corporativo e formal exigido nas operações do Pix.
  
  ![alt text](image-2.png)
  ![alt text](image-3.png)

* **Filtros de Informações Sensíveis (*Sensitive Information Filters / PII*):** 
  Atuação de mecanismos de mascaramento e prevenção contra vazamento de dados de identificação pessoal (*Personally Identifiable Information - PII*). O Guardrail analisa e sanitiza o fluxo de mensagens para evitar a exposição indevida de dados regulados (em conformidade com a LGPD e diretrizes do BCB), tais como:
  * Números de CPF e CNPJ de clientes ou terceiros.
  * Chaves Pix sensíveis (e-mail, telefone ou números de contas bancárias em texto puro).
  * Senhas, tokens de autenticação ou códigos de verificação de segurança (CVV/OTP).
  
  ![alt text](image-4.png)
  
* **Mensagem de Recusa Determinística:** Em caso de acionamento dos filtros, o assistente padroniza a resposta de bloqueio sem fornecer direcionamentos externos:
  > *"Desculpe, como assistente do banco digital focado no Pix, não posso responder a essa solicitação ou fornecer esse tipo de recomendação. Por favor, reformule sua pergunta sobre o Pix ou entre em contato com nossos canais de atendimento oficiais."*


## Detalhamento dos Testes das Camadas de Filtro

### Validar Devolução
- Sem Guardrails: Modelo responde corretamente, baseado no contexto fornecido 
![alt text](image-5.png)
- Com Guardrails: Modelo mantém o padrão de resposta
  ![alt text](image-6.png)

### Prazo de Devolução 
- Sem Guardrails: Modelo fornece mensagem de não encontrar informação no contexto
![alt text](image-7.png)
- Com Guardrails: Modelo fornece mensagem eficiente e segura. 
![alt text](image-8.png)

### Recomendação de investimento
- Sem Guardrails: Modelo oferece recomendação de investimento, algo proibido nas regras
![alt text](image-9.png)
- Com guardrails: Modelo retorna mensagem padrão, seguindo as regras pré estabelecidas contra recomendação de investimentos.
![alt text](image-10.png)
- Teste dulo com Guardrails: Modelo responde de forma segura com os 2 prompts.
![alt text](image-11.png)


#### Realizado por José Ivanildo








