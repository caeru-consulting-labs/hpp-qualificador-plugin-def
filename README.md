# Qualificador HPP — Plugin

Plugin que empacota o fluxo completo de qualificação B2B do Hospital Pequeno
Príncipe (HPP) para captação via incentivos fiscais (FIA / Rouanet).

## O que está incluído

- **6 skills** (`qualificador-hpp/skills/`):
  - `instrucoes-gerais-hpp` — papel geral, comportamento, formato de resposta
    (substitui a necessidade de criar um Projeto manual no claude.ai com
    instruções coladas — já vem embutido no plugin)
  - `fluxo-qualificacao-hpp` — orquestra o fluxo ponta a ponta
  - `consultar-empresa-hpp` — consulta cadastral/econômica da empresa
  - `qualificar-empresa-hpp` — interpreta elegibilidade fiscal, calcula score ICP
  - `selecionar-decisores-hpp` — seleciona e classifica decisores
  - `abordagem-email-hpp` — prepara e envia e-mails de abordagem
- **1 conector MCP** (`qualificador-hpp/.mcp.json`): aponta para o servidor MCP
  já existente (n8n) que expõe as ferramentas `Consultar Empresa`,
  `Qualificar Empresa`, `Buscar Candidatos`, `Enriquecer Decisores` e
  `Cadastrar no Pipefy`.

## Subir no GitHub

```bash
cd hpp-qualificador-plugin
git init
git add .
git commit -m "Plugin Qualificador HPP"
git branch -M main
git remote add origin <URL_DO_SEU_REPOSITORIO>
git push -u origin main
```

O repositório pode ser público ou privado. Se for privado, a conta Claude que
for instalar precisa ter o **GitHub App do Claude** instalado nesse
repositório/conta.

## Instalar e testar

No Claude (Customize → Plugins → "+" → Add marketplace → GitHub), ou via
Claude Code:

```bash
claude plugin marketplace add <owner>/<repo>
claude plugin install qualificador-hpp@hpp-qualificador-marketplace
```

Na primeira ativação, você precisará autorizar/conectar o servidor MCP
`Qualificador_HPP` (isso é feito por quem instala — não precisa de admin
para uso pessoal).

## Ponto de atenção para handoff a outra organização

O `.mcp.json` aponta para a **mesma instância n8n** usada aqui (mesmas
credenciais de Pipefy/Apollo). Para entregar isso como produto a outra
organização:

1. Deployar uma instância própria do fluxo n8n para essa organização (ou
   multi-tenant, com credenciais isoladas);
2. Atualizar a `url` em `.mcp.json` para apontar para essa nova instância;
3. Revisar as regras "hardcoded" nas skills (UFs prioritárias, faixas de
   faturamento, remetente do e-mail em `abordagem-email-hpp`) e adaptar
   para os critérios da nova organização;
4. Publicar essa versão do repositório para eles instalarem.

## Estrutura

```
hpp-qualificador-plugin/
├── .claude-plugin/
│   └── marketplace.json
└── qualificador-hpp/
    ├── .claude-plugin/
    │   └── plugin.json
    ├── .mcp.json
    └── skills/
        ├── instrucoes-gerais-hpp/SKILL.md
        ├── fluxo-qualificacao-hpp/SKILL.md
        ├── consultar-empresa-hpp/SKILL.md
        ├── qualificar-empresa-hpp/SKILL.md
        ├── selecionar-decisores-hpp/SKILL.md
        └── abordagem-email-hpp/SKILL.md
```
