# Assistente de Triagem Pix

> Prova de conceito da Squad 4 para apoiar o primeiro atendimento de clientes de um banco digital com mais agilidade, consistência e segurança.

## Visão executiva

O Assistente de Triagem Pix recebe uma mensagem fictícia, identifica o assunto principal e prepara uma resposta inicial com base em documentos públicos do Banco Central do Brasil.

A solução foi criada para demonstrar como a inteligência artificial pode apoiar o atendimento sem movimentar dinheiro, tomar decisões financeiras ou substituir a análise humana. Nenhum dado real de cliente, conta ou transação foi utilizado.

## O que foi desenvolvido?

Foi desenvolvida uma prova de conceito capaz de:

- direcionar mensagens para cinco assuntos: **Devolução, Limite, Golpe/Fraude, Agendamento e Chave Pix**;
- reconhecer solicitações que não pertencem ao escopo do assistente;
- consultar informações oficiais fornecidas à solução;
- produzir uma resposta inicial sem completar lacunas com informações não confirmadas;
- aplicar uma barreira de segurança antes de apresentar a resposta;
- registrar atividades, acompanhar sinais de funcionamento e visualizar custos da conta;
- manter documentos protegidos e acessíveis apenas às pessoas e aos serviços autorizados.

### Indicadores da demonstração

| Indicador | Resultado |
|---|---:|
| Assuntos de atendimento definidos | 5 |
| Mensagens fictícias avaliadas | 6 |
| Classificações corretas na amostra controlada | 6 de 6 |
| Documentos oficiais preparados como referência | 4 |
| Cenários de resposta baseada em documento | 3 |
| Dados reais de clientes utilizados | 0 |

O resultado de 6 em 6 representa apenas uma amostra pequena e controlada. Ele confirma a viabilidade da proposta, mas não equivale ao desempenho esperado em produção.

## Por que esta solução importa?

Equipes de atendimento recebem muitas perguntas repetidas sobre Pix. O desafio não é apenas responder rápido: é responder de forma consistente, usar uma fonte confiável e reconhecer quando a situação precisa ser encaminhada.

A proposta pode gerar valor ao negócio ao:

- reduzir o tempo gasto na identificação do motivo do contato;
- aumentar a consistência do primeiro atendimento;
- facilitar o direcionamento para a fila adequada;
- diminuir respostas sem fundamento;
- apoiar a rastreabilidade das decisões;
- criar uma base segura para futuras automações.

Esses benefícios são potenciais e precisam ser confirmados em uma etapa posterior, com maior volume de testes e indicadores operacionais.

## Como funciona?

1. **Receber:** o cliente envia uma mensagem sobre Pix.
2. **Identificar:** o assistente reconhece o assunto e direciona a solicitação.
3. **Consultar:** a resposta utiliza informações oficiais disponibilizadas à solução.
4. **Verificar:** uma barreira avalia se a solicitação está dentro do escopo permitido.
5. **Responder ou encaminhar:** o assistente apresenta uma orientação inicial ou informa que o caso exige outro canal.

A solução também mantém controles de acesso, histórico de atividades, acompanhamento do ambiente e visibilidade de custos. Assim, o ganho de agilidade não fica separado da segurança e da governança.

## Quando esta solução deve ser utilizada?

O projeto está na fase de **prova de conceito validada em ambiente controlado**. Ele está pronto para demonstração e avaliação dos aprendizados da Sprint 4, mas ainda não é um produto bancário de produção.

Antes de uma utilização real, será necessário:

- ampliar a quantidade e a variedade dos testes;
- incluir mensagens ambíguas e situações de exceção;
- definir metas de qualidade, tempo de resposta e encaminhamento;
- realizar avaliações de privacidade, segurança, risco e conformidade;
- integrar a solução aos canais e processos de atendimento;
- acompanhar a qualidade das respostas ao longo do tempo;
- validar custos em um ambiente dedicado.

## Quem participou?

O trabalho foi desenvolvido pela **Squad 4 - AI/R Agentic AI Engineering**, com responsabilidades complementares:

| Integrante | Contribuição para a entrega |
|---|---|
| **Cleidyanne Castro Pereira** | Produto, visão da solução, consolidação do relatório, acompanhamento do ambiente e apresentação executiva. |
| **João Vitor Althaus Godoi** | Organização dos acessos e separação segura de responsabilidades. |
| **Kaique Silva Sousa** | Armazenamento protegido e organização dos documentos oficiais. |
| **Natan Alencar Maia** | Levantamento da estrutura de rede e dos controles de comunicação. |
| **Bruno Jordão das Neves Moura** | Avaliação dos modelos, testes de triagem, respostas baseadas em documentos e análise de evolução da base de conhecimento. |
| **José Ivanildo de Oliveira Marques** | Regras de segurança e conformidade aplicadas às respostas. |

## Resultados de negócio observados

A demonstração confirmou que a proposta consegue:

- classificar corretamente as seis mensagens da amostra;
- recusar uma solicitação fora do escopo definido;
- responder quando a informação está presente no documento;
- reconhecer quando o documento não possui informação suficiente;
- bloquear uma orientação de investimento após a aplicação da barreira de segurança;
- manter evidências de acesso, armazenamento, testes, acompanhamento e custos.

A escolha do modelo considerou qualidade suficiente para o cenário e menor custo estimado entre as opções avaliadas. Os números obtidos no ambiente de teste não devem ser tratados como previsão de custo ou desempenho em produção.

## Limites da prova de conceito

Esta entrega:

- não usa dados reais de clientes;
- não movimenta valores;
- não executa transações Pix;
- não oferece recomendação financeira;
- não substitui atendimento humano, jurídico ou de segurança;
- não representa uma solução pronta para produção.

Casos de fraude, risco financeiro, dados pessoais, conflito de informação ou ausência de fonte confiável devem ser encaminhados para análise humana.

## Visão da solução

![Diagrama conceitual do assistente: a mensagem passa pela triagem, consulta a documentos oficiais e regras de segurança antes da resposta.](docs/architecture/Arquitetura.png)

A arquitetura conceitual mostra como atendimento, documentos oficiais, inteligência artificial e controles de segurança trabalham em conjunto. Ela representa a visão da solução e não uma implantação bancária completa.

## Materiais para consulta

- [Arquitetura conceitual](docs/architecture/Arquitetura.png)
- [Evidências da demonstração](evidence/)
- [Testes do assistente](evidence/bedrock/)
- [Evidências de acompanhamento e custos](evidence/observability/)
- [Prompts utilizados nas avaliações](prompts/)
- [Licença do projeto](LICENSE)

## Próxima evolução recomendada

A próxima fase deve transformar a prova de conceito em um piloto mensurável. A prioridade é ampliar os testes, automatizar a consulta aos documentos oficiais, definir indicadores de negócio e submeter a solução às avaliações de segurança, privacidade e conformidade exigidas para um ambiente bancário.

---

**Squad 4 - AI/R Agentic AI Engineering**  
Projeto educacional desenvolvido no contexto da Sprint 4.
