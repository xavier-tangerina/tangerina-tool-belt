# Registro de decisões

Formato: uma linha por decisão. Mudar uma decisão = nova linha que **substitui** a anterior (nunca apagar).

| # | Data | Decisão | Alternativas consideradas | Quem decidiu |
|---|------|---------|---------------------------|--------------|
| D01 | 30/10/2026 | Projeto em `C:\Users\livia\_code\tangerina\tool-belt` | Ao lado de `_tools`; dentro de `_tools` | Xavier |
| D02 | 30/10/2026 | Ferramentas **migram para dentro do repositório** (`tools/<id>/`); `_tools` vira legado | Ler `_tools` no lugar; híbrido | Xavier |
| D03 | 30/10/2026 | **Portar tudo para `.sh` já** (PowerShell, Python e Node), com exceções técnicas em P1 | *Wrapper* `.sh` agora e porte depois; só ferramentas novas | Xavier |
| D04 | 30/10/2026 | Público: **uso pessoal agora, equipe depois**, com arquitetura pronta para equipe | Só pessoal; equipe desde já | Xavier |
| D05 | 30/10/2026 | Criar ferramentas por **formulário, importação e IA** (os três modos) | Apenas um modo | Xavier |
| D06 | 30/10/2026 | Guia = **doc por ferramenta + guia por categoria + biblioteca de specs** | — | Xavier |
| D07 | 30/10/2026 | Visual com a **marca Tangerina Tech** (`#0d0d0d`, `#FF6A00`, Space Grotesk/Figtree), temas claro e escuro | Neutro dev-tool; identidade própria | Xavier |
| D08 | 30/10/2026 | Ferramenta 01 entrega **copiar, `.md` e pacote com anexos** | Uma saída só | Xavier |
| D09 | 30/10/2026 | Documentação em **Markdown no repositório + espelho no Project** do claude.ai | Só repo; Docs do claude.ai | Xavier |
| D10 | 30/10/2026 | Segredos no **cofre do SO** (Electron `safeStorage`) | `.env` fora do git; manter como está | Xavier |
| D11 | 30/10/2026 | Next.js + Electron via **`next-electron-rsc`** | Static export + IPC (plano B); Nextron | Xavier |
| D12 | 30/10/2026 | Ferramentas HTML **reescritas em React** | Embutir em *webview*; embutir e reescrever depois | Xavier |
| D13 | 30/10/2026 | IA com **Claude Code CLI e Claude API, configurável** | Só CLI; só API | Xavier |
| D14 | 30/10/2026 | Itens que não são ferramentas **ficam em `_tools`** (massas, conversa, imagens) | Virar *fixtures*; decidir item a item | Xavier |
| D15 | 30/10/2026 | Template da Ferramenta 01 = `.docx` enviado, convertido em `docs/referencias/` | Template criado a partir da skill | Xavier |
| D16 | 30/10/2026 | Campo obrigatório vazio **não bloqueia** a geração do template (segue a instrução "o que faltar vira pergunta") | Bloquear até preencher | Xavier (proposta aceita, P8) |
| D17 | 30/10/2026 | Exceção ao "tudo em `.sh`": `fullpage-screenshot` usa `run.sh` + Node do próprio Electron (`ELECTRON_RUN_AS_NODE=1`) | Exigir Node instalado; reescrever sem Playwright | Xavier (P1) |
| D18 | 30/10/2026 | Dependências **ImageMagick** e **`jq`** aceitas (instaláveis via `winget`), checadas na tela de pré-requisitos | Manter Python/Pillow | Xavier (P2) |
| D19 | 30/10/2026 | `git_report.py` portado para **Bash**, com template HTML em arquivo separado | Exceção em Python | Xavier (P3) |
| D20 | 30/10/2026 | Scripts exigem **Bash 4+**; no macOS o app avisa e mostra como instalar (Homebrew) | Compatibilidade com Bash 3.2 | Xavier (P4) |
| D21 | 30/10/2026 | `sync-items-transform`: migram só a **v5 (SemBanco)** e o `transform-response`; v1–v4 ficam em `_tools` como legado | Migrar todas as versões | Xavier (P5) |
| D22 | 30/10/2026 | `base64.txt` vira **parâmetro de arquivo de imagem**, com um *asset* pequeno como padrão | Copiar o arquivo de 1,2 MB como *asset* | Xavier (P6) |
| D23 | 30/10/2026 | Gerenciador de pacotes **pnpm**, com `node-linker=hoisted` se o empacotamento do Electron exigir | npm | Xavier (P7) |
| D24 | 30/10/2026 | Pasta padrão dos pacotes de especificação: **`Documentos\ToolBelt\specs\`**, configurável | `docs/specs/` no repo do projeto informado | Xavier (P9) |
| D25 | 30/10/2026 | `git init` em `tool-belt` já; remoto **privado na conta Tangerina** | Conta pessoal; sem versionamento por ora | Xavier (P10) |
