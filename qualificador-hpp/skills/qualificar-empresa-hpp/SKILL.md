---
name: qualificar-empresa-hpp
description: Use when the user wants HPP eligibility interpretation, ICP score, commercial priority, fiscal-incentive history, FIA potential, social fit, alerts, review guidance, or a commercial approach for a company.
---

# Qualificar Empresa HPP

## Objetivo

Substituir a camada antiga de agente de **SCORE ICP + Qualificação comercial** usando as ferramentas MCP do HPP.

A ferramenta **Qualificar Empresa** produz os fatos, decisões fiscais, filtros determinísticos e enriquecimentos necessários. Esta Skill interpreta esse retorno, calcula prioridade comercial, score ICP, classificação, alertas, contestação e argumento comercial.

A Skill **não refaz a elegibilidade fiscal**.

## Ferramentas MCP

Ferramentas relevantes:

- `Consultar Empresa`
- `Qualificar Empresa`

### Ordem padrão

Quando houver um CNPJ e a empresa ainda não tiver sido consultada na conversa:

1. chame `Consultar Empresa`;
2. chame `Qualificar Empresa`;
3. interprete o resultado;
4. calcule o score ICP apenas quando a empresa estiver fiscalmente elegível.

Se `Consultar Empresa` já tiver sido executada para o mesmo CNPJ na conversa atual, vá diretamente para `Qualificar Empresa`.

Não faça pesquisa externa adicional por conta própria. O enriquecimento social fornecido pela Tool 2 já faz parte do dado recebido. Só pesquise fora das ferramentas se o usuário pedir explicitamente.

---

# 1. AUTORIDADE DOS DADOS

Considere o retorno de `Qualificar Empresa` como a fonte de verdade para:

- `fiscal.status`;
- `fiscal.regime`;
- `fiscal.lucro_real`;
- `fiscal.motivo`;
- `fiscal.fonte`;
- `fiscal.indicios`;
- elegibilidade setorial/CNAE;
- histórico de incentivos;
- potencial FIA calculado;
- investimento social e fit retornados;
- evidências e fontes coletadas pelo workflow.

Nunca substitua essas decisões por inferências próprias.

---

# 2. ELEGIBILIDADE X PRIORIDADE

Elegibilidade fiscal e prioridade comercial são conceitos diferentes.

## `NAO_ELEGIVEL`

Se a ferramenta retornar status fiscal explicitamente não elegível, ou outra inelegibilidade explícita do backend:

- não tente recuperar o lead via score;
- `score_final = 0`;
- classificação: `D — Desqualificado`;
- explique o motivo produzido pela ferramenta;
- não use contestação comercial para revisar a elegibilidade.

## `INDETERMINADA`

Se a ferramenta retornar status fiscal indeterminado:

- não trate a empresa como elegível;
- não produza score comercial definitivo;
- informe `REVISÃO FISCAL NECESSÁRIA`;
- explique objetivamente qual evidência fiscal está faltando ou conflitando;
- não inferira Lucro Real por faturamento, porte ou CNAE.

## `ELEGIVEL`

Se a ferramenta retornar elegível:

- aceite a decisão;
- calcule prioridade comercial e score ICP;
- não refaça a decisão fiscal.

---

# 3. REGRA DE FATURAMENTO ATUAL DO HPP

A regra vigente é:

**faturamento abaixo de R$ 78 milhões não desqualifica automaticamente a empresa.**

O faturamento é critério de priorização.

- >= R$ 78 milhões: recebe ponto de potencial;
- >= R$ 500 milhões: recebe ponto adicional de potencial.

Nunca utilize esses limites para provar Lucro Real.

---

# 4. REGRAS FISCAIS ABSOLUTAS

Nunca determine Lucro Real apenas por:

- faturamento;
- porte;
- CNAE;
- natureza jurídica;
- funcionários;
- capital social.

Nunca presuma lucro tributável apenas porque a empresa está em Lucro Real.

Se `fiscal.fonte = TESTE_MANUAL` ou outro marcador de mock/teste:

- deixe explícito que a elegibilidade fiscal está sendo simulada/testada;
- não apresente a conclusão como confirmação de produção.

`fiscal.indicios` são contexto e nunca substituem a evidência fiscal principal.

---

# 5. CONTEXTO HPP

O HPP trabalha principalmente com:

- FIA — Fundo da Infância e do Adolescente;
- Lei Rouanet / SALIC.

FIA é o principal instrumento de captação.

Histórico Rouanet/SALIC possui aderência direta ao HPP, não apenas valor de proxy.

Histórico em outros mecanismos pode demonstrar familiaridade com incentivos fiscais, mas possui aderência diferente.

---

# 6. SCORE ICP

Calcule:

- `s_potencial` de 0 a 3;
- `s_historico` de 0 a 3;
- `s_fit` de 0 a 3;
- `s_local` de 0 a 1;
- `s_web` de 0 a 1.

Depois:

`score_bruto = s_potencial + s_historico + s_fit + s_local + s_web`

`score_final = min(10, score_bruto)`

Nunca ajuste manualmente o score para encaixar uma empresa em uma classificação desejada.

## Classificação

Para empresas elegíveis:

- 1–4 → `C — Baixa prioridade`
- 5–7 → `B — Média prioridade`
- 8–10 → `A — Alta prioridade`

`D — Desqualificado` é reservado a inelegibilidade explícita produzida pela Tool 2 ou a contradição inequívoca de dados que torne a empresa inelegível.

---

# 7. s_potencial — 0 a 3

Some:

- +1 se faturamento declarado/estimado explicitamente no retorno >= R$ 78M;
- +1 se faturamento >= R$ 500M;
- +1 se `potencial_fia_estimado >= R$ 50K` OU histórico fiscal confirmado relevante > R$ 200K.

Máximo: 3.

Não invente faturamento ausente.

Prefira os valores de potencial FIA já calculados pela Tool 2.

---

# 8. s_historico — 0 a 3

Some:

- +1 se houver qualquer histórico fiscal relevante;
- +1 se o total incentivado via FIA ou Rouanet/SALIC for superior a R$ 200K;
- +1 se houver FIA ou Rouanet a partir de 2020, OU histórico FIA/Rouanet anterior a 2020 que represente oportunidade de reengajamento.

Máximo: 3.

Histórico antigo continua válido e não deve ser ignorado.

---

# 9. s_fit — 0 a 3

Some:

- +1 se a empresa estiver fora da lista negativa;
- +1 se houver histórico FIA ou Rouanet/SALIC em qualquer período;
- +1 se houver pelo menos uma destas condições:
  - agenda ESG estruturada;
  - agenda ODS publicada;
  - programa social estruturado;
  - FIA ou Rouanet a partir de 2020.

Máximo: 3.

Histórico exclusivamente em Lei do Esporte ou Fundo do Idoso não recebe o ponto de FIA/Rouanet, salvo outra evidência válida.

Não aplique pontuação negativa.

---

# 10. s_local — 0 a 1

Some +1 se a sede da empresa estiver em uma das UFs prioritárias atuais:

- PR
- RJ
- RS
- SC
- GO
- DF
- MG
- MT

Demais UFs: 0.

SP não está na lista prioritária atual.

Nunca invente a UF.

---

# 11. s_web — 0 a 1

Use apenas as evidências de investimento social retornadas pela ferramenta.

Some +1 quando houver evidência suficiente de:

- programa social;
- investimento social;
- ESG;
- agenda ODS;
- projetos comunitários;
- causa alinhada ao HPP.

Se o campo estiver vazio ou sem evidência suficiente: 0.

Não faça busca web independente para preencher esse ponto, salvo pedido explícito do usuário.

---

# 12. FIT INSTITUCIONAL

## Fit alto

Considere forte aderência quando houver:

- FIA a partir de 2020;
- Rouanet/SALIC a partir de 2020;
- projetos ligados a infância, criança ou adolescente;
- saúde infantil/pediatria;
- combinação FIA + Rouanet.

## Fit médio-alto

Considere quando houver:

- FIA anterior a 2020;
- Rouanet anterior a 2020;
- histórico de utilização sem registros recentes.

Isso representa oportunidade de reengajamento, não ausência de fit.

## Fit médio

Outros mecanismos de incentivo relevantes, sem FIA/Rouanet, como:

- Audiovisual;
- PRONON;
- PRONAS;
- outros mecanismos de renúncia.

## Fit baixo

Histórico exclusivamente em:

- Lei do Esporte;
- Fundo do Idoso/DOSO.

Existe familiaridade fiscal, mas menor aderência direta.

## Histórico misto

Sempre considere o instrumento de maior aderência.

FIA + Esporte, por exemplo, mantém o fit proporcionado pelo FIA.

---

# 13. POTENCIAL FIA

Prefira sempre os campos estruturados retornados pela Tool 2:

- `potencial_fia_estimado`;
- `potencial_fia_maximo_historico`;
- `potencial_fia_medio`;
- `espaco_fiscal_fia_estimado`;
- `confiabilidade`;
- `tendencia`.

Esses valores são **estimativas comerciais**, não saldo fiscal confirmado.

Nunca diga:

- "R$ X disponíveis";
- "saldo comprovado";
- "valor garantido";
- "a empresa pode doar exatamente R$ X".

Prefira:

- "potencial FIA estimado de R$ X";
- "referência comercial de potencial FIA";
- "estimativa baseada no histórico de incentivos".

Se a Tool 2 não fornecer potencial e houver dados suficientes, a referência de fallback é:

1. histórico FIA direto;
2. 25% do histórico Rouanet/SALIC;
3. na ausência de histórico utilizável, 1% do faturamento explicitamente informado.

Nunca calcule a partir de capital social, funcionários, porte ou notícias.

---

# 14. ALERTAS

Inclua somente alertas aplicáveis.

Valores previstos:

- `sem_dados_faturamento`
- `sem_lucro_provavel`
- `historico_desatualizado`
- `icebreaker_forte_fia`
- `sem_historico_fiscal`
- `sem_sinais_web`
- `fit_premium`
- `setor_lista_negativa`
- `fit_divergente`
- `reengajamento_possivel`

## Regras principais

### `sem_dados_faturamento`
Faturamento ausente ou não confiável.

### `sem_lucro_provavel`
Grande porte/faturamento alto, mas nenhuma evidência financeira suficiente de lucro tributável.

Esse alerta nunca altera elegibilidade.

### `historico_desatualizado`
FIA/Rouanet existente, mas registro mais recente anterior a 2020.

### `icebreaker_forte_fia`
Há histórico FIA direto.

### `sem_historico_fiscal`
Nenhum incentivo fiscal relevante identificado.

### `sem_sinais_web`
Nenhum sinal social/ESG suficiente retornado.

### `fit_premium`
Evidência especialmente aderente: infância, primeira infância, pediatria, saúde infantil ou cultura aderente.

### `setor_lista_negativa`
Somente se a Tool 2 trouxer setor explicitamente negativo. Nesse caso, tratar como inconsistência/inelegibilidade.

### `fit_divergente`
Histórico fiscal exclusivamente em instrumentos de menor aderência, especialmente Esporte ou Fundo do Idoso.

### `reengajamento_possivel`
FIA/Rouanet anterior a 2020 sem registros recentes.

---

# 15. CONTESTAÇÃO / REVISÃO HUMANA

Contestação trata apenas de **prioridade comercial**.

Nunca revisa:

- Lucro Real;
- regime tributário;
- elegibilidade fiscal;
- CNAE negativo definido pelo backend.

Sempre produza:

- `faz_sentido_revisar`;
- `ponto_a_validar`;
- `justificativa`.

## Score >= 5

Obrigatoriamente:

- `faz_sentido_revisar = false`
- `ponto_a_validar = "nenhum"`

## Score < 5

Só marque revisão quando existir **uma informação objetiva ausente ou inconclusiva** que, se confirmada, possa elevar o score para 5 ou mais.

Exemplos válidos:

- validar faturamento anual atualizado;
- verificar aportes FIA/Rouanet recentes;
- confirmar programa estruturado ESG/investimento social.

Score 4 sozinho não justifica revisão.

Se nenhuma lacuna concreta puder elevar a empresa ao limiar:

- `faz_sentido_revisar = false`
- `ponto_a_validar = "nenhum"`

Não crie contestação artificial para salvar lead fraco.

---

# 16. EVIDÊNCIAS E NÃO-ALUCINAÇÃO

Use exclusivamente as informações devolvidas pelas ferramentas para a análise principal.

Nunca invente:

- projeto;
- valor;
- ano;
- instrumento fiscal;
- programa social;
- causa;
- fonte;
- decisor;
- evidência ESG.

Não complemente automaticamente com conhecimento próprio.

Se o usuário pedir pesquisa externa, separe claramente:

- dados do workflow/MCP;
- informações adicionais pesquisadas externamente.


## Regra crítica: critérios não são evidências

Os exemplos, critérios, palavras-chave e categorias descritos nesta Skill
servem apenas para CLASSIFICAR evidências recebidas pelas ferramentas.

Eles nunca constituem evidência sobre uma empresa.

Por exemplo, a presença de termos como:

- infância;
- primeira infância;
- pediatria;
- saúde infantil;
- ESG;
- ODS;
- instituto empresarial;

nas regras desta Skill NÃO autoriza afirmar que a empresa possui essas
características.

Só atribua uma característica, programa, compromisso, pacto, projeto ou
causa à empresa quando essa informação estiver explicitamente presente
no retorno das ferramentas MCP.

Nunca transforme um critério de score em fato sobre a empresa.

---

# 17. ARGUMENTO COMERCIAL

Gere um argumento curto e baseado nas evidências.

Priorize, nesta ordem:

1. mecanismo já utilizado pela empresa;
2. aderência com FIA/Rouanet;
3. potencial FIA estimado;
4. causa social alinhada;
5. agenda ESG/ODS;
6. oportunidade de reengajamento, quando aplicável.

Nunca prometa economia, disponibilidade fiscal ou doação garantida.

Exemplo de formulação correta:

"A empresa já utiliza mecanismos de incentivo e apresenta potencial FIA estimado relevante. O histórico e a agenda social indicam aderência à causa do HPP, criando uma oportunidade concreta de abordagem."

---

# 18. FORMATO PADRÃO DA RESPOSTA

Quando a empresa estiver elegível, apresente:

## Empresa
Razão social e CNPJ.

## Elegibilidade
Status fiscal, regime e fonte.

Se a fonte for de teste, declare isso.

## Score ICP
- `s_potencial`
- `s_historico`
- `s_fit`
- `s_local`
- `s_web`
- `score_final`
- classificação

Explique cada ponto concedido de forma curta e rastreável às evidências.

## Histórico de incentivos
Resumo dos mecanismos e anos mais relevantes.

## Potencial FIA
Valor estimado, tendência e confiabilidade.

Sempre rotule como estimativa.

## Fit HPP
Nível de aderência e justificativa.

## Alertas
Somente os aplicáveis.

## Contestação
- faz sentido revisar?
- ponto a validar;
- justificativa.

## Argumento comercial
Uma sugestão curta e utilizável pelo time comercial.

---

# 19. CADASTRO NO PIPEFY

Quando o usuário solicitar o cadastro da empresa no Pipefy após a qualificação,
use a ferramenta `Cadastrar no Pipefy`.

Antes de chamar a ferramenta, materialize o resultado desta Skill no objeto
`qualificacao`.

NUNCA envie somente `qualification_status`, `fiscal`, `setor`,
`incentivos` ou `investimento_social`.

O objeto `qualificacao` enviado para `Cadastrar no Pipefy` deve conter:

```json
{
  "scoring": {
    "score_final": 0,
    "classificacao": "",
    "sub_scores": {
      "s_potencial": 0,
      "s_historico": 0,
      "s_fit": 0,
      "s_local": 0,
      "s_web": 0
    },
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

  "contestacao": {
    "faz_sentido_revisar": false,
    "justificativa": "",
    "ponto_a_validar": "nenhum"
  }
}
```

Preserve também, quando disponíveis, os dados objetivos retornados pela
ferramenta `Qualificar Empresa`, como `fiscal`, `setor`, `incentivos`
e `investimento_social`.

Não resuma, omita ou renomeie `scoring` e `resumo_fit` antes de chamar
`Cadastrar no Pipefy`.

`score_final` e `classificacao` enviados ao Pipefy devem ser exatamente
os valores calculados por esta Skill.

`investimentos_recentes` deve ser construído exclusivamente a partir de
`incentivos.historico_incentivos` retornado pela ferramenta `Qualificar Empresa`.

Siga a mesma regra do workflow original:

* priorize os investimentos via incentivos fiscais dos últimos cinco anos;
* se não houver registros nesse período, utilize os registros mais recentes disponíveis;
* nunca invente projeto, valor, ano ou instrumento;
* nunca crie registros placeholder apenas para preencher quantidade;
* se não houver histórico fiscal válido, envie `investimentos_recentes: []`.

Cada registro deve usar o formato:

```json
{
  "nome_projeto_fundo": "",
  "instrumento": "",
  "valor": "",
  "ano": 0
}
```

Mapeamento:

* `beneficio` → `nome_projeto_fundo`;
* `valor` → `valor`, formatado em reais quando houver valor;
* `ano` → `ano`;
* determine `instrumento` somente a partir das evidências disponíveis em `beneficio`, `tributo`, `tipo_renuncia` ou `base_legal`.

Quando o mecanismo puder ser identificado diretamente, use a classificação correspondente, como:

* `FIA`;
* `SALIC/Rouanet`;
* `Lei do Esporte`;
* `DOSO`;
* `PRONON`;
* `PRONAS`.

Quando houver incentivo fiscal identificado, mas não for possível enquadrá-lo em um desses instrumentos específicos, use:

`outro`

Nunca invente um instrumento específico.

Preserve em `qualificacao.incentivos`, sem recalcular ou alterar, os valores retornados pela ferramenta `Qualificar Empresa`, incluindo:

* `potencial_fia_estimado`;
* `potencial_cultura_estimado`;
* `potencial_fia_maximo_historico`;
* `potencial_fia_medio`;
* `espaco_fiscal_fia_estimado`;
* `tendencia`;
* `confiabilidade`;
* `historico_relevante`;
* `historico_incentivos`;
* `briefing`.

Os campos específicos do Pipefy:

* `Potencial anual de doação FIA (0,9%)`;
* `Potencial anual de doação Cultura (3,6%)`;

devem receber, respectivamente:

* `qualificacao.incentivos.potencial_fia_estimado`;
* `qualificacao.incentivos.potencial_cultura_estimado`.

Nunca recalcule esses valores durante o cadastro no Pipefy.


# 20. VALIDAÇÃO FINAL

Antes de responder, confira:

1. A decisão fiscal foi respeitada?
2. O regime tributário não foi inferido pelo faturamento?
3. Faturamento < R$ 78M não foi usado para desqualificar?
4. O score foi calculado exatamente pela soma dos sub-scores e limitado a 10?
5. A classificação corresponde ao score?
6. D foi reservado à inelegibilidade explícita?
7. Potencial FIA foi descrito como estimativa?
8. Nenhum fato externo foi acrescentado?
9. A contestação não tentou revisar elegibilidade?
10. `TESTE_MANUAL`, quando presente, foi identificado como teste?

Se qualquer item falhar, corrija antes de responder.
