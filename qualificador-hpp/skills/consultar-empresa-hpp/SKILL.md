---
name: consultar-empresa-hpp
description: Use when the user wants to identify, confirm, inspect, or retrieve cadastral and economic data for a Brazilian company before HPP qualification.
---

# Consultar Empresa HPP

## Objetivo

Usar a ferramenta MCP **Consultar Empresa** para obter e confirmar os dados estruturados de uma empresa pelo CNPJ.

Esta Skill representa a etapa de consulta e preparação de dados. Ela **não** substitui a qualificação HPP, não calcula score ICP e não decide elegibilidade fiscal.

## Quando usar

Use esta Skill quando o usuário quiser:

- consultar um CNPJ;
- confirmar razão social ou nome fantasia;
- visualizar situação cadastral;
- obter endereço, CNAEs, natureza jurídica, porte ou capital social;
- verificar faturamento ou funcionários quando disponíveis;
- conhecer sócios;
- preparar a empresa para uma qualificação HPP posterior.

Se o usuário pedir qualificação, score ICP, potencial FIA, histórico de incentivos, fit social ou prioridade comercial, use também a Skill **qualificar-empresa-hpp**.

## Ferramenta MCP

Ferramenta principal:

`Consultar Empresa`

### Entrada principal

- `cnpj`: CNPJ da empresa.

Utilize os demais campos somente quando a própria ferramenta os expuser e houver dado explícito do usuário para preenchê-los.

## Fluxo

1. Normalize mentalmente o CNPJ apenas para entender a intenção do usuário.
2. Chame **Consultar Empresa** com o CNPJ informado.
3. Use o retorno da ferramenta como fonte de verdade para os dados cadastrais e econômicos.
4. Apresente somente os dados relevantes ao pedido.
5. Se o usuário quiser seguir para qualificação HPP, use a Skill de qualificação.

## Regras obrigatórias

Nunca conclua, apenas com esta ferramenta, que a empresa:

- é ou não é elegível para o HPP;
- está ou não em Lucro Real, quando isso não estiver explicitamente confirmado pelo retorno;
- possui determinado score ICP;
- possui determinado potencial FIA;
- deve ser priorizada comercialmente;
- deve ser cadastrada no pipeline.

Nunca determine regime tributário a partir de:

- faturamento;
- porte;
- quantidade de funcionários;
- CNAE;
- natureza jurídica;
- capital social.

Esses dados podem ser contexto, mas não constituem prova do regime fiscal.

Não invente campos ausentes.

Quando um dado não estiver disponível, diga que não foi identificado.

## Relação com a qualificação

Quando o usuário pedir uma qualificação completa e houver CNPJ:

1. execute **Consultar Empresa** para garantir os dados/cache necessários;
2. em seguida, aplique a Skill **qualificar-empresa-hpp**.

Se a consulta desse mesmo CNPJ já tiver sido executada na conversa atual e os dados estiverem disponíveis, não é necessário repetir a consulta sem motivo.

## Formato de resposta

Para consultas simples, prefira uma resposta curta contendo, quando disponível:

- Razão social
- Nome fantasia
- CNPJ
- Situação cadastral
- Localização
- CNAE principal
- Porte
- Faturamento
- Funcionários
- Regime informado pela fonte, se houver
- Quantidade de sócios ou principais sócios, quando relevante

Finalize perguntando se o usuário quer qualificar a empresa apenas quando isso for útil ao contexto.
