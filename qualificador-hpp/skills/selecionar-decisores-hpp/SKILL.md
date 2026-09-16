---
name: selecionar-decisores-hpp
description: Use when the HPP qualification flow needs to identify, validate, rank, or select corporate decision-maker candidates for a company from the Buscar Candidatos MCP tool.
---

# Selecionar Decisores HPP

## Objetivo

Selecionar os **4 melhores candidatos corporativos** para abordagem do Hospital Pequeno Príncipe (HPP) a partir dos perfis retornados pela ferramenta MCP **Buscar Candidatos**.

Após a seleção, esta Skill também orquestra o enriquecimento dos decisores e o cadastro automático do resultado no Pipefy.

Esta Skill substitui o julgamento que antes era feito por agentes internos para:
- validar vínculo corporativo;
- avaliar aderência temática;
- avaliar poder de decisão, influência ou encaminhamento;
- classificar nível e score;
- selecionar os 4 melhores candidatos.

A ferramenta busca dados. **Esta Skill faz o julgamento.**

## Quando usar

Use quando o usuário pedir para:
- encontrar decisores, contatos ou responsáveis de uma empresa para o HPP;
- selecionar os melhores perfis para abordagem;
- continuar uma qualificação HPP até a etapa de decisores;
- analisar os candidatos retornados por `Buscar Candidatos`.
-Cadastrar decisorres encontrados;

Se o CNPJ não estiver disponível no contexto, obtenha-o pelas ferramentas do projeto antes de buscar candidatos.

## Ferramenta obrigatória

Para descobrir candidatos, use:

`Buscar Candidatos`

Entrada:

```json
{
  "cnpj": "CNPJ com 14 dígitos"
}
```

A ferramenta pode retornar até 20 candidatos com dados como:
- nome;
- LinkedIn;
- headline;
- localização;
- empresa atual informada;
- experiências atuais;
- cargo;
- descrição da experiência;
- vínculo empresarial.

Use **somente os dados efetivamente retornados pelas ferramentas** como evidência sobre a pessoa.

Não use exemplos, palavras-chave desta Skill ou conhecimento geral como se fossem fatos sobre um candidato.

Não faça pesquisa externa na web para completar o perfil, salvo se o usuário pedir explicitamente.

## Princípio central

A seleção deve responder:

> Quais são os 4 melhores profissionais deste conjunto para uma abordagem institucional/comercial do HPP?

A qualidade do candidato é definida pela combinação de:

1. vínculo corporativo atual com a empresa-alvo ou operação relacionada;
2. aderência temática ao contexto HPP;
3. capacidade de decisão, influência ou encaminhamento;
4. senioridade e alcance corporativo.

**Aderência temática pesa mais que senioridade isolada.**

Um profissional diretamente ligado a Responsabilidade Social, Investimento Social, Sustentabilidade ou Relações Institucionais pode ser melhor candidato que um executivo mais sênior sem relação clara com o tema.

---

# 1. Validar vínculo corporativo

Antes de classificar o candidato, determine se existe vínculo atual plausível.

## Vínculo direto

Considere vínculo direto quando o perfil indicar atuação atual na própria empresa-alvo.

Exemplos de evidência válida:
- `empresa_atual_informada` corresponde à empresa-alvo;
- experiência com `is_current` já filtrada pela ferramenta mostra a empresa-alvo;
- headline e experiência atual são coerentes entre si.

## Vínculo relacionado

Também pode ser válido vínculo atual com:
- holding;
- controlada;
- subsidiária;
- empresa do mesmo grupo;
- joint venture;
- operação brasileira relacionada;
- empresa prestadora com atuação explicitamente alocada dentro da empresa-alvo.

Quando o vínculo for relacionado e não direto:
- mantenha explícita a origem;
- não diga que a pessoa trabalha diretamente na empresa-alvo;
- reduza a confiança/score quando a relação for menos clara.

## Vínculo inválido

Considere inválido quando:
- a empresa-alvo aparece apenas em experiência passada;
- a pessoa atualmente trabalha em organização sem relação demonstrada;
- a menção à empresa é apenas cliente, fornecedor, projeto antigo ou referência textual;
- não existe evidência suficiente de vínculo atual ou relacionado;
- o resultado é homônimo ou claramente irrelevante.

Nunca transforme emprego antigo em vínculo atual.

---

# 2. Avaliar aderência temática

## Prioridade máxima

Áreas diretamente relacionadas ao objetivo HPP:

- responsabilidade social;
- investimento social;
- impacto social;
- sustentabilidade;
- ESG / ASG;
- cidadania corporativa;
- direitos humanos;
- relacionamento comunitário;
- projetos socioambientais;
- patrocínios;
- incentivos fiscais;
- projetos sociais;
- fundação ou instituto corporativo;
- relações institucionais;
- relações governamentais;
- public affairs;
- corporate affairs;
- relacionamento externo.

## Prioridade secundária

Áreas úteis para influência ou encaminhamento:

- comunicação corporativa;
- reputação;
- relações públicas;
- marketing institucional;
- marca corporativa;
- recursos humanos;
- People;
- cultura;
- desenvolvimento organizacional;
- experiência do empregado;
- employer branding institucional.

## Prioridade financeira/fiscal

Áreas potencialmente relevantes para viabilização técnica/fiscal:

- controladoria;
- contabilidade gerencial;
- tributário;
- fiscal;
- tax;
- planejamento tributário;
- finanças corporativas;
- FP&A;
- tesouraria estratégica;
- CFO;
- diretoria financeira;
- jurídico tributário estratégico.

---

# 3. Classificar cada candidato

Classifique cada candidato individualmente em um dos níveis abaixo.

## Nível 1 — 85 a 100 — decisor = true

Use quando há vínculo válido e aderência direta às áreas prioritárias de HPP.

Exemplos de enquadramento:
- responsabilidade social;
- investimento social;
- sustentabilidade / ESG;
- impacto social;
- cidadania;
- relações institucionais/governamentais;
- public/corporate affairs;
- relacionamento comunitário;
- patrocínios;
- incentivos fiscais;
- fundação/instituto corporativo.

A senioridade aumenta o score dentro da faixa, mas não é requisito absoluto quando a aderência temática é muito forte e o profissional demonstra capacidade de influência ou encaminhamento.

## Nível 2 — 70 a 84 — decisor = true

Use para perfis com vínculo válido e boa capacidade de influência em áreas corporativas adjacentes:

- comunicação corporativa;
- reputação;
- relações públicas;
- marketing institucional;
- marca;
- RH / People;
- cultura;
- desenvolvimento organizacional;
- employee experience;
- employer branding institucional.

## Nível 3 — 55 a 69 — decisor = true

Use para perfis com vínculo válido em áreas financeiras/fiscais relevantes:

- controladoria;
- contabilidade;
- tributário/fiscal;
- tax planning;
- corporate finance;
- FP&A;
- tesouraria estratégica;
- CFO/diretoria financeira;
- jurídico tributário estratégico.

## Fallback — 35 a 54 — decisor = false

Use para contato corporativo sênior plausível que não tenha aderência temática suficiente para os níveis 1–3, mas possa encaminhar a conversa.

Exemplos:
- CEO;
- presidente;
- sócio/fundador;
- diretor executivo;
- diretor geral;
- VP;
- COO;
- superintendente;
- secretário-geral;
- diretor comercial;
- estratégia;
- business development;
- head;
- general manager.

Fallback é contato complementar, não deve ser apresentado como decisor temático.

## Inválido — 0 a 34 — decisor = false

Use quando:
- não existe vínculo atual plausível;
- o perfil é predominantemente operacional/técnico sem relação com o objetivo;
- a evidência é insuficiente;
- o candidato é de empresa não relacionada;
- a experiência relevante é apenas histórica e não atual.

---

# 4. Como definir o score dentro da faixa

O score não deve ser arbitrário.

Considere, nesta ordem:

1. força do vínculo atual;
2. proximidade temática com HPP;
3. capacidade aparente de decisão/influência/encaminhamento;
4. senioridade e alcance corporativo;
5. qualidade e clareza da evidência disponível.

Não aumente score apenas por cargo executivo.

Não reduza um especialista tematicamente perfeito apenas porque outro perfil possui título mais sênior.

Quando houver incerteza, use a parte inferior da faixa correspondente e explicite a limitação.

---


## Consistência obrigatória entre nível e score

O score sempre deve permanecer dentro da faixa definida para o nível atribuído:

- Nível 1 → 85 a 100
- Nível 2 → 70 a 84
- Nível 3 → 55 a 69
- Fallback → 35 a 54
- Inválido → 0 a 34

Antes de finalizar a resposta, valide cada candidato.

Antes de enviar os candidatos para `Enriquecer Decisores`, valide obrigatoriamente cada candidato.

Nenhum candidato pode ser enviado para enriquecimento com combinação inconsistente entre nível e score.

Faixas obrigatórias:
- Nível 1 → 85 a 100
- Nível 2 → 70 a 84
- Nível 3 → 55 a 69
- Fallback → 35 a 54
- Inválido → 0 a 34

Se houver inconsistência, corrija o score ou reavalie o nível ANTES de chamar `Enriquecer Decisores`.

# 5. Regra obrigatória de seleção: retornar 4 candidatos

Após classificar todos os perfis, ordene-os por qualidade comercial.

Objetivo padrão: **retornar exatamente 4 candidatos**.

Ordem preferencial:

1. melhores Nível 1;
2. melhores Nível 2;
3. melhores Nível 3;
4. melhores fallbacks válidos.

Regras duras:

- Havendo pelo menos 4 candidatos plausíveis, **não retornar menos de 4**.
- Não parar após encontrar apenas 1 ou 2 candidatos excelentes.
- Complete as posições restantes com os melhores candidatos válidos das faixas seguintes.
- Nunca use candidato `Inválido` apenas para completar quantidade.
- Só retorne menos de 4 quando realmente existirem menos de 4 candidatos corporativamente plausíveis no conjunto disponível.
- Em empate, priorize: aderência temática > poder de influência > senioridade > força do vínculo relacionado.

---

# 6. Contato NÃO interfere na seleção

**E-mail ou telefone não fazem parte do critério de escolha dos 4 melhores candidatos.**

Nunca substitua um candidato melhor por um candidato pior porque:
- possui e-mail;
- possui telefone;
- foi mais fácil de enriquecer;
- outra fonte encontrou mais dados de contato.

Primeiro escolha os 4 melhores profissionais.

Somente depois faça enriquecimento de contato.

Se um dos 4 melhores não tiver e-mail ou telefone encontrado, ele **continua entre os 4 melhores candidatos**.

Nunca invente e-mail, telefone ou padrão corporativo.

---

# 7. Enriquecimento posterior

Depois de selecionar definitivamente os candidatos, use obrigatoriamente a ferramenta MCP:

`Enriquecer Decisores`

A ferramenta deve receber exatamente os candidatos selecionados nesta Skill.

Não envie candidatos descartados ou candidatos adicionais para tentar encontrar contatos melhores.

## Entrada para Enriquecer Decisores

Envie:

- `cnpj`: CNPJ da empresa-alvo;
- `razao_social`: razão social da empresa-alvo;
- `decisores`: os candidatos finais selecionados.

Para cada decisor, preserve sempre que disponível:

- `nome`;
- `cargo`;
- `link_perfil`;
- `empresa_vinculo`;
- `origem_vinculo`;
- `prioridade`;
- `score`;
- `justificativa`.

Mapeie os dados desta Skill para a ferramenta da seguinte forma:

- `nome` → nome do candidato;
- `cargo_atual` → `cargo`;
- `linkedin_url` → `link_perfil`;
- empresa evidenciada pelo vínculo → `empresa_vinculo`;
- tipo/origem do vínculo → `origem_vinculo`;
- `nivel` → `prioridade`;
- `score` → `score`;
- `motivo_selecao` → `justificativa`.

Se o candidato possuir vínculo direto com a empresa-alvo:

`origem_vinculo = "empresa"`

Se o vínculo for com holding, grupo, subsidiária ou outra organização relacionada,
mantenha essa origem explicitamente no envio.

## Regra fundamental

O enriquecimento ocorre SOMENTE depois da seleção.

Resultados do Apollo não podem alterar:

- nível;
- score;
- ranking;
- posição;
- decisão de manter o candidato entre os selecionados.

Se o Apollo não encontrar e-mail para um candidato, ele continua selecionado.

Se o Apollo retornar cargo mais genérico ou diferente, preserve separadamente:

- o cargo identificado durante a análise;
- o cargo retornado pelo Apollo.

Nunca substitua automaticamente a evidência original da seleção pelo dado enriquecido.

Se a ferramenta retornar `identidade_apollo = "divergente"`, informe a divergência e
não utilize o e-mail retornado como contato confirmado.

Se retornar `identidade_apollo = "confirmado"`, os dados de contato validados podem
ser apresentados junto ao candidato.

Nunca invente e-mail, telefone ou qualquer dado ausente.
---


# 8. Cadastro automático no Pipefy

Após concluir o enriquecimento dos decisores selecionados, use obrigatoriamente a ferramenta MCP:

`Cadastrar no Pipefy`

O cadastro no Pipefy faz parte do fluxo padrão da qualificação HPP e deve ocorrer automaticamente após a seleção e o enriquecimento dos decisores.

Não pedir confirmação adicional ao usuário.

## Fonte da qualificação

Ao cadastrar no Pipefy, preserve integralmente o resultado final anteriormente produzido pela Skill `qualificar-empresa-hpp`.

O objeto `qualificacao`:

* NÃO é o retorno bruto da ferramenta `Qualificar Empresa`;
* NÃO deve ser reconstruído nesta Skill;
* NÃO deve ter `scoring` ou `resumo_fit` recalculados;
* NÃO deve ser resumido ou renomeado;
* deve ser exatamente o resultado final da Skill `qualificar-empresa-hpp`.

A ferramenta `Qualificar Empresa` fornece fatos e evidências utilizados pela Skill de qualificação, mas seu retorno bruto não substitui a qualificação final.

## Payload para cadastro

A ferramenta `Cadastrar no Pipefy` deve receber:

* os dados da empresa consultada;
* o resultado final preservado da Skill `qualificar-empresa-hpp`;
* exatamente os decisores finais selecionados por esta Skill;
* os dados retornados por `Enriquecer Decisores`, adicionados aos respectivos decisores sem substituir os dados originais da seleção.

Envie no campo `payload_json` todo o objeto abaixo serializado como uma única string JSON válida:

```json
{
  "empresa": {
    "cnpj": "...",
    "razao_social": "...",
    "cidade": "...",
    "endereco": "..."
  },
  "qualificacao": {
    "scoring": {
      "score_final": 0,
      "classificacao": "",
      "sub_scores": {},
      "justificativa": "",
      "motivo_descarte": ""
    },
    "alertas": [],
    "resumo_fit": {
      "faturamento": "",
      "investimentos_recentes": [],
      "potencial_investimento_2025_2026": "",
      "informacoes_complementares": [],
      "justificativa_fit": ""
    },
    "contestacao": {},
    "fiscal": {},
    "setor": {},
    "incentivos": {},
    "investimento_social": {}
  },
  "decisores": [
    {
      "nome": "...",
      "cargo_atual": "...",
      "linkedin_url": "...",
      "nivel": 1,
      "score": 90,
      "decisor": true,
      "motivo_selecao": "...",
      "evidencias": [],
      "email": "...",
      "email_status": "verified",
      "identidade_apollo": "confirmado",
      "cargo_apollo": "...",
      "empresa_apollo": "...",
      "linkedin_apollo": "..."
    }
  ]
}
```

## Regras obrigatórias

* preserve `qualificacao` exatamente como produzida por `qualificar-empresa-hpp`;
* nunca substitua `qualificacao` pelo retorno bruto de `Qualificar Empresa`;
* preserve integralmente `scoring` e `resumo_fit`;
* cadastrar exatamente os decisores finais selecionados pela Skill;
* os dados do Apollo apenas enriquecem o decisor já selecionado;
* não trocar candidatos com base no resultado do Apollo;
* não alterar `nivel`, `score`, ranking ou `motivo_selecao` após o enriquecimento;
* a ausência de e-mail não impede o cadastro do decisor;
* se `identidade_apollo` não for `confirmado`, não tratar o e-mail como contato validado;
* não adicionar candidatos descartados;
* não cadastrar candidatos extras apenas porque possuem e-mail;
* não inventar dados ausentes;
* o cadastro no Pipefy deve ocorrer antes da resposta final ao usuário.

Após a execução de `Cadastrar no Pipefy`, informe o resultado do cadastro junto da resposta final.


----
# 9. Handoff para abordagem por e-mail

Depois de concluir o enriquecimento e o cadastro no Pipefy, verifique os decisores selecionados.

Se existir pelo menos um decisor com:

- `email` preenchido;
- `email_status = "verified"`;
- `identidade_apollo = "confirmado"`.

informe quais possuem e-mail verificado e ofereça o próximo passo:

> Gostaria também que eu enviasse e-mails personalizados para esses decisores?

Não envie automaticamente neste momento.

Aguarde confirmação explícita do usuário.

Se o usuário confirmar, utilize a Skill:

`abordagem-email-hpp`

A Skill `abordagem-email-hpp` é responsável por preparar e enviar os e-mails personalizados.

Não peça novamente para selecionar decisores e não repita o enriquecimento.

Use os decisores já selecionados e enriquecidos nesta Skill.

----

# 10. Saída obrigatória

Retorne os 4 selecionados em ordem de prioridade.

Para cada candidato, inclua:

```json
{
  "posicao": 1,
  "nome": "Nome",
  "linkedin_url": "URL",
  "vinculo": {
    "status": "VALIDO",
    "tipo": "DIRETO",
    "empresa_evidenciada": "Empresa"
  },
  "cargo_atual": "Cargo",
  "nivel": 1,
  "score": 95,
  "decisor": true,
  "motivo_selecao": "Justificativa curta baseada em evidências do perfil",
  "evidencias": [
    "Evidência factual retornada pela ferramenta"
  ],
  "email": "email@empresa.com.br",
  "email_status": "verified",
  "identidade_apollo": "confirmado",
  "cargo_apollo": "Cargo retornado pelo Apollo",
  "empresa_apollo": "Empresa retornada pelo Apollo",
  "linkedin_apollo": "URL retornada pelo Apollo"
}
```

Valores permitidos para `vinculo.status`:
- `VALIDO`
- `INCERTO`
- `INVALIDO`

Valores preferidos para `vinculo.tipo`:
- `DIRETO`
- `GRUPO_RELACIONADO`
- `SUBSIDIARIA_CONTROLADA`
- `PRESTADOR_ALOCADO`
- `SEM_VINCULO_ATUAL`




Não invente estrutura societária se ela não estiver evidenciada.

Depois dos 4 candidatos, apresente uma síntese curta explicando por que esse conjunto cobre melhor a abordagem HPP.

Não exponha uma longa lista de descartados, salvo se o usuário pedir.

Se algum campo de enriquecimento não for retornado pela ferramenta `Enriquecer Decisores`, use `null` e não invente valores.

Se `identidade_apollo` não for `confirmado`, não trate o e-mail retornado como contato validado.
---

# 11. Regras anti-alucinação

Nunca afirmar sem evidência retornada pela ferramenta:
- cargo;
- empregador;
- vínculo direto;
- nível hierárquico real além do que o cargo permite inferir;
- poder formal de decisão;
- departamento;
- responsabilidade;
- localização;
- tempo de empresa;
- participação em programa/projeto;
- e-mail;
- telefone.

Diferencie:
- fato retornado pela ferramenta;
- inferência de classificação desta Skill.

Exemplo correto:

> O perfil informa atuação atual como Gerente de Relacionamento Institucional na empresa. Pela aderência temática e senioridade, é classificado como Nível 1.

Exemplo incorreto:

> Ela é responsável pelos investimentos incentivados da empresa.

A segunda afirmação só pode ser feita se isso estiver explicitamente evidenciado.

---

# 12. Checklist antes de responder

Antes de finalizar, verifique:

- A ferramenta `Buscar Candidatos` foi usada?
- Todos os candidatos relevantes foram avaliados antes da seleção?
- Os 4 selecionados possuem vínculo atual plausível?
- Nenhum emprego antigo foi tratado como atual?
- Perfis de grupo/subsidiária/prestador foram identificados como tal?
- Aderência temática teve mais peso que senioridade isolada?
- Foram retornados 4 candidatos quando havia pelo menos 4 plausíveis?
- Nenhum inválido foi usado apenas para completar 4?
- Disponibilidade de e-mail/telefone não alterou a seleção?
- Nenhum dado ausente foi inventado?
- As justificativas estão baseadas em evidências retornadas pela ferramenta?
- `Enriquecer Decisores` foi executado para os candidatos finais?
- O resultado do Apollo preservou nível, score e ranking?
- `Cadastrar no Pipefy` foi executado após o enriquecimento?
- Foram enviados ao Pipefy exatamente os decisores finais selecionados?

Se qualquer resposta for não, corrija antes de finalizar.
