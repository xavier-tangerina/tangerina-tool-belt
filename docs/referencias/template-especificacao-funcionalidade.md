# Template — Especificação de funcionalidade

Sep 28, 2026 · @Xavier

Preencha só o que souber; o que faltar vira pergunta na especificação
gerada.

## Como usar

1.  Duplique este documento e dê a ele o nome da funcionalidade.

2.  Preencha os quatro campos obrigatórios. Frases curtas e listas
    bastam; não precisa formatar.

3.  Preencha os opcionais que souber e liste os anexos na última seção.

4.  Numa conversa com o Claude, anexe os arquivos, cole o link deste
    documento e peça: *"Gere a especificação a partir deste template"*.
    Se o repositório estiver acessível, diga a pasta; a parte técnica
    fica bem mais precisa.

5.  O Claude gera um documento novo com Parte A (funcional), Parte B
    (técnica) e Parte C (lacunas e decisões). Responda às dúvidas por
    comentários no próprio documento até a Parte C ficar vazia.

## Campos obrigatórios

| Campo                   | Preencha aqui | Exemplo (Vigilância da Carne)                                                       |
|-------------------------|---------------|-------------------------------------------------------------------------------------|
| Nome da funcionalidade  |               | Rastreamento de ações do usuário                                                    |
| Projeto e repositório   |               | Mighty Earth · mightyearth-vigilanciadacarne                                        |
| Objetivo (1 a 3 frases) |               | Saber quais regiões mobilizam mais e quais redes são mais cobradas e compartilhadas |
| Quem usa                |               | Visitante anônimo; admin do Payload; equipe Mighty Earth no GA4                     |

**O que precisa fazer** (uma linha por item, do jeito que vier à
cabeça):

- 
- 
- 

*Exemplo: "criar enum para sys_action e tags"; "cada ação gera registro
em tb_user_actions e evento no GA4"; "dashboard do admin com regiões
mais acessadas".*

## Campos opcionais

Quanto mais disso vier preenchido, menos perguntas a especificação terá
na Parte C.

| Campo                                             | Preencha aqui | Para que serve                                       |
|---------------------------------------------------|---------------|------------------------------------------------------|
| Regras já conhecidas                              |               | Viram as regras de negócio (RN) da Parte A           |
| Fora de escopo                                    |               | Evita que a especificação cresça além do pedido      |
| Dados e integrações (tabelas, APIs, GA4, e-mail…) |               | Base do modelo de dados e das integrações na Parte B |
| Telas ou relatórios afetados                      |               | Onde instrumentar ou o que desenhar                  |
| Métricas de sucesso                               |               | Viram KPIs e critérios de aceite                     |
| Restrições (prazo, stack, LGPD, orçamento)        |               | Limitam as escolhas técnicas                         |
| Dúvidas que você já tem                           |               | Entram direto na Parte C, com uma proposta           |
| Quem decide / valida                              |               | Preenche a coluna "Decide" das decisões em aberto    |

## Anexos

Liste o que vai anexar na conversa. Fluxogramas, planilhas de eventos,
prints de tela e notas de reunião valem mais que descrições longas.

| Arquivo | O que é | Observação |
|---------|---------|------------|
|         |         |            |
|         |         |            |
|         |         |            |

*Exemplo: system_actions.pdf · planilha de transições entry_point →
sys_action → tag · "a aba 3 é a versão final"; load_region.pdf ·
fluxograma do carregamento com região · "prevalece sobre a planilha em
caso de conflito".*
