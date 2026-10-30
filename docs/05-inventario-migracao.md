# 05 — Inventário e plano de migração

30/10/2026 · Xavier (Tangerina Tech) · Origem: `C:\Users\livia\_tools`

## 1. Ferramentas encontradas (13)

| # | ID proposto | Origem | Tipo hoje | Categoria | Projeto | Destino | Dependências externas |
|---|-------------|--------|-----------|-----------|---------|---------|-----------------------|
| 1 | `jwt-decoder` | `jwt-decoder.html` | HTML | DevTools | — | `ui` (React) | — |
| 2 | `markdown-to-text` | `markdown-converter.html` | HTML (marked 9.1.6) | Formatação & Conversão | — | `ui` (React) | `marked` (npm) |
| 3 | `html-to-pdf` | `html-to-pdf.html` | HTML (html2canvas + jsPDF) | Formatação & Conversão | — | `ui` (React) | `html2canvas`, `jspdf` (npm) |
| 4 | `fullpage-screenshot` | `fullpage-screenshot.js` | Node + Playwright | Web & QA | — | `script` (`run.sh` → Node) ⚠️ | Playwright + Chromium |
| 5 | `git-report` | `git_report.py` (27 KB) | Python | Git | — | `script` (Bash puro) | `git` |
| 6 | `git-remote-ssh` | `git-remote-ssh.sh` + testes | **Bash (já no padrão)** | Git | — | `script` (mover) | `git`, `ssh` |
| 7 | `pull-app-db` | `pull-app-db.ps1` | PowerShell | Banco de Dados | GDF Boticário | `script` (Bash) | `adb` |
| 8 | `push-app-db` | `push-app-db.ps1` | PowerShell | Banco de Dados | GDF Boticário | `script` (Bash), **destrutiva** | `adb` |
| 9 | `seed-db` | `seed-db.ps1` | PowerShell + Bruno + sqlite3 | Banco de Dados | GDF Boticário | `script` (Bash), **destrutiva** | `npx @usebruno/cli`, `sqlite3`, `adb` |
| 10 | `export-audit-json` | `export-audit-json.ps1` | PowerShell + Bruno + Node | API & Massa de Teste | GDF Boticário | `script` (Bash) | `npx @usebruno/cli`, `jq` |
| 11 | `send-json-files` | `send-json-files.ps1` | PowerShell + Bruno | API & Massa de Teste | GDF Boticário | `script` (Bash) | `npx @usebruno/cli` |
| 12 | `sync-items-transform` | `sync-items-transform/*.js` (v1–v5 + response) | Node | API & Massa de Teste | GDF Boticário | `script` (Bash + `jq`), só v5 e response | `jq` |
| 13 | `generate-request-body` | `generate_request_body.py` | Python + numpy + Pillow | API & Massa de Teste | GDF Boticário | `script` (Bash + ImageMagick + `jq`) | `magick`, `jq` |

⚠️ **O `fullpage-screenshot` não tem como ser Bash puro**, porque o Playwright é uma biblioteca Node. Proposta: o `run.sh` chama o Node do próprio Electron (`ELECTRON_RUN_AS_NODE=1`), sem exigir Node instalado. Exceção aprovada (D17).

## 2. Fora da migração (ficam em `_tools`)

| Item | Motivo |
|------|--------|
| `request_body.json`, `request_body_01..04.*` (~125 MB) | Massas de teste geradas; não são ferramentas |
| Pasta e `.zip` "Giovanna Meirelles" | Não é ferramenta; conteúdo não foi aberto |
| `mighty-hml.png` | Imagem solta |
| `_refs/attachIds.txt` | Referência de dados |
| `sync-items-transform/*.json` (refs, respostas) | Dados de exemplo; amostras pequenas podem virar *fixtures* depois |
| `transform-request-v1*.js`, `v4_Completo.js` | Versões antigas substituídas pela v5 (D21) |
| `package.json` / `package-lock.json` de `_tools` | Substituídos pelo `package.json` do Tool Belt |

`sync-items-transform/base64.txt` (1,2 MB) é **insumo** de `export-audit-json` e `sync-items-transform`. Vira um parâmetro de arquivo de imagem, com um *asset* pequeno como padrão em `tools/sync-items-transform/assets/` (D22).

## 3. Segredos e valores fixos a remover

| Valor encontrado | Onde | Vira |
|------------------|------|------|
| `apigeeClientId` HML | `seed-db.ps1`, `export-audit-json.ps1`, `send-json-files.ps1` | Segredo `APIGEE_CLIENT_ID_HML` |
| `apigeeClientId` DEV (comentado) | `export-audit-json.ps1`, `send-json-files.ps1` | Segredo `APIGEE_CLIENT_ID_DEV` |
| E-mail corporativo `livia.xavier.t_alparservice@…` | `transform-request-v5_SemBanco.js` | Segredo `GDF_USER_EMAIL` (é dado pessoal) |
| `C:\Users\livia\Documents\bruno\alpar-boticario-apigee` | 3 scripts `.ps1` | Parâmetro `--collection` (tipo `dir`) com valor padrão nas configurações |
| `C:\Users\livia\_tools\sync-items-transform\…` | `export-audit-json.ps1` | Caminho relativo à pasta da ferramenta |
| `$env:TEMP\…` | vários | `TB_OUT_DIR` |
| `com.boticario.gdfauditoria`, `gdf_boticario.db` | pull/push/seed | Parâmetros com valor padrão no `tool.yaml` |
| `QUESTION_IDS` fixos | `generate_request_body.py` | Parâmetro `--question-id` (lista) |

> ⚠️ Os client IDs do Apigee estão em texto puro em `_tools`. Se essa pasta já foi para algum repositório ou backup compartilhado, vale considerar a rotação.

## 4. Mapeamento de porte (PowerShell/Python/Node → Bash)

| Construção original | Equivalente em Bash |
|---------------------|---------------------|
| `Write-Host -ForegroundColor` | `step`/`log`/`die` de `common.sh` (cores ANSI, `NO_COLOR`) |
| `param(...)` / `argparse` | `while (( $# )); case "$1" in --x) …` + `usage()` |
| `ConvertFrom-Json` / `json` / `JSON.parse` | `jq` |
| `Get-ChildItem -Filter` | `find … -name` / globs com `nullglob` |
| `cmd /c "adb exec-out … > file"` | `adb exec-out "run-as $pkg cat $db" > "$out"` (Git Bash não converte binário; testar) |
| `Read-Host` / "Pressione ENTER" | Removido; confirmação vai para `destructive: true` no manifesto |
| Pillow + numpy (ruído por pixel) | `magick -size WxH xc: +noise Random -quality N out.jpg` |
| `base64` em Python/Node | `base64 -w0` (coreutils do Git Bash) |
| `uuid.uuid4()` / `crypto.randomUUID()` | `cat /proc/sys/kernel/random/uuid` (Linux) ou função em `common.sh` |
| Caminhos Windows | `cygpath -u/-w` dentro de `to_native_path` |

## 5. Ordem de migração

| Onda | Ferramentas | Por quê |
|------|-------------|---------|
| 1 | `git-remote-ssh` | Já está em Bash; valida estrutura, manifesto, runner e testes |
| 2 | `jwt-decoder`, `markdown-to-text`, `html-to-pdf` | Tipo `ui`, sem SO; valida o layout entrada/saída |
| 3 | `pull-app-db`, `push-app-db` | Bash simples; valida o fluxo destrutivo e os pré-requisitos |
| 4 | `sync-items-transform`, `export-audit-json`, `send-json-files`, `seed-db` | Dependem do cofre e do Bruno; formam o guia "Massa de teste GDF" |
| 5 | `git-report`, `generate-request-body`, `fullpage-screenshot` | Portes maiores ou com exceção |

Critério de "migrada": `tool.yaml` válido, `run.sh` passa no shellcheck, teste em Bash com fixtures, README/guia escrito, saída equivalente à da versão original no mesmo cenário.
