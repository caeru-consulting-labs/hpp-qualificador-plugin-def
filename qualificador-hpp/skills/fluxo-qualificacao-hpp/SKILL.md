---
name: "fluxo-qualificacao-hpp"
description: "Use whenever the user asks to run a complete HPP qualification for a company or CNPJ. Orchestrates the full workflow across the specialized HPP tools and skills, continuing automatically from company consultation and qualification through candidate selection, decision-maker enrichment, and Pipefy registration whenever the company is eligible to proceed."
---

# Fluxo de Qualificação HPP

## Objetivo

Orquestrar o processo completo de qualificação HPP.

Esta Skill não substitui as Skills especializadas e não refaz suas regras de negócio.

## Fluxo

Quando o usuário pedir para qualificar uma empresa ou CNPJ:
1. Use `Consultar Empresa`.
2. Use `Qualificar Empresa`.
3. Aplique as regras da Skill `qualificar-empresa-hpp` ao resultado.
4. Preserve integralmente o resultado final produzido por
   `qualificar-empresa-hpp`. Esse objeto é a fonte de verdade da
   qualificação para o restante do fluxo.
5. Se a empresa estiver apta a continuar, use `Buscar Candidatos`.
6. Aplique as regras da Skill `selecionar-decisores-hpp` e use
   `Enriquecer Decisores` para os candidatos selecionados.
7. Use `Cadastrar no Pipefy`.
   Ao cadastrar:
   - use como `qualificacao` exatamente o resultado final preservado no passo 4;
   - não substitua `qualificacao` pelo retorno bruto de `Qualificar Empresa`;
   - não reconstrua, resuma ou renomeie `scoring` ou `resumo_fit`;
   - acrescente apenas os dados finais da empresa e dos decisores enriquecidos.
8. Apresente o resultado final da qualificação.
9. Identifique os decisores selecionados que possuem:
   - `email` preenchido;
   - `email_status = "verified"`;
   - `identidade_apollo = "confirmado"`;
   - nenhuma divergência relevante de identidade ou vínculo.
10. Se houver pelo menos um, informe quais são e pergunte se o usuário
    deseja preparar e enviar e-mails personalizados para esses decisores.
11. Interrompa o fluxo e aguarde confirmação explícita.
12. Somente após confirmação, aplique a Skill `abordagem-email-hpp`.

## Continuidade automática

Não peça confirmação entre as etapas.

Não pergunte:
- "Quer que eu busque candidatos?"
- "Quer que eu continue?"
- "Quer que eu enriqueça os decisores?"
- "Quer que eu cadastre no Pipefy?"

Quando o usuário pede uma qualificação HPP, essas etapas fazem parte da mesma tarefa.

A abordagem por e-mail NÃO faz parte da continuidade automática.

O envio de e-mails exige confirmação explícita do usuário após a
qualificação, enriquecimento e cadastro no Pipefy.

## Quando interromper

Pare o fluxo apenas se houver impedimento real retornado pelas ferramentas, por exemplo:

- empresa não elegível;
- `can_continue = false`;
- status fiscal que exija revisão;
- erro de ferramenta que impossibilite a próxima etapa;
- ausência de candidatos plausíveis;
- dado obrigatório ausente.

Nesse caso, informe o motivo da interrupção.