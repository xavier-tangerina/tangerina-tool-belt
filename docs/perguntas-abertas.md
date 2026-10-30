# Perguntas em aberto

Status: **0 perguntas abertas.** Em 30/10/2026 todas as propostas foram aceitas e registradas como decisões (D16 a D25 em [decisoes.md](decisoes.md)). Nada bloqueia o início da fase 1.

| # | Pergunta | Proposta | Bloqueia | Status |
|---|----------|----------|----------|--------|
| P1 | O `fullpage-screenshot` depende do Playwright (Node). Aceita exceção ao "tudo em `.sh`": `run.sh` chamando o Node do próprio Electron? | Sim: `run.sh` + `ELECTRON_RUN_AS_NODE=1`, sem Node instalado | Onda 5 | Resolvida: proposta aceita → D17 |
| P2 | O porte do `generate_request_body.py` troca Pillow/numpy por **ImageMagick** e o JSON por **`jq`**. Aceita essas duas dependências (instaláveis via `winget`)? | Sim; checadas na tela de pré-requisitos | Ondas 4–5 | Resolvida: proposta aceita → D18 |
| P3 | O `git_report.py` (27 KB, gera HTML) em Bash puro fica longo. Portar mesmo assim ou abrir exceção como a P1? | Portar para Bash com template HTML em arquivo separado | Onda 5 | Resolvida: proposta aceita → D19 |
| P4 | O macOS vem com Bash 3.2. Exigir Bash 4+ (Homebrew) ou escrever scripts compatíveis com 3.2? | Exigir Bash 4+; o app avisa e mostra como instalar | Fase 4 | Resolvida: proposta aceita → D20 |
| P5 | Do `sync-items-transform`, migrar só a **v5 (SemBanco)** e o `transform-response`? As v1–v4 ficam como legado? | Sim | Onda 4 | Resolvida: proposta aceita → D21 |
| P6 | O `base64.txt` (1,2 MB, imagem de anexo) vai como *asset* da ferramenta ou vira parâmetro "arquivo de imagem"? | Parâmetro de arquivo, com um *asset* pequeno como padrão | Onda 4 | Resolvida: proposta aceita → D22 |
| P7 | Gerenciador de pacotes: **pnpm** ou **npm**? | pnpm (mais rápido), com `node-linker=hoisted` se o empacotamento do Electron exigir; npm se preferir zero configuração | **Fase 1** | Resolvida: proposta aceita → D23 |
| P8 | Confirmar D16: campo obrigatório vazio não bloqueia a geração do template | Confirmar | Ferramenta 01 | Resolvida: proposta aceita → D16 |
| P9 | Pasta padrão dos pacotes de especificação | `Documentos\ToolBelt\specs\` (configurável); alternativa: `docs/specs/` dentro do repo do projeto informado | **Ferramenta 01** | Resolvida: proposta aceita → D24 |
| P10 | Versionamento: iniciar `git` em `tool-belt` agora? Remoto em GitHub ou Bitbucket, em qual conta (pessoal ou Tangerina)? | `git init` já; remoto privado na conta Tangerina | Fase 1 | Resolvida: proposta aceita → D25 |

## Riscos para acompanhar

- Os client IDs do Apigee estão em texto puro em `_tools` (veja doc 05, seção 3).
- O `next-electron-rsc` tem um mantenedor só; há um spike de streaming previsto (doc 04, seção 5).
