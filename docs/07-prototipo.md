# 07 — Protótipo navegável (fase 0 → 1)

30/10/2026 · Xavier (Tangerina Tech)

Protótipo visual para revisão **antes de qualquer código**. Cobre T1 Início, T2 Paleta `Ctrl+K`, T4 Ferramenta `script` (Pull App DB) e a Ferramenta 01 (Template de especificação), nos temas escuro (padrão) e claro.

| Item | Onde |
|------|------|
| Canvas de design (revisão, comentários) | Artefato **"Tool Belt — Protótipo"** no claude.ai: <https://claude.ai/artifact/MkiqYqmtY7kjNuZ3q5ntn1> (privado; compartilhar pelo menu *Share* se outra pessoa for revisar) |
| Fonte do protótipo (cópia) | [`docs/prototipo/`](prototipo/) — arquivos `.dc.html` do canvas; só renderizam dentro do editor de design do claude.ai |

## 1. Pranchas do canvas

| Prancha | Tela | Tema | Estado inicial |
|---------|------|------|----------------|
| `Main` | T1 Início (navegável, todas as telas) | Escuro | Início |
| `Paleta` | T2 Paleta `Ctrl+K` | Escuro | Paleta aberta com a busca "pull" |
| `PullAppDb` | T4 Ferramenta `script` | Escuro | Pull App DB, aba Executar |
| `TemplateSpec` | Ferramenta 01 | Escuro | Formulário com "Quem usa" vazio |
| `InicioClaro` | T1 Início | Claro | Início |
| `TemplateSpecClaro` | Ferramenta 01 | Claro | Igual à escura |

Todas as pranchas usam o mesmo componente (`Main`) com propriedades `theme`, `screen`, `palette` e `paletteQuery`. Mudar o `Main` muda todas. No canvas, o botão **Play** de qualquer prancha deixa navegar.

## 2. O que dá para fazer no protótipo

### Geral
- Barra de título com busca, Configurações, alternância de tema (sol/lua) e controles de janela do Windows.
- Barra lateral de 240 px com Início, Favoritos, Recentes, Categorias (com contagem), Projetos, Guias e **+ Nova ferramenta**; botão de recolher (`Ctrl+B` no app real).
- Itens fora do escopo (outras ferramentas, Guias, Cofre, Nova ferramenta) mostram um aviso "fica fora deste protótipo".

### T1 Início
Saudação, busca grande (abre a paleta), Favoritos em cards (Pull App DB, Template de especificação, JWT Decoder), Recentes com status da última execução e grade de Categorias com contagem e atalho "Nova ferramenta".

### T2 Paleta `Ctrl+K`
- Abre pela busca da barra de título ou do Início.
- Sem texto: grupos **Recentes** e **Ações**.
- Com texto: busca *fuzzy* sem acento em nome, categoria e palavras-chave (ex.: "adb", "bruno", "jwt"), agrupada em **Ferramentas / Guias / Ações**.
- **Detecção pelo conteúdo colado**: um texto que começa com `eyJ…` sugere o JWT Decoder; Markdown (`# título`, listas, `**negrito**`) sugere Markdown → Texto.
- Teclado: ↑ ↓ navegam, Enter abre, Esc fecha. "Alternar tema" e "Ir para o Início" funcionam.

### T4 Pull App DB
- Cabeçalho com trilha, chips **GDF Boticário** e **script**, e alerta de pré-requisito "ADB não encontrado" com link **Configurar** (simula a detecção do `adb`).
- Abas **Executar | Guia | Histórico**.
- Formulário gerado pelo manifesto (pacote, caminho do banco, pasta de saída) e **comando equivalente** que muda ao editar os campos, com botão copiar.
- **Executar** simula o runner: sem `adb` falha no passo 1 com código 3; depois de "Configurar" roda os 4 passos (`::step::`), mostra a barra de progresso, a saída (`::output::`) com "Abrir pasta" e "Copiar caminho", e grava a execução no Histórico. **Cancelar** encerra com código 4.
- Guia: parâmetros, pré-requisitos com status e códigos de saída.

### Ferramenta 01 — Template de especificação
- Formulário à esquerda, **pré-visualização Markdown ao vivo** à direita, barra de ações no rodapé.
- Obrigatórios com contador (`4/5` e pontos). "O que precisa fazer" é uma lista: **Enter** cria item, **Backspace** em item vazio remove.
- Opcionais (8 campos, com o "Para que serve" como ajuda) e Anexos (arquivo local ou só texto/link) em seções recolhíveis.
- Aviso amarelo "**Falta:** Quem usa" sem bloquear a geração (D16/RN01); o `.md` sai com `_(não informado)_`.
- `|` e quebras de linha são escapados na tabela; opcionais vazios saem do `.md`; seção Repositório aparece quando a pasta é escolhida.
- **Copiar** (área de transferência + *toast*), **Salvar .md** (diálogo simulado) e **Gerar pacote**: modal com a árvore da pasta em `Documentos\ToolBelt\specs\<projeto>\<data>-<slug>\` e o `PROMPT.txt`, com "Abrir pasta" e "Copiar prompt". Gerar de novo no mesmo dia cria `…-2` (RN03). Os pacotes aparecem na aba Histórico.

## 3. Simplificações do protótipo

| No protótipo | No app |
|--------------|--------|
| `Ctrl+K`, `Ctrl+B`, `Ctrl+Enter` aparecem como dica; abrem por clique (o editor de design não permite atalhos globais) | Atalhos globais do doc 03 |
| Diálogos de arquivo/pasta, "Abrir pasta" e execução do script são simulados | `dialog.showOpenDialog`, `shell.openPath`, runner Bash |
| Dados de exemplo (objetivo, itens, histórico, anexo `system_actions.pdf`) | Rascunho real salvo em `<userData>/drafts/` |
| Só Pull App DB e Template de especificação abrem | 14 ferramentas pelo manifesto |
| Controles de janela no estilo Windows | `titleBarStyle: hidden` com controles por SO |

## 4. Achados de design

1. **Contraste do acento no tema claro.** O doc 03 define `--accent-fg: #ffffff` no claro, mas branco sobre `#E55F00` dá cerca de 4,1:1 (não passa AA em texto de 14 px). O texto escuro `#0d0d0d` sobre `#E55F00` dá cerca de 4,7:1. O protótipo usa `#0d0d0d` nos dois temas → **D26 (aprovada)**.
2. **Laranja como cor de texto.** `#E55F00` sobre branco também fica em ~4,1:1. Para links, item ativo e chips no tema claro, o protótipo usa um token novo `--accent-text: #B84A00` (~5,2:1). No escuro, `--accent-text: #FF7A1A` → **D26**.
3. Tokens novos de apoio: `--accent-soft` (fundo do item ativo e de chips), `--scrim` (fundo de modal) e `--shadow`.
4. O log usa fundo fixo quase preto nos dois temas, para as cores ANSI dos scripts ficarem legíveis.
5. O doc 03 mostra a janela com controles de macOS (● ● ●). Como o uso agora é no Windows, o protótipo usa os controles do Windows à direita.

## 5. Como revisar

1. Abrir o canvas e usar **Play** na prancha `Main` para navegar por tudo.
2. Comentar direto nas pranchas (comentários do canvas) ou listar ajustes no chat.
3. Depois da revisão: atualizar o doc 03 com os tokens aprovados e abrir a fase 1 (repositório Next + Electron).
