# Evidências de armazenamento (Amazon S3)

Esta pasta reúne as evidências da frente de **Armazenamento (Amazon S3)** do protótipo Assistente de Triagem Pix na AWS, desenvolvido pela Squad 4 (AI/R Agentic AI Engineering).

## Minha participação no protótipo

Fiquei responsável pela frente de **Documentos (Amazon S3)**, atuando por meio da role `Gerenciamento_S3_Desafio_Kaique`, criada sob o princípio de menor privilégio para conceder apenas as permissões necessárias à minha contribuição.

Minhas responsabilidades no projeto foram:

- Criar e configurar o bucket oficial `squad-pix-14-08-2026`, na região `us-east-1`, que armazena os quatro manuais públicos do Banco Central usados como base de consulta do assistente.
- Bloquear o acesso público ao bucket, mantendo a propriedade dos objetos centralizada no dono do bucket (ACLs desabilitadas).
- Ativar a criptografia padrão do lado do servidor (SSE-S3).
- Ativar o versionamento do bucket, permitindo recuperar versões anteriores de um documento em caso de substituição ou remoção indevida.
- Aplicar etiquetas (`Project` e `Squad`) para apoiar a rastreabilidade e a alocação de custos.
- Organizar os documentos sob o prefixo `knowledge-base/`, preparando a estrutura para uma futura integração com Amazon Bedrock Knowledge Bases.
- Enviar (upload) os quatro manuais oficiais do Pix ao bucket.

A política de identidade `Gerenciamento_S3_Desafio_Kaique` me permite gerenciar completamente o bucket e seus objetos (criar, apagar, configurar, enviar e remover documentos), mas **não inclui** `s3:PutBucketPolicy` nem `s3:PutBucketAcl` — as ações que tornariam o bucket público. Essa restrição foi proposital: consigo administrar o conteúdo do bucket, mas não consigo abri-lo para a internet, o que é importante no contexto de um banco digital.

> Repositório completo do projeto: https://github.com/cleidyanne-castro/aws-digital-bank-triage-assistant/tree/main/evidence/s3

## Evidências

### 1. Bucket oficial criado

![Bucket oficial criado](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/bucket-criado.png)

*Lista de buckets de uso geral exibindo o bucket único do projeto (`squad-pix-14-08-2026`), na região us-east-1, com a data de criação.*

### 2. Configuração geral do bucket

![Configuração geral do bucket](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/configuracao-geral-bucket.png)

*Tela de criação do bucket mostrando a região us-east-1, o tipo "bucket de uso geral" e o namespace global escolhido para manter compatibilidade com o formato de ARN exigido pela política de menor privilégio (IAM).*

### 3. Bloqueio total de acesso público

![Bloqueio total de acesso público](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/configuracoes-acesso.png)

*Configuração do Amazon S3 com a opção "Bloquear todo o acesso público" ativada, junto das suas quatro proteções associadas, evitando que o bucket seja exposto por descuido.*

### 4. Criptografia e configurações avançadas

![Criptografia e configurações avançadas](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/criptografia-e-configuracoes-avancadas.png)

*Criação do bucket com criptografia gerenciada pelo Amazon S3 (SSE-S3) selecionada, protegendo os objetos armazenados com chaves gerenciadas pelo próprio serviço.*

### 5. Propriedade de objetos imposta pelo dono do bucket

![Propriedade de objetos](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/prioridade-objeto-bucket.png)

*Tela indicando que as ACLs estão desabilitadas e que todos os objetos do bucket pertencem à conta proprietária, com o acesso definido exclusivamente por políticas.*

### 6. Versionamento e etiquetas do projeto

![Versionamento e etiquetas](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/versionamento-e-tags-buckets.png)

*Versionamento do bucket ativado e etiquetas `Project = Bedrock triage assistant` e `Squad = 4` aplicadas para organização e rastreabilidade de custos.*

### 7. Upload dos manuais oficiais

![Upload bem-sucedido dos manuais](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/upload_de_arquivos.png)

*Resumo do envio dos quatro manuais em PDF do Banco Central para a pasta `knowledge-base/` do bucket, todos concluídos com sucesso e sem erros.*

### 8. Documentos disponíveis na base de conhecimento

![Documentos na knowledge-base](https://raw.githubusercontent.com/cleidyanne-castro/aws-digital-bank-triage-assistant/main/evidence/s3/arquivos.png)

*Lista da pasta `knowledge-base/` com os quatro documentos oficiais do Pix: fluxos do processo de efetivação, requisitos mínimos de experiência do usuário, tempos do Pix e resolução de disputas.*

---
