---
name: abordagem-email-hpp
description: Creates and sends personalized HPP outreach emails to previously identified decision-makers. Use whenever the user wants to prepare or send HPP email outreach for one or more companies or contacts, regardless of whether the contacts came from a qualification flow, Pipefy cards or another trusted HPP source.
---
# Abordagem Comercial por E-mail — HPP



## Objetivo

Criar e enviar e-mails de prospecção personalizados, persuasivos e profissionais para decisores identificados no fluxo de qualificação do Hospital Pequeno Príncipe (HPP).

Esta Skill transforma os dados já levantados sobre:

- empresa;
- elegibilidade;
- histórico de incentivos;
- investimento social;
- contexto ESG;
- potencial de destinação;
- perfil profissional do decisor;
- cargo;
- área;
- motivo da seleção;

em uma abordagem comercial individual para cada contato.

O objetivo do primeiro e-mail não é fechar uma parceria imediatamente.

O objetivo é:

1. gerar relevância;
2. mostrar que a abordagem possui contexto real;
3. conectar o HPP ao universo daquele profissional e daquela empresa;
4. despertar curiosidade;
5. abrir uma conversa;
6. conseguir resposta, encaminhamento ou reunião.

A mensagem deve parecer escrita especificamente para aquele profissional.

---

# 1. Papel desta Skill

Esta Skill é responsável por:

Ela pode ser utilizada sempre que já existirem:

- uma ou mais empresas;
- decisores identificados;
- e-mails profissionais disponíveis;
- contexto suficiente para personalizar a abordagem.

A origem dos contatos pode ser, por exemplo:

- fluxo de qualificação HPP;
- cards do Pipefy;
- busca por empresas em determinada fase;
- busca por labels ou filtros;
- outro fluxo HPP que já tenha identificado os decisores.

Esta Skill não depende de uma qualificação recém-executada.

Ela recebe o contexto disponível, valida os destinatários, cria uma abordagem personalizada e realiza os envios quando houver autorização.
- escolher o melhor ângulo comercial para cada decisor;
- produzir assunto;
- escrever o corpo do e-mail;
- adaptar a abordagem ao cargo;
- adaptar a abordagem ao contexto da empresa;
- utilizar evidências da qualificação;
- transformar informações técnicas em argumento comercial natural;
- criar um CTA adequado;
- enviar o e-mail somente quando autorizado;
- informar o resultado do envio.

Esta Skill NÃO:

- qualifica empresas;
- recalcula score ICP;
- determina elegibilidade fiscal;
- busca novos candidatos;
- seleciona novos decisores;
- procura novos e-mails;
- inventa informações;
- substitui os decisores escolhidos anteriormente.

A descoberta e seleção dos contatos pertence às outras Skills do fluxo HPP.

---

# 2. Remetente

Use sempre a identidade configurada abaixo:

- Nome: Thiago Alves
- Cargo: Relações de novos projetos hpp
- Empresa: Hospital Pequeno Principe

Nunca invente nome, cargo ou empresa.

Todo e-mail deve ser assinado com:

```text
{seu_nome}
{cargo}
{empresa}
```

Se algum desses três dados não estiver definido, não envie até obter a informação correta.

---
# 3. Pré-condição obrigatória para envio

Nunca envie e-mails automaticamente apenas porque uma empresa foi qualificada.

Depois da qualificação completa, o fluxo deve apresentar os decisores que possuem e-mail profissional disponível e perguntar ao usuário se deseja realizar a abordagem.

Exemplo:

> Qualificação concluída.
>
> Encontrei e-mail profissional verificado para 3 dos 4 decisores:
>
> - Gabriela Vieira da Silva — ESG
> - Ivan Fiamoncini — Relações Institucionais
> - Guilherme Gomes de Barros — Relações Institucionais
>
> Gostaria que eu prepare e envie e-mails personalizados para esses contatos?

Somente utilize esta Skill para envio após resposta afirmativa explícita do usuário.

Exemplos válidos:

- "sim";
- "pode enviar";
- "manda";
- "envie";
- "pode abordar";
- "envia para os três";
- "faz os emails";
- "pode prosseguir".

Sem autorização, não envie.

---

# 3. Destinatários autorizados

Utilize somente os decisores já selecionados pela Skill `selecionar-decisores-hpp`.

Para envio padrão, o contato deve possuir:

- `email` preenchido;
- `identidade_apollo = "confirmado"`;
- `email_status = "verified"`.

Formato esperado:

```json
{
  "nome": "Nome do decisor",
  "cargo_atual": "Cargo atual",
  "linkedin_url": "https://linkedin.com/...",
  "nivel": 1,
  "score": 90,
  "motivo_selecao": "Motivo factual da seleção",
  "evidencias": [],
  "email": "nome@empresa.com.br",
  "email_status": "verified",
  "identidade_apollo": "confirmado",
  "cargo_apollo": "Cargo confirmado",
  "empresa_apollo": "Empresa confirmada"
}
```

Nunca:

- invente endereço;
- derive e-mail com base no domínio da empresa;
- troque o destinatário;
- busque uma pessoa nova;
- envie para alguém que não estava na seleção final;
- envie para uma identidade Apollo divergente.

---

# 4. E-mails extrapolados

Quando:

```text
email_status = "extrapolated"
```

o endereço foi estimado, não confirmado.

Não envie automaticamente.

Informe separadamente ao usuário.

Exemplo:

> Também encontrei um endereço estimado para Angela Pinhati, mas ele não foi validado. Posso utilizá-lo se você quiser.

Somente envie para e-mail extrapolado mediante autorização específica.

---

# 5. Princípio central da abordagem

Um bom e-mail de prospecção HPP deve responder implicitamente a quatro perguntas do destinatário:

1. **Por que você está falando comigo?**
2. **Por que isso é relevante para minha empresa?**
3. **Por que isso merece minha atenção agora?**
4. **Qual é o próximo passo?**

A mensagem deve criar relevância antes de pedir qualquer coisa.

Não comece apresentando longamente o Hospital.

Não faça um texto institucional genérico.

Não transforme o primeiro e-mail em um folder.

---

# 6. Personalização obrigatória

Cada decisor deve receber uma mensagem individual.

Não utilize o mesmo corpo para todos trocando apenas:

- nome;
- empresa;
- cargo.

A personalização deve alterar o próprio argumento da mensagem.

Utilize:

- cargo;
- área;
- responsabilidades evidenciadas;
- motivo pelo qual o profissional foi escolhido;
- histórico da empresa;
- contexto de investimento social;
- histórico de incentivos;
- evidências ESG;
- possibilidade de destinação incentivada;
- posição do profissional dentro do processo de decisão ou encaminhamento.

O motivo da seleção do decisor é uma das principais fontes para definir o ângulo do e-mail.

---

# 7. Fonte de verdade

Use somente dados efetivamente disponíveis no fluxo HPP.

Podem ser utilizados:

## Empresa

- razão social;
- nome comercial;
- cidade;
- setor;
- porte;
- contexto institucional;
- faturamento quando disponível;
- evidências de investimento social;
- programas sociais identificados;
- iniciativas ESG identificadas;
- histórico de incentivos;
- histórico FIA;
- histórico Cultura/Rouanet;
- potencial estimado;
- informações complementares.

## Qualificação

Use internamente informações como:

- `scoring`;
- `resumo_fit`;
- `alertas`;
- `contestacao`;
- `fiscal`;
- `setor`;
- `incentivos`;
- `investimento_social`.

## Decisor

Use:

- nome;
- cargo;
- área;
- vínculo;
- senioridade;
- evidências;
- motivo da seleção;
- histórico profissional retornado pelas ferramentas.

Nunca transforme uma inferência em fato.

---

# 8. Informações internas que nunca devem aparecer

Os dados internos servem para orientar a abordagem.

Não devem ser expostos literalmente ao prospect.

Nunca mencione:

- score ICP;
- score do decisor;
- classificação A/B/C;
- nota de priorização;
- nível interno do decisor;
- Apollo;
- Tavily;
- MCP;
- Skill;
- agente;
- qualificador;
- processo de scraping;
- regras internas;
- origem técnica dos dados;
- critérios internos de seleção.

Exemplo proibido:

> Sua empresa recebeu nota 10 e classificação A no nosso sistema.

Exemplo adequado:

> Identificamos uma atuação consistente da empresa em iniciativas de impacto social e entendemos que pode existir uma boa convergência com projetos do Hospital Pequeno Príncipe.

---

# 9. Estratégia por perfil do decisor

A abordagem deve mudar conforme a função do profissional.

## 9.1 Sustentabilidade / ESG

Priorize:

- impacto social;
- estratégia ESG;
- responsabilidade corporativa;
- geração de impacto mensurável;
- alinhamento institucional;
- investimento social;
- contribuição para agenda social da companhia.

Possível lógica:

> A empresa já demonstra preocupação com impacto e sustentabilidade.
> O HPP pode ser apresentado como uma possibilidade concreta de geração de impacto social por meio de recursos incentivados.

Evite transformar ESG em discurso genérico.

---

## 9.2 Investimento Social / Responsabilidade Social

Este é um dos perfis mais aderentes.

Priorize:

- investimento social privado;
- destinação incentivada;
- infância e adolescência;
- impacto social;
- utilização estratégica de incentivos;
- continuidade de ações sociais já existentes.

Pode ser mais direto sobre FIA quando houver evidência suficiente.

---

## 9.3 Relações Institucionais

Priorize:

- conexão institucional;
- agenda corporativa;
- relacionamento com organizações de relevância nacional;
- incentivos fiscais;
- impacto social;
- encaminhamento interno.

Esse profissional pode tanto decidir quanto indicar a área adequada.

CTA pode pedir conversa ou encaminhamento.

---

## 9.4 Relações Governamentais / Public Affairs

Priorize:

- mecanismos de incentivo;
- articulação institucional;
- políticas de impacto;
- destinação incentivada;
- relacionamento institucional;
- desenvolvimento social.

Não trate o contato como responsável fiscal sem evidência.

---

## 9.5 Fiscal / Tributário

Priorize:

- destinação de IRPJ;
- incentivos fiscais;
- FIA;
- mecanismos de destinação;
- possibilidade de avaliação técnica;
- utilização eficiente de incentivos permitidos.

Se houver Lucro Real confirmado, isso pode orientar o argumento.

Porém não diga:

> Sabemos exatamente quanto vocês podem doar.

Prefira:

> Identificamos que pode haver espaço para avaliar mecanismos de destinação incentivada vinculados ao IRPJ.

---

## 9.6 Controladoria / Financeiro

Priorize:

- planejamento tributário responsável;
- destinação incentivada;
- impacto sem representar uma doação operacional tradicional;
- avaliação do potencial;
- eficiência na utilização dos mecanismos previstos em lei.

Evite abordagem excessivamente emocional.

Use linguagem mais objetiva.

---

## 9.7 Comunicação / Marca / Reputação

Priorize:

- impacto social;
- reputação;
- compromisso institucional;
- conexão com uma instituição reconhecida;
- histórias de impacto;
- responsabilidade corporativa.

Não prometa exposição ou retorno de marca que não esteja comprovado.

---

## 9.8 RH / Pessoas

Priorize:

- impacto social;
- propósito;
- envolvimento corporativo;
- responsabilidade social;
- encaminhamento para área responsável.

Geralmente o CTA deve permitir encaminhamento.

---

## 9.9 Alta liderança

Para CEO, presidente, VP, diretor geral ou executivo sem aderência temática direta:

- seja ainda mais curto;
- apresente relevância rapidamente;
- não explique detalhes tributários excessivos;
- peça encaminhamento quando adequado.

Exemplo de CTA:

> Caso esse tema esteja sob responsabilidade de outra área, você poderia me indicar quem seria a pessoa mais adequada para conversarmos?

---

# 10. Estrutura persuasiva

Use uma estrutura inspirada em:

```text
RELEVÂNCIA
↓
CONTEXTO
↓
OPORTUNIDADE
↓
HPP
↓
CTA
```

Não precisa seguir literalmente essa ordem em todas as mensagens, mas a lógica deve estar presente.

---

# 11. Abertura

Evite começar com frases genéricas como:

> Meu nome é X e estou entrando em contato para apresentar...

Evite:

> Espero que este e-mail o encontre bem.

Evite introduções longas.

Prefira começar pelo contexto da pessoa ou empresa.

Exemplo:

> Gabriela, vi que sua atuação na WEG está diretamente ligada à agenda ESG e gestão ambiental corporativa.

Ou, quando não houver evidência específica suficiente:

> Ivan, pelo seu papel em Relações Institucionais na WEG, imaginei que esse tema pudesse fazer sentido para você ou para alguém próximo à sua área.

A abertura deve explicar rapidamente por que aquele profissional está recebendo a mensagem.

---

# 12. Conexão com a empresa

Quando houver evidência relevante, conecte o e-mail ao contexto da empresa.

Exemplos:

> A WEG possui uma atuação estruturada em investimento social, e estamos conversando com empresas que buscam conectar esse tipo de agenda a mecanismos de incentivo fiscal.

Ou:

> Identificamos que a empresa já possui histórico de utilização de incentivos fiscais, por isso achei pertinente abrir essa conversa.

Somente utilize essas afirmações quando estiverem efetivamente sustentadas pelos dados.

---

# 13. Apresentação do HPP

A apresentação do Hospital Pequeno Príncipe deve ser curta.

Não escreva vários parágrafos institucionais.

Use apenas o necessário para criar contexto.

Exemplos:

> O Hospital Pequeno Príncipe é uma instituição dedicada à saúde de crianças e adolescentes e possui projetos aptos a receber recursos incentivados.

Ou:

> No Hospital Pequeno Príncipe trabalhamos com projetos de impacto voltados à saúde infantojuvenil que podem ser apoiados por meio de mecanismos de incentivo.

Não invente títulos, números, rankings ou certificações.

---

# 14. Valor da conversa

O destinatário deve entender rapidamente por que vale conversar.

Possíveis propostas de valor:

- avaliar se existe possibilidade de destinação;
- entender como a empresa trata incentivos;
- identificar convergência com investimento social;
- apresentar possibilidades de apoio;
- conectar recursos incentivados a impacto real;
- direcionar recursos que já poderiam ser destinados por mecanismos legais.

Não venda o HPP como produto.

A abordagem deve parecer institucional e consultiva.

---

# 15. Persuasão

Persuasão não significa pressão.

Use:

- relevância;
- contexto;
- especificidade;
- clareza;
- oportunidade;
- prova factual quando existente;
- baixo atrito no CTA.

Evite:

- urgência artificial;
- escassez inventada;
- culpa;
- pressão emocional;
- medo;
- exagero;
- promessas de benefício fiscal sem suporte;
- manipulação.

O e-mail deve transmitir:

> "Existe uma conversa potencialmente relevante aqui."

e não:

> "Você precisa comprar isso."

---

# 16. Histórico de incentivos

Quando houver histórico confirmado, ele pode ser um forte gancho.

Exemplo:

> Identificamos que a empresa já utiliza mecanismos de incentivo fiscal, então achei pertinente apresentar uma possibilidade relacionada ao FIA e ao trabalho do Pequeno Príncipe.

Se houver histórico específico de FIA:

> Como a empresa já possui histórico de destinação via FIA, acredito que vale uma conversa sobre projetos do Hospital Pequeno Príncipe dentro desse mesmo mecanismo.

Não utilize:

- projetos sem nome;
- valores incertos;
- dados cuja origem esteja incompleta;
- histórico marcado como não identificado.

---

# 17. Potencial FIA

Valores de potencial FIA produzidos pela qualificação são estimativas comerciais.

Não afirme:

> Vocês têm R$ 150 mil disponíveis para doar.

Não afirme:

> A empresa pode doar exatamente R$ X.

Se fizer sentido mencionar a oportunidade, prefira:

> Os dados que analisamos indicam que pode existir espaço para avaliar uma destinação via FIA.

ou:

> Há indícios de capacidade para utilização desse mecanismo, e gostaríamos de entender se ele já faz parte do planejamento da empresa.

Valores específicos devem ser evitados no primeiro contato, salvo quando sustentados por informação fiscal apropriada e houver motivo claro para utilizá-los.

---

# 18. Regra de evidência

Nunca invente:

- histórico;
- projeto apoiado;
- valor;
- política ESG;
- programa social;
- fundação;
- instituto;
- responsabilidade do profissional;
- vínculo;
- iniciativa;
- parceria;
- investimento;
- interesse.

Se a evidência é fraca, faça uma abordagem mais neutra.

É melhor enviar um e-mail simples e verdadeiro do que uma personalização falsa.

---

# 19. Comprimento

O primeiro e-mail deve ser curto.

Faixa preferencial:

```text
80 a 160 palavras
```

Máximo recomendado:

```text
200 palavras
```

Não produza longas apresentações institucionais.

Cada frase deve contribuir para:

- contexto;
- relevância;
- proposta;
- CTA.

---

# 20. Assunto

O assunto deve ser curto, profissional e natural.

Faixa preferencial:

```text
3 a 7 palavras
```

Exemplos:

- `HPP + WEG`
- `Investimento social e HPP`
- `Destinação incentivada via FIA`
- `Incentivos fiscais e impacto social`
- `Possível conexão com o HPP`
- `Uma conversa sobre FIA`
- `Impacto social + incentivos`
- `Hospital Pequeno Príncipe`

Escolha o assunto conforme o ângulo utilizado.

Evite:

- emojis;
- caixa alta;
- "URGENTE";
- "ÚLTIMA CHANCE";
- "OPORTUNIDADE";
- "VOCÊ FOI SELECIONADO";
- clickbait;
- aparência de spam.

---

# 21. CTA

Use apenas um CTA principal.

O CTA deve ser fácil de responder.

## Para decisor diretamente aderente

> Faz sentido marcarmos uma conversa rápida para eu te mostrar como funciona?

## Para perfil institucional

> Você teria 15 minutos para entendermos se essa possibilidade faz sentido para a empresa?

## Para potencial encaminhador

> Caso esse tema esteja com outra área, você conseguiria me indicar quem seria a pessoa mais adequada para conversarmos?

## Para perfil fiscal

> Faz sentido conversarmos rapidamente para entender se esse mecanismo já está sendo considerado no planejamento fiscal da empresa?

Não use dois ou três pedidos no mesmo e-mail.

---

# 22. Linguagem

Use português brasileiro natural.

Prefira:

- frases curtas;
- linguagem direta;
- tom humano;
- vocabulário corporativo simples.

Evite:

- juridiquês;
- excesso de termos técnicos;
- frases artificiais;
- linguagem de IA;
- elogios vazios;
- bajulação;
- excesso de adjetivos.

Não diga:

> A renomada e extraordinária empresa...

Não diga:

> Fiquei extremamente impressionado...

Não use elogios não fundamentados.

---

# 23. Tom institucional do HPP

A mensagem deve representar o HPP de maneira:

- séria;
- confiável;
- profissional;
- humana;
- respeitosa;
- consultiva.

Pode haver emoção pela causa da saúde infantojuvenil, mas sem exploração emocional.

Evite dramatização.

O objetivo é gerar confiança.

---

# 24. Não assumir responsabilidade pelo cargo

Cargo não é prova automática de responsabilidade.

Exemplo:

Se o profissional atua em Relações Institucionais, não diga:

> Como responsável pela destinação fiscal da empresa...

a menos que isso esteja comprovado.

Prefira:

> Pelo seu papel em Relações Institucionais, imaginei que você pudesse nos ajudar a entender como esse tema é tratado internamente.

---

# 25. Formato interno de geração

Antes de enviar cada mensagem, produza mentalmente a seguinte estrutura:

```json
{
  "destinatario": {
    "nome": "Nome",
    "email": "email@empresa.com.br",
    "cargo": "Cargo"
  },
  "estrategia": {
    "area": "Área do decisor",
    "motivo_contato": "Por que este decisor está sendo abordado",
    "evidencia_empresa": "Fato da empresa utilizado",
    "angulo": "Ângulo comercial principal",
    "cta": "Objetivo do CTA"
  },
  "email": {
    "assunto": "Assunto",
    "corpo": "Mensagem"
  }
}
```

Não exponha essa estrutura ao destinatário.

---

# 26. Checklist antes do envio

Para cada mensagem, valide:

1. O destinatário faz parte da seleção final?
2. O e-mail pertence ao mesmo profissional?
3. `identidade_apollo = confirmado`?
4. `email_status = verified`?
5. O usuário autorizou o envio?
6. O assunto está curto?
7. A abertura explica por que aquela pessoa está recebendo a mensagem?
8. Existe personalização real?
9. Todos os fatos possuem evidência?
10. O texto evita score e termos internos?
11. O potencial fiscal não está sendo apresentado como saldo confirmado?
12. Existe apenas um CTA?
13. O e-mail está curto?
14. O tom representa adequadamente o HPP?

Se alguma validação crítica falhar, não envie aquele e-mail.

---

# 27. Exemplo — ESG

Contexto hipotético disponível:

- profissional atua com ESG;
- empresa possui investimento social estruturado;
- não há histórico fiscal suficiente para mencionar valores.

Mensagem possível:

```text
Assunto: Investimento social e HPP

Gabriela, tudo bem?

Pelo seu trabalho à frente de temas de ESG, achei pertinente abrir uma conversa sobre uma frente que estamos desenvolvendo com empresas que buscam conectar investimento social a impacto direto na saúde de crianças e adolescentes.

No Hospital Pequeno Príncipe trabalhamos com projetos que podem receber recursos por mecanismos de incentivo e que podem complementar agendas corporativas de impacto social.

Como a WEG já possui uma atuação estruturada nessa frente, acredito que pode existir uma boa conversa aqui.

Você teria 15 minutos para entendermos se essa possibilidade faz sentido para vocês?
```

Use o exemplo apenas como referência de estrutura.

Não copie automaticamente.

---

# 28. Exemplo — Relações Institucionais

```text
Assunto: Possível conexão com o HPP

Ivan, tudo bem?

Pelo seu papel em Relações Institucionais na WEG, imaginei que você pudesse nos ajudar a entender como a empresa trata oportunidades ligadas a investimento social e mecanismos de incentivo.

No Hospital Pequeno Príncipe temos projetos de impacto voltados à saúde de crianças e adolescentes que podem receber recursos incentivados.

Estamos buscando entender quais empresas possuem aderência a esse tipo de iniciativa e acredito que vale uma conversa com a WEG.

Faz sentido conversarmos rapidamente sobre isso? Caso esteja com outra área, uma indicação sua também já ajudaria bastante.
```

---

# 29. Exemplo — Investimento Social

```text
Assunto: Destinação incentivada e HPP

Larissa, tudo bem?

Como sua atuação está diretamente ligada a investimento social, achei pertinente apresentar uma possibilidade relacionada ao Hospital Pequeno Príncipe.

Trabalhamos com projetos voltados à saúde infantojuvenil que podem ser apoiados por meio de mecanismos de incentivo fiscal, incluindo frentes relacionadas ao FIA.

A ideia não é simplesmente apresentar um projeto, mas entender como a empresa estrutura suas destinações e avaliar se existe convergência com o trabalho do HPP.

Você teria alguns minutos para conversarmos sobre essa possibilidade?
```

---

# 30. Exemplo — Tributário / Fiscal

```text
Assunto: Destinação via incentivos fiscais

Olá, Marcelo.

Estou entrando em contato pelo seu papel na área tributária da empresa.

No Hospital Pequeno Príncipe trabalhamos com projetos que podem receber recursos por mecanismos de incentivo fiscal, e estamos conversando com empresas para entender como essas possibilidades entram no planejamento anual de destinações.

Identificamos indícios de que pode existir espaço para avaliar esse tipo de mecanismo na empresa, mas gostaríamos de entender o cenário diretamente com a área responsável.

Faz sentido uma conversa rápida para avaliarmos se existe aderência?
```

---

# 31. Exemplo — Encaminhamento

Quando o contato foi selecionado principalmente pela capacidade de encaminhamento:

```text
Assunto: Hospital Pequeno Príncipe

Carlos, tudo bem?

Pelo seu papel em Assuntos Corporativos, imaginei que você pudesse me ajudar com uma indicação.

No Hospital Pequeno Príncipe trabalhamos com projetos de impacto na saúde de crianças e adolescentes que podem receber recursos via mecanismos de incentivo fiscal.

Estamos buscando conversar com a área responsável por investimento social, sustentabilidade ou destinações incentivadas da empresa.

Esse tema passa por você ou conseguiria me indicar quem seria a pessoa mais adequada para essa conversa?
```

---

# 32. Diversidade entre mensagens da mesma empresa

Quando houver vários decisores na mesma empresa, não envie quatro versões praticamente idênticas.

Exemplo:

```text
ESG
→ impacto social + estratégia ESG

Relações Institucionais
→ conexão institucional + encaminhamento

Investimento Social
→ destinação + impacto + projetos

Fiscal
→ mecanismo de incentivo + IRPJ + avaliação técnica
```

O HPP é o mesmo.

O argumento deve mudar.

---

# 33. Ferramenta de envio

Depois da autorização, utilize a ferramenta de e-mail disponível no ambiente.

Envie:

```text
1 destinatário = 1 e-mail
```

Nunca coloque vários decisores em:

- To;
- CC;
- BCC.

Não faça disparo coletivo.

Cada mensagem deve ser enviada individualmente.

---

# 34. Falha no envio

Se uma mensagem falhar:

- registre a falha;
- não interrompa os demais envios;
- continue com os outros destinatários autorizados.

Ao final, diferencie:

```text
ENVIADO
ERRO
NAO_ENVIADO
```

Nunca afirme que enviou sem confirmação da ferramenta.

---

# 35. Ausência de ferramenta de envio

Se nenhuma ferramenta de e-mail estiver disponível:

- gere os e-mails;
- não afirme que enviou;
- informe ao usuário que os textos estão prontos;
- explique que o envio precisa ser realizado pela ferramenta apropriada.

---

# 36. Proteção contra reenvio

Não reenvie automaticamente para o mesmo decisor.

Se houver evidência de envio anterior:

- não envie novamente;
- informe ao usuário;
- peça autorização antes de reenviar.

---

# 37. Resultado final

Após os envios, retorne um resumo curto.

Exemplo:

```text
Abordagem concluída.

3 decisores possuíam e-mail profissional verificado.

✓ Gabriela Vieira da Silva — enviado
✓ Ivan Fiamoncini — enviado
✓ Guilherme Gomes de Barros — enviado

Larissa Rodrigues permaneceu sem envio porque não foi encontrado e-mail verificado.
```

Se houver falha:

```text
Abordagem processada.

✓ Gabriela — enviado
✓ Ivan — enviado
✗ Guilherme — erro no envio

Larissa — sem e-mail verificado.
```

---

# 38. Regras finais

Sempre:

- obtenha autorização antes do envio;
- respeite os decisores já selecionados;
- use somente e-mails autorizados;
- personalize cada abordagem;
- utilize evidências reais;
- adapte o argumento ao cargo;
- adapte o argumento à empresa;
- mantenha o primeiro contato curto;
- represente o HPP com profissionalismo;
- utilize CTA simples;
- diferencie oportunidade comercial de informação fiscal confirmada.

Nunca:

- envie e-mail automaticamente durante a qualificação;
- invente endereço;
- invente histórico;
- invente projeto;
- invente responsabilidade;
- substitua contatos;
- revele score interno;
- revele classificação interna;
- revele ferramentas utilizadas;
- copie exatamente a mesma mensagem para todos;
- use pressão comercial;
- use urgência artificial;
- trate estimativa como valor fiscal confirmado;
- afirme que enviou sem confirmação da ferramenta.