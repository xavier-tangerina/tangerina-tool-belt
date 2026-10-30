# Tangerina Tool Belt — Cinturão de Ferramentas

Aplicativo desktop (Next.js + Electron) que reúne, organiza por categoria e executa as ferramentas locais de desenvolvimento, design e especificação da Tangerina Tech.

> **Status:** Fase 0 (estratégia e documentação). Ainda não há código.

## Documentação

| # | Documento | Conteúdo |
|---|-----------|----------|
| 00 | [Orientações de produto](docs/00-orientacoes-produto.md) | Visão, público, princípios, o que é e o que não é |
| 01 | [Pesquisa de mercado](docs/01-pesquisa-mercado.md) | Referências (DevToys, IT-Tools, Raycast, Backstage…) e o que adotar |
| 02 | [Estratégia de produto](docs/02-estrategia-produto.md) | Arquitetura de informação, categorias, jornadas, roadmap |
| 03 | [Design](docs/03-design.md) | Identidade, tokens, layout, telas e componentes |
| 04 | [Arquitetura técnica](docs/04-arquitetura-tecnica.md) | Stack, manifesto de ferramenta, runner `.sh`, cofre, IA |
| 05 | [Inventário e migração](docs/05-inventario-migracao.md) | Ferramentas de `_tools`, categoria, plano de porte |
| 06 | [Ferramenta 01 — Template de especificação](docs/06-ferramenta-template-especificacao.md) | Especificação da primeira ferramenta |
| — | [Decisões](docs/decisoes.md) | Registro de decisões (ADR resumido) |
| — | [Perguntas em aberto](docs/perguntas-abertas.md) | Perguntas da fase 0 e respostas (todas resolvidas) |
| — | [Referências](docs/referencias/) | Template original da skill `especificacao-funcionalidade` |

## Regras do projeto

1. **Toda decisão é documentada** em `docs/decisoes.md` antes de virar código.
2. **Scripts locais são Git Bash (`.sh`)**, para rodar no Windows (Git for Windows), no macOS e no Linux.
3. **Nenhum segredo no repositório.** Os valores ficam no cofre do sistema operacional (veja o doc 04).
4. Os documentos principais são espelhados no Project **[TANGERINA] - TOOL BELT** do claude.ai.
