# 06 — Ferramenta 01: Template de especificação

30/10/2026 · Xavier (Tangerina Tech)

| Campo | Valor |
|-------|-------|
| ID | `spec-template` |
| Categoria | Especificação |
| Tipo | `ui` (React; grava arquivos pelo servidor) |
| Referência | [`referencias/template-especificacao-funcionalidade.md`](referencias/template-especificacao-funcionalidade.md) (original `.docx` na mesma pasta) |
| Consumidor | Skill `especificacao-funcionalidade` do Claude |

## 1. Objetivo

Preencher o "Template — Especificação de funcionalidade" num formulário guiado e entregar o resultado no formato que a skill espera: texto pronto para colar, `.md` ou um pacote com os anexos. Isso dispensa duplicar o documento à mão e reduz as perguntas da Parte C.

## 2. Escopo

**Dentro**
- Formulário com todos os campos do template: 4 obrigatórios, a lista "O que precisa fazer", 8 opcionais e a tabela de anexos.
- Exemplos do template visíveis como *placeholder* e ajuda por campo ("Para que serve").
- Três saídas: **copiar** (Markdown), **salvar `.md`** e **gerar pacote** (pasta com `.md` + anexos + `PROMPT.txt`).
- Rascunho salvo automaticamente e lista de rascunhos/pacotes anteriores.
- Prompt sugerido para colar no Claude, incluindo a pasta do repositório quando informada.

**Fora (por enquanto)**
- Chamar o Claude direto para gerar a especificação (fica para a fase 3, reaproveitando os provedores de IA).
- Criar um Doc no claude.ai ou Google Docs.
- Editar `.docx`.

## 3. Campos

### Obrigatórios

| Campo | ID | Tipo | Validação | Placeholder (do template) |
|-------|----|------|-----------|---------------------------|
| Nome da funcionalidade | `nome` | texto | não vazio, ≤ 120 | Rastreamento de ações do usuário |
| Projeto e repositório | `projeto` | texto + seletor de pasta opcional (`repoPath`) | não vazio | Mighty Earth · mightyearth-vigilanciadacarne |
| Objetivo (1 a 3 frases) | `objetivo` | texto longo | não vazio; aviso se > 3 frases | Saber quais regiões mobilizam mais… |
| Quem usa | `quemUsa` | texto | não vazio | Visitante anônimo; admin do Payload; … |
| O que precisa fazer | `itens[]` | lista (uma linha por item, Enter cria novo) | ≥ 1 item | "criar enum para sys_action e tags" |

### Opcionais

| Campo | ID | Para que serve (exibido como ajuda) |
|-------|----|------------------------------------|
| Regras já conhecidas | `regras` | Viram as regras de negócio (RN) da Parte A |
| Fora de escopo | `foraEscopo` | Evita que a especificação cresça além do pedido |
| Dados e integrações | `dados` | Base do modelo de dados e das integrações na Parte B |
| Telas ou relatórios afetados | `telas` | Onde instrumentar ou o que desenhar |
| Métricas de sucesso | `metricas` | Viram KPIs e critérios de aceite |
| Restrições | `restricoes` | Limitam as escolhas técnicas |
| Dúvidas que você já tem | `duvidas` | Entram direto na Parte C, com uma proposta |
| Quem decide / valida | `decisores` | Preenche a coluna "Decide" das decisões em aberto |

### Anexos

Tabela editável `Arquivo | O que é | Observação`. Cada linha pode ser:
- **Arquivo local** (seletor; `arquivo` vem do nome e o caminho fica guardado), copiado para o pacote; ou
- **Só texto** (ex.: um link), sem cópia.

### Regra dos obrigatórios

O template diz *"Preencha só o que souber; o que faltar vira pergunta"*. Por isso, **campo obrigatório vazio não bloqueia a geração**: o botão fica ativo, aparece um aviso amarelo listando o que falta e o `.md` sai com `_(não informado)_` no campo, o que a skill transforma em pergunta.

## 4. Saídas

### 4.1 Markdown gerado

Segue a estrutura do template original, sem as seções de instrução e com os exemplos substituídos pelos valores:

```markdown
# Template — Especificação de funcionalidade: {nome}

{data dd/mm/aaaa} · @{autor}

## Campos obrigatórios

| Campo | Valor |
|-------|-------|
| Nome da funcionalidade | {nome} |
| Projeto e repositório | {projeto} |
| Objetivo (1 a 3 frases) | {objetivo} |
| Quem usa | {quemUsa} |

**O que precisa fazer**

- {itens[0]}
- {itens[1]}

## Campos opcionais

| Campo | Valor |
|-------|-------|
| Regras já conhecidas | {regras} |
| … | … |

## Anexos

| Arquivo | O que é | Observação |
|---------|---------|------------|
| {arquivo} | {oQueE} | {observacao} |

## Repositório

Pasta local: `{repoPath}`
```

- Opcionais vazios: a linha é omitida (configurável: "manter linhas vazias").
- Quebras de linha e `|` dentro de células são escapados para não quebrar a tabela.
- `autor` vem de Configurações (padrão: nome do usuário do SO).

### 4.2 Copiar

Copia o Markdown para a área de transferência e mostra um *toast*: "Template copiado. Cole no Claude junto dos anexos."

### 4.3 Salvar `.md`

Abre um diálogo de salvar com o nome padrão `especificacao-{slug}.md`.

### 4.4 Gerar pacote

```
{pastaSpecs}/{projeto-slug}/{AAAA-MM-DD}-{slug}/     # pastaSpecs padrão: Documentos\ToolBelt\specs\ (D24)
├─ especificacao-{slug}.md      # o template preenchido
├─ anexos/                      # cópias dos arquivos anexados
│  └─ system_actions.pdf
├─ PROMPT.txt                   # texto para colar no Claude
└─ .spec.json                   # dados do formulário (permite reabrir/editar)
```

`PROMPT.txt`:

```
Gere a especificação a partir deste template.
Anexei: especificacao-{slug}.md e os arquivos da pasta anexos/ ({lista}).
O repositório está em: {repoPath}        ← só se informado
```

Depois de gerar: botões "Abrir pasta" e "Copiar prompt".

## 5. Tela

```
┌ Especificação › Template de especificação ───────────────────────────┐
│ [ Executar ]  Guia   Histórico                     Rascunhos ▾       │
├───────────────────────────────────┬──────────────────────────────────┤
│ OBRIGATÓRIOS             3/5 ●●●○○│  Pré-visualização (Markdown)      │
│ Nome da funcionalidade  [       ] │  # Template — Especificação…     │
│ Projeto e repositório   [     ]📁 │  | Campo | Valor |               │
│ Objetivo                [       ] │  …                               │
│ Quem usa                [       ] │                                  │
│ O que precisa fazer               │                                  │
│  • [                         ] ＋ │                                  │
│ ▸ OPCIONAIS (0/8)                 │                                  │
│ ▸ ANEXOS (0)                      │                                  │
├───────────────────────────────────┴──────────────────────────────────┤
│ ⚠ Falta: Quem usa       [ Copiar ]  [ Salvar .md ]  [ ▶ Gerar pacote ]│
└───────────────────────────────────────────────────────────────────────┘
```

Formulário à esquerda e pré-visualização ao vivo à direita. Opcionais e anexos ficam em seções recolhíveis, e a barra de ações fica fixa no rodapé.

## 6. Regras

| # | Regra |
|---|-------|
| RN01 | (D16) Gerar nunca é bloqueado por campo vazio; os obrigatórios vazios aparecem no aviso e no `.md` como `_(não informado)_` |
| RN02 | O `slug` vem do nome: minúsculas, sem acento, `-` como separador, ≤ 60 caracteres |
| RN03 | Se a pasta do pacote já existir, o nome ganha o sufixo `-2`, `-3`… (nunca sobrescreve) |
| RN04 | Anexos são **copiados**, nunca movidos; o original não é alterado |
| RN05 | O rascunho é salvo a cada 2 s de inatividade em `<userData>/drafts/spec-template/` |
| RN06 | Um pacote pode ser reaberto a partir do `.spec.json` para editar e gerar de novo (gera uma nova versão da pasta, sem sobrescrever) |
| RN07 | Pacotes gerados aparecem na **Biblioteca de specs** (Guias), agrupados por projeto |

## 7. Critérios de aceite

- [ ] Com todos os campos preenchidos → "Copiar" coloca na área de transferência um Markdown idêntico à pré-visualização.
- [ ] Com "Quem usa" vazio → o aviso mostra "Falta: Quem usa" e o `.md` contém `Quem usa | _(não informado)_`.
- [ ] Com 2 anexos locais → o pacote tem `anexos/` com os 2 arquivos, a tabela de anexos cita os 2 e o `PROMPT.txt` lista os 2.
- [ ] Gerar o pacote duas vezes com o mesmo nome no mesmo dia → existem duas pastas (`…-slug` e `…-slug-2`).
- [ ] Fechar o app no meio do preenchimento e reabrir → o rascunho é recuperado.
- [ ] Célula com `|` e quebra de linha → a tabela Markdown continua válida.
- [ ] O `.md` gerado, anexado ao Claude com o prompt, faz a skill `especificacao-funcionalidade` gerar a especificação sem perguntar pelos campos preenchidos.
- [ ] Todo o fluxo funciona por teclado (Tab, Enter na lista, `Ctrl+Enter` gera o pacote).

## 8. Técnica

| Item | Implementação |
|------|---------------|
| Esquema | `tools/spec-template/schema.ts` (Zod), compartilhado entre formulário, gerador e `.spec.json` |
| Gerador | `tools/spec-template/render.ts`: função pura `render(data) → string`, testada com Vitest (snapshots) |
| Pacote | Server Action `createSpecPackage(data)`: cria pasta, copia anexos, grava `.md`, `PROMPT.txt` e `.spec.json` |
| Rascunhos | Server Actions `saveDraft` / `listDrafts` / `loadDraft` |
| Seletor de pasta/arquivo | `dialog.showOpenDialog` do Electron, chamado pelo servidor |
| Área de transferência | `navigator.clipboard.writeText` no renderer |
| Manifesto | `tools/spec-template/tool.yaml` com `type: ui`, `category: especificacao` |
| Guia | `tools/spec-template/README.md` (resumo deste documento + exemplo preenchido) |
