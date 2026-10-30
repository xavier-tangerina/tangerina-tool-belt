# 00 — Orientações de produto

30/10/2026 · Xavier (Tangerina Tech)

## Uma frase

**Um único lugar, offline, para encontrar, entender, executar e criar as ferramentas do dia a dia, sem lembrar onde o script está nem quais parâmetros ele recebe.**

## Problema

- As ferramentas estão espalhadas em `C:\Users\livia\_tools`, misturadas com dados de teste e arquivos pessoais.
- Cada uma roda de um jeito: HTML no navegador, PowerShell, Python, Node, Bash.
- Os parâmetros, pré-requisitos (ADB, Bruno, Playwright) e a ordem de uso (pull → seed → push) ficam só na memória de quem criou.
- Segredos e caminhos estão fixos no código, o que impede compartilhar as ferramentas.
- Criar uma ferramenta nova não segue nenhum padrão.

## Público

| Fase | Quem | Implicação |
|------|------|------------|
| Agora | Xavier (uso pessoal, Windows) | Sem instalador nem auto-update; foco em velocidade |
| Depois | Equipe Tangerina Tech | A arquitetura já nasce pronta: manifesto, cofre por usuário, nada fixo em `C:\Users\livia` |

## Princípios

1. **Offline e local primeiro.** Nada sai da máquina, exceto as chamadas que a própria ferramenta faz (ex.: Bruno → API) e a IA, quando o usuário pede.
2. **Toda ferramenta tem um manifesto.** Se não está descrita em `tool.yaml`, não existe no portal. O manifesto gera a tela, a validação e o guia.
3. **Encontrar em 2 segundos.** Busca `Ctrl+K` em primeiro lugar, depois categorias, favoritos e recentes.
4. **Executar sem decorar.** Parâmetros viram formulário; o comando equivalente fica visível e pode ser copiado.
5. **Seguro por padrão.** Segredos só no cofre do SO; ações destrutivas (ex.: sobrescrever banco do app) pedem confirmação explícita.
6. **Multiplataforma via Git Bash.** Todo script local é `.sh`.
7. **Documentado ao nascer.** Criar uma ferramenta cria também o guia dela.
8. **Identidade Tangerina.** Visual da marca (preto `#0d0d0d`, laranja `#FF6A00`), com tema claro e escuro.

## O que o Tool Belt é

- Catálogo navegável de ferramentas por **categoria** e por **projeto** (ex.: GDF Boticário).
- Executor de scripts `.sh` com formulário, log em tempo real, cancelamento e histórico.
- Casa de ferramentas de interface (React) como JWT Decoder e Markdown → Texto.
- **Guia**: documentação de uso por ferramenta, guias por categoria (fluxos) e biblioteca das especificações geradas pela skill.
- **Fábrica de ferramentas**: criar por formulário, importar um script existente ou gerar com IA.

## O que o Tool Belt não é (por enquanto)

- Não é um portal web nem um SaaS; não há servidor remoto.
- Não substitui o Bruno, o terminal ou a IDE; ele chama essas ferramentas.
- Não guarda dados de clientes nem massas de teste grandes (ficam fora do repositório).
- Não tem marketplace público de extensões.

## Primeira ferramenta

**Gerar template para a skill `especificacao-funcionalidade`**: um formulário com os campos do template oficial que gera o `.md` preenchido, copia para a área de transferência ou monta uma pasta de pacote com os anexos, pronta para pedir ao Claude: *"Gere a especificação a partir deste template"*. Detalhes no [doc 06](06-ferramenta-template-especificacao.md).

## Como medimos sucesso (uso pessoal)

| Indicador | Meta inicial |
|-----------|--------------|
| Ferramentas de `_tools` migradas com manifesto | 100% das 13 ferramentas |
| Tempo para achar e rodar uma ferramenta | < 10 s (busca + formulário) |
| Segredos fixos no código | 0 |
| Ferramentas novas criadas pelo portal com guia | 100% |
