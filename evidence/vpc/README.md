# Parte A.4 — Rede (VPC)

Documentação da camada de rede do assistente de triagem do banco digital. Esta etapa foi feita **apenas por observação** da VPC já provisionada na conta da turma, sem criação de novos recursos — conforme escopo do desafio.

## Recursos identificados

| Recurso | ID | Detalhe |
|---|---|---|
| VPC | `vpc-08460275458d37186` | CIDR `172.31.0.0/16`, padrão da conta |
| Subnet | `subnet-0e117f9834f2564f3` | us-east-2a — `172.31.0.0/20` |
| Subnet | `subnet-0d64ef5bf5bcae92a` | us-east-2b — `172.31.16.0/20` |
| Subnet | `subnet-08a02f740f55e29ee` | us-east-2c — `172.31.32.0/20` |
| Security Group | `sg-09e6d79fec42b1316` | default da VPC |
| Internet Gateway | `igw-0a4c9fd49bb062fdc` | conexão com a internet |
| Tabela de rotas | `rtb-01b2d495941f3587c` | principal |

As capturas de tela correspondentes estão nesta mesma pasta (`evidence/vpc`), com o ID da conta AWS coberto por segurança — os IDs de VPC, subnet e security group foram mantidos por fundamentarem a análise.

## O que foi observado

- **3 subnets em zonas de disponibilidade diferentes** (us-east-2a/2b/2c). Isso é só o pré-requisito estrutural para alta disponibilidade — não garante HA sozinho, pois a aplicação precisaria ser implantada em recursos replicados em pelo menos duas dessas zonas, o que está fora do escopo deste protótipo.
- **Security group default**: entrada restrita ao próprio grupo (nenhum acesso direto da internet); saída liberada para `0.0.0.0/0`. Funciona como uma segunda camada de proteção, independente do IAM — mesmo com permissão de IAM concedida, o tráfego só chega ao recurso se o security group também permitir.

## Limitações e pontos de atenção

- O security group protege apenas o tráfego **dentro da VPC**. Ele não cobre o acesso ao S3 nem ao Bedrock, que são serviços gerenciados acessados via API/console fora da VPC. Para tráfego privado até esses serviços seria necessário criar **VPC endpoints (AWS PrivateLink)**.
- Há uma **divergência de região**: a VPC está em `us-east-2`, enquanto o bucket S3 (Parte A.3) está em `us-east-1`. Não impede o funcionamento do protótipo, mas numa arquitetura real as regiões deveriam ser alinhadas para reduzir latência e custo de transferência entre regiões.

## Escopo

Nenhum recurso de rede foi criado nesta atividade — apenas observação e descrição da topologia já existente, conforme exigido pelo desafio.
