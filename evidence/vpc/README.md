# Parte A.4 — Rede (VPC)

Documentação da camada de rede do Assistente de Triagem do banco digital. Esta etapa foi realizada **apenas por observação** da VPC já provisionada na conta da turma, sem criação de novos recursos, conforme definido no escopo do desafio.

## Responsabilidade pela frente

Fiquei responsável pela frente de **Rede (VPC)** por ter interesse nas áreas de **redes de computadores, infraestrutura e segurança da informação**, temas que venho estudando e explorando durante minha formação acadêmica em Ciência da Computação.

A atividade também foi uma oportunidade de aproximar esses conhecimentos do contexto de computação em nuvem, permitindo compreender na prática como conceitos de rede são aplicados na AWS por meio de recursos como **VPC, subnets, Security Groups, tabelas de rotas e Internet Gateway**.

## Recursos identificados

| Recurso          | ID                         | Detalhe                               |
| ---------------- | -------------------------- | ------------------------------------- |
| VPC              | `vpc-08460275458d37186`    | CIDR `172.31.0.0/16`, padrão da conta |
| Subnet           | `subnet-0e117f9834f2564f3` | us-east-2a — `172.31.0.0/20`          |
| Subnet           | `subnet-0d64ef5bf5bcae92a` | us-east-2b — `172.31.16.0/20`         |
| Subnet           | `subnet-08a02f740f55e29ee` | us-east-2c — `172.31.32.0/20`         |
| Security Group   | `sg-09e6d79fec42b1316`     | default da VPC                        |
| Internet Gateway | `igw-0a4c9fd49bb062fdc`    | conexão com a internet                |
| Tabela de rotas  | `rtb-01b2d495941f3587c`    | principal                             |

As capturas de tela correspondentes estão nesta mesma pasta (`evidence/vpc`), com o ID da conta AWS coberto por segurança. Os IDs da VPC, das subnets e do Security Group foram mantidos por serem relevantes para fundamentar e identificar os recursos analisados.

## O que foi observado

* **3 subnets em zonas de disponibilidade diferentes** (`us-east-2a`, `us-east-2b` e `us-east-2c`). Essa distribuição representa apenas o pré-requisito estrutural para alta disponibilidade e não garante HA por si só. Para isso, a aplicação precisaria ser implantada em recursos replicados em pelo menos duas dessas zonas, o que está fora do escopo deste protótipo.

* **Security Group default:** a regra de entrada permite tráfego quando a origem é o próprio grupo, enquanto a regra de saída permite tráfego para `0.0.0.0/0`. Dessa forma, a regra observada não libera diretamente a entrada de qualquer endereço da internet.

* O **Security Group** atua como uma camada de controle de rede independente das permissões de IAM. Mesmo que uma identidade possua determinada autorização via IAM, o tráfego destinado a um recurso dentro da VPC também precisa ser permitido pelas regras de rede aplicáveis.

## Limitações e pontos de atenção

* O Security Group analisado controla o tráfego relacionado aos recursos **dentro da VPC**. Ele não controla diretamente o acesso ao Amazon S3 ou ao Amazon Bedrock, que são serviços gerenciados da AWS. Para uma arquitetura que necessite comunicação privada com esses serviços, seria necessário avaliar a utilização de **VPC Endpoints**, incluindo tecnologias como AWS PrivateLink, de acordo com o serviço utilizado.

* Foi identificada uma **divergência de região**: a VPC analisada está em `us-east-2`, enquanto o bucket S3 utilizado na Parte A.3 está em `us-east-1`. Isso não impede o funcionamento do protótipo, mas, em uma arquitetura real, seria importante avaliar o alinhamento das regiões para reduzir latência e possíveis custos relacionados à transferência de dados entre regiões.

## Escopo

Nenhum novo recurso de rede foi criado ou alterado durante esta atividade. O trabalho consistiu exclusivamente na **observação, análise e documentação da topologia de rede já existente** na conta da turma, respeitando o escopo definido pelo desafio.
