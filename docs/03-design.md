# 03 — Design

30/10/2026 · Xavier (Tangerina Tech)

## 1. Direção

**Ferramenta de trabalho com a marca Tangerina.** É denso e rápido como um DevToys ou Raycast, mas com a identidade da Tangerina: base quase preta, laranja como único acento e tipografia geométrica. O tema escuro é o padrão, com um tema claro equivalente.

Regras:
- **O laranja é para ação e foco**, não para decoração: botão primário, item ativo, anel de foco e progresso.
- **Uma ferramenta por tela**, com entrada e saída visíveis ao mesmo tempo.
- **O texto técnico usa fonte mono**: comandos, logs, JSON e caminhos.

## 2. Tokens

### Cor

| Token | Escuro (padrão) | Claro | Uso |
|-------|-----------------|-------|-----|
| `--bg` | `#0d0d0d` | `#fafaf9` | Fundo da janela |
| `--surface` | `#161616` | `#ffffff` | Painéis, cards |
| `--surface-2` | `#1f1f1f` | `#f2f2f0` | Campos, hover |
| `--border` | `#2a2a2a` | `#e4e4e0` | Divisórias |
| `--text` | `#f5f5f4` | `#141414` | Texto principal |
| `--text-muted` | `#a3a3a3` | `#5c5c5c` | Rótulos, ajuda |
| `--accent` | `#FF6A00` | `#E55F00` | Primário, ativo, foco |
| `--accent-fg` | `#0d0d0d` | `#0d0d0d` | Texto sobre o acento (D26; era `#ffffff` no claro) |
| `--accent-text` | `#FF7A1A` | `#B84A00` | Laranja como texto: links, item ativo, chips (D26) |
| `--accent-soft` | `rgba(255,106,0,.14)` | `rgba(229,95,0,.12)` | Fundo do item ativo e de chips |
| `--success` | `#22c55e` | `#15803d` | Execução OK |
| `--warning` | `#f59e0b` | `#b45309` | Pré-requisito ausente |
| `--danger` | `#ef4444` | `#b91c1c` | Erro, ação destrutiva |

> O contraste precisa ser validado com WCAG AA na implementação. O laranja sobre branco não atinge 4.5:1 em texto pequeno, por isso o tema claro usa `#E55F00` e o texto escuro vai sobre o acento.

### Tipografia

| Papel | Fonte | Tamanhos |
|-------|-------|----------|
| Títulos | Space Grotesk 600 | 24 / 18 / 15 |
| Interface e texto | Figtree 400/500 | 14 (base) / 13 / 12 |
| Código, logs, comandos | JetBrains Mono 400 | 13 / 12 |

### Espaço, raio e movimento

- Grade de 4 px; espaçamentos 4 · 8 · 12 · 16 · 24 · 32.
- Raio: 6 (campos), 10 (cards), 999 (chips).
- Movimento: 120–180 ms *ease-out*; respeita `prefers-reduced-motion`.
- Densidade: compacta por padrão (linhas de 32 px na navegação).

## 3. Layout da janela

```
┌──────────────────────────────────────────────────────────────────────┐
│ ● ● ●  Tool Belt          [ 🔍 Buscar ferramenta…  Ctrl+K ]   ⚙  ◐ │  ← barra de título (arrastável)
├───────────────┬──────────────────────────────────────────────────────┤
│ ★ Favoritos   │  Banco de Dados › Pull App DB          [GDF Boticário]│
│   Pull App DB │  Copia o banco SQLite do app Android para o PC.       │
│ ⟲ Recentes    │  ⚠ ADB não encontrado — Configurar                   │
│               │ ─────────────────────────────────────────────────────│
│ CATEGORIAS    │  [ Executar ]  Guia   Histórico                       │
│ ▸ Especificação│                                                      │
│ ▸ Formatação  │  Pacote do app   [com.boticario.gdfauditoria   ]      │
│ ▸ DevTools    │  Pasta de saída  [~/ToolBelt/out/android_db  📁]      │
│ ▾ Banco Dados │                                                      │
│   • Pull      │  $ tools/pull-app-db/run.sh --pkg com.botic…  ⧉      │
│   • Push      │                                   [ ▶ Executar ]     │
│   • Seed      │ ┌──────────────────────────────────────────────────┐ │
│ ▸ API & Massa │ │ [1/4] Verificando dispositivo ADB…   OK          │ │
│ ▸ Git         │ │ [2/4] Verificando banco…             OK          │ │
│ ▸ Web & QA    │ └──────────────────────────────────────────────────┘ │
│ PROJETOS      │                                                      │
│ ▸ GDF Boticário│                                                     │
│ ─────────────│                                                      │
│ 📖 Guias      │                                                      │
│ ＋ Nova       │                                                      │
└───────────────┴──────────────────────────────────────────────────────┘
```

- Barra lateral de 240 px, recolhível (`Ctrl+B`), com favoritos e recentes no topo.
- Busca sempre na barra de título; `Ctrl+K` abre a paleta sobreposta.
- O cabeçalho da ferramenta mostra trilha, descrição, chip de projeto e alerta de pré-requisito.
- As abas são **Executar | Guia | Histórico**. Nas ferramentas `ui`, a aba Executar é a própria ferramenta.

## 4. Telas

| # | Tela | Conteúdo principal |
|---|------|--------------------|
| T1 | **Início** | Busca grande, favoritos (cards), recentes, categorias com contagem, atalho "+ Nova ferramenta" |
| T2 | **Paleta `Ctrl+K`** | Busca *fuzzy* em ferramentas, guias, specs e ações ("Nova ferramenta", "Abrir cofre"); detecção pelo conteúdo colado (JWT → JWT Decoder; Markdown → Markdown → Texto) |
| T3 | **Categoria** | Descrição, lista de ferramentas em cards, guias da categoria |
| T4 | **Ferramenta `script`** | Formulário gerado, comando equivalente copiável, botão Executar, terminal de log, saídas (arquivos e pasta) |
| T5 | **Ferramenta `ui`** | Layout entrada/saída lado a lado, com copiar, salvar e limpar |
| T6 | **Guia da ferramenta** | Markdown renderizado + tabela de parâmetros + pré-requisitos com status |
| T7 | **Histórico** | Execuções com data, parâmetros, duração e status; "Reexecutar" e "Ver log" |
| T8 | **Guias** | Guias por categoria (fluxos com passos clicáveis) e biblioteca de specs |
| T9 | **Nova ferramenta** | Assistente em 3 modos (formulário, importar, IA) → revisão de arquivos → salvar |
| T10 | **Configurações** | Aparência, Cofre (segredos), Pré-requisitos (bash, node, adb, bruno, python…), IA (motor, modelo), Pastas |
| T11 | **Confirmação destrutiva** | Modal que exige digitar o nome do recurso (ex.: nome do pacote) |

## 5. Componentes

Base: **shadcn/ui + Tailwind CSS** (componentes copiados para o repositório, com os tokens acima) e ícones **Lucide**.

| Componente | Observação |
|------------|------------|
| `AppShell` | Barra de título personalizada (`titleBarStyle: hidden`) + barra lateral + área de conteúdo |
| `CommandPalette` | `cmdk`, com grupos Ferramentas / Guias / Specs / Ações |
| `ToolHeader` | Trilha, nome, descrição, chips (categoria, projeto, tipo), status dos pré-requisitos |
| `ManifestForm` | Gera campos do `tool.yaml` (texto, número, enum, booleano, caminho, arquivo, segredo, lista) com validação Zod |
| `CommandPreview` | Linha de comando equivalente, mono, com copiar |
| `RunTerminal` | Log ao vivo (xterm.js), cores ANSI, cancelar, rolagem automática |
| `OutputPanel` | Arquivos gerados, abrir pasta, copiar caminho |
| `Markdown` | Renderização dos guias (com `mermaid`) |
| `EmptyState` | Ilustração simples + ação principal |
| `DangerConfirm` | Confirmação digitada para ações destrutivas |

## 6. Atalhos

| Atalho | Ação |
|--------|------|
| `Ctrl+K` | Paleta de comandos |
| `Ctrl+Enter` | Executar a ferramenta aberta |
| `Ctrl+B` | Recolher a barra lateral |
| `Ctrl+D` | Favoritar/desfavoritar |
| `Ctrl+,` | Configurações |
| `Esc` | Cancelar execução / fechar modal |

## 7. Acessibilidade

- Tudo navegável por teclado, com foco visível no laranja (anel de 2 px).
- Contraste AA nos dois temas.
- O log tem `aria-live="polite"`, e o status final é anunciado.
- A cor nunca é o único sinal: status sempre vem com ícone e texto.

## 8. Próximos passos de design

1. ~~Montar o protótipo das telas T1, T2, T4 e da Ferramenta 01~~ → feito, em revisão ([doc 07](07-prototipo.md)).
2. ~~Validar os tokens de contraste~~ → D26 aprovada (doc 07, seção 4); revalidar AA na implementação.
3. Desenhar o ícone do app (cinto + laranja).
