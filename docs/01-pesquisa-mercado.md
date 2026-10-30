# 01 — Pesquisa de mercado

30/10/2026 · Xavier (Tangerina Tech)

Objetivo: entender os padrões de mercado para "caixas de ferramentas" de desenvolvedor e portais internos, e decidir o que adotar.

## Referências analisadas

| Produto | Tipo | O que faz bem | O que adotamos |
|---------|------|---------------|----------------|
| **DevToys 2.0** | Desktop, open source (Win/Mac/Linux) | Dezenas de ferramentas offline; busca *fuzzy*; favoritos; "smart detection" (cola um conteúdo e ele sugere a ferramenta); encadeamento de ferramentas; CLI; extensões via SDK | Busca *fuzzy*, favoritos, detecção pelo conteúdo colado, CLI no futuro, modelo de extensão |
| **DevUtils** | Desktop (macOS, pago) | Interface limpa, integração com o SO, detecção automática pela área de transferência | Detecção pela área de transferência |
| **IT-Tools** | Web, open source | Catálogo grande organizado por categoria, favoritos no topo, ferramentas autocontidas | Categorias com ícone, favoritos fixados no topo da navegação |
| **CyberChef** | Web | "Receitas": encadear operações em sequência | Guias por categoria como fluxos (ex.: pull → seed → push) |
| **Raycast** | Launcher (macOS/Win) | Paleta de comandos como entrada principal; cada comando declarado em manifesto; extensões com formulário gerado | Paleta `Ctrl+K`; manifesto declarativo; formulário gerado pelos parâmetros |
| **Backstage (Spotify)** | Portal interno de desenvolvedor | Catálogo de software descrito por YAML; *Software Templates* (scaffolder: `parameters → steps`); TechDocs (docs junto do código) | `tool.yaml` por ferramenta; criação de ferramenta por template com formulário; guia gerado a partir do que está no repositório |

## Padrões que se repetem

1. **Navegação em dois níveis**: categoria → ferramenta, com busca global por cima de tudo.
2. **Favoritos e recentes** acima das categorias.
3. **Ferramenta = tela única**: entrada à esquerda/topo, saída à direita/baixo, com copiar/salvar sempre visíveis.
4. **Offline como argumento de confiança**: dados sensíveis (JWT, payloads) não saem da máquina.
5. **Descrição declarativa** (manifesto) separada da implementação, o que permite gerar UI, docs e validação.
6. **Extensibilidade** por pacote/pasta com contrato estável.
7. **Templates de criação** que já trazem estrutura, docs e testes.

## Next.js + Electron em 2026

| Abordagem | Como funciona | Prós | Contras |
|-----------|---------------|------|---------|
| Nextron | Boilerplate Next + Electron | Fácil de começar | Pouca manutenção; preso ao Pages Router |
| Static export + IPC | `output: 'export'`; o processo main faz o trabalho de SO via IPC | Simples; superfície de ataque menor | Sem Server Components nem Route Handlers; toda chamada de SO precisa de um canal IPC |
| **`next-electron-rsc`** (escolhido) | O Next roda dentro do processo main do Electron, sem abrir porta; as requisições são interceptadas pelo `protocol` da sessão | Server Components, Server Actions e Route Handlers acessam Node e Electron diretamente; App Router completo | `asar: false`; as páginas precisam ser `force-dynamic`; o `next` precisa ser `dependency`; HTTP externo só pelo lado servidor |

## Conclusões para o Tool Belt

- O diferencial em relação ao DevToys e ao IT-Tools é **executar os scripts próprios** (Bash, ADB, Bruno) **com contexto de projeto e guia**, e não só utilitários genéricos.
- O modelo **manifesto + scaffolder** do Backstage, em escala local, resolve a catalogação e a criação de ferramentas.
- A **paleta de comandos** do Raycast resolve o "encontrar em 2 segundos".

## Fontes

- [DevToys 2.0 Preview (blog oficial)](https://www.devtoys.app/blog/announcing-devtoys-2.0-preview)
- [DevToys — documentação de extensões](https://devtoys.app/doc/articles/extension-development/getting-started/create-an-extension.html)
- [DevToys 2.0 lançado com extensões e CLI (AlternativeTo)](https://alternativeto.net/news/2024/6/devtoys-2-0-released-with-macos-and-linux-support-extensions-and-command-line-integration)
- [DevUtils vs DevToys vs OpenDev (DEV Community)](https://dev.to/jamalianpour/devutils-vs-devtoys-vs-opendev-which-developer-utility-tool-is-right-for-you-a4j)
- [IT-Tools vs DevToys](https://aiindigo.com/compare/it-tools-vs-devtoys)
- [Backstage — guia de portal interno 2026](https://lucaberton.com/blog/backstage-internal-developer-portal-setup-guide-2026/)
- [Backstage na prática (OneUptime)](https://oneuptime.com/blog/post/2026-01-25-developer-portal-backstage/view)
- [next-electron-rsc (GitHub)](https://github.com/kirill-konshin/next-electron-rsc)
- [Electron + Next.js sem Nextron (DEV Community)](https://dev.to/rbfraphael/desktop-apps-with-electron-nextjs-without-nextron-ad2)
- [Building an Electron app with Next.js (DoltHub)](https://dolthub.com/blog/2024-09-11-building-an-electron-app-with-nextjs)
