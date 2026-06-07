# paperclip-skills

Skills para os agents do Paperclip. **100% técnicas e universais** — nenhuma menção a projeto específico. Os fatos de cada projeto vivem em documentos de contexto (`.md`) separados, não aqui.

Duas camadas:

## `discipline/` — modo de agir (TODOS os agents)
Comportamento, método e princípios que todo agent segue, qualquer que seja a função:

- **investigate-before-acting** — investigar o estado real antes de agir; nunca chutar
- **excellence-over-speed** — sempre a melhor solução pro projeto, custe o que custar; nunca a saída preguiçosa; pensar longo prazo
- **risk-categories-abc** — método de classificar tasks em A/B/C (defaults conservadores, fluxos)
- **production-safety-mindset** — backup, rollback, smoke test, não assumir sucesso
- **secrets-handling** — não expor secrets em artefatos; não policiar o operador
- **decision-and-communication** — opções + recomendação + esperar aprovação; comandos com contexto; tom direto; honestidade

## `expertise/` — excelência por função (só agents que existem hoje)
O que torna cada agent elite na sua especialidade:

- **orchestration-craft** — para o CEO (decomposição, priorização, delegação, estado)
- **strategic-planning** — para o TechLead (Discovery, arquitetura, trade-offs, planos completos)
- **engineering-craft** — para os Engineers (código correto, limpo, sem gambiarra, coeso)
- **code-review-excellence** — para os Reviewers (review profundo, sem rubber-stamp, veredito estruturado)

## Atribuição recomendada

| Agent | discipline/ | expertise/ |
|---|---|---|
| CEO | todas (6) | orchestration-craft |
| TechLead | todas | strategic-planning |
| EngineerA | todas | engineering-craft |
| EngineerB | todas | engineering-craft |
| ReviewerA | todas | code-review-excellence |
| ReviewerB | todas | code-review-excellence |
| ReviewerSenior | todas | code-review-excellence |

## Princípio de separação

- **Skill** = COMO o agent age/pensa/atua (universal, sem projeto específico)
- **Contexto** = FATOS de um projeto (vai em `.md` anexado, ex: `mileto-ia-context.md`)

Quando uma skill precisa de um fato específico (qual é a lista de Categoria C, quais workflows são críticos, quais ambientes existem), ela aponta para "o documento de contexto do projeto" em vez de embutir o fato.

## Skills futuras (backlog)
- `vps-standard-setup` — VPS padrão usada em todos os projetos
- `frontend-mastery`, `backend-mastery`, `n8n-mastery`, `qa-mastery`, `devops-mastery`, `verification-rigor` — ao contratar os respectivos especialistas

## Como adicionar ao Paperclip
Na tela Skills, campo "Paste path, GitHub URL, or skills", cole o caminho da skill e clique Add. Depois atribua aos agents no campo USED BY.
