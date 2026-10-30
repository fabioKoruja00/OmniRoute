# Catálogo de skills e domínios do OmniRoute

O mapeamento por caminho de código está em `.claude/skill-dominios.json`, seguindo o formato do `grnet-monitor`. Cada padrão corresponde a caminhos iniciados por `/`, e múltiplos domínios podem se aplicar ao mesmo arquivo.

## Fontes e disponibilidade

- **Skills nativas:** `skills/<nome>/SKILL.md`. Estão versionadas no OmniRoute e são usadas como referência funcional para a API, CLI, MCP, roteamento e demais módulos. Não são, por si só, ferramentas de revisão de implementação.
- **Skills externas referenciadas:** consulte `sem_arquivo` no mapa. Essas referências **existem no catálogo central** `fabioKoruja00/grnet-monitor/.claude/skills/`, mas **ainda não foram copiadas ao OmniRoute**. Não se deve afirmar que foram instaladas ou executadas aqui.

| Skill externa referenciada | Origem central |
| --- | --- |
| `frontend-patterns` | `grnet-monitor/.claude/skills/frontend-patterns/SKILL.md` |
| `a11y-audit` | `grnet-monitor/.claude/skills/a11y-audit/SKILL.md` |
| `nodejs-boas-praticas` | `grnet-monitor/.claude/skills/nodejs-boas-praticas/SKILL.md` |
| `error-handling` | `grnet-monitor/.claude/skills/error-handling/SKILL.md` |
| `jest-skill` | `grnet-monitor/.claude/skills/jest-skill/SKILL.md` |
| `api-test-suite-builder` | `grnet-monitor/.claude/skills/api-test-suite-builder/SKILL.md` |
| `constraint-driven-development` | `grnet-monitor/.claude/skills/constraint-driven-development/SKILL.md` |
| `github-actions-hardening` | `grnet-monitor/.claude/skills/github-actions-hardening/SKILL.md` |
| `github-actions-efficiency` | `grnet-monitor/.claude/skills/github-actions-efficiency/SKILL.md` |
| `github-ops` | `grnet-monitor/.claude/skills/github-ops/SKILL.md` |
| `git-workflow` | `grnet-monitor/.claude/skills/git-workflow/SKILL.md` |
| `linux-administration` | `grnet-monitor/.claude/skills/linux-administration/SKILL.md` |
| `secrets-management` | `grnet-monitor/.claude/skills/secrets-management/SKILL.md` |
| `writing-guidelines` | `grnet-monitor/.claude/skills/writing-guidelines/SKILL.md` |

## Auditoria ampliada (30/10/2026)

A árvore verificada contém 46 skills nativas em `skills/` (incluindo 22 skills de CLI e a skill `ponytail`), que possuem finalidades de operação do produto; elas não substituem skills de engenharia. O mapa foi ampliado para contemplar comandos CLI, agentes, internacionalização, testes de integração, segurança, scripts operacionais, backend e UI. O catálogo central do monitor foi consultado antes da seleção externa.

**Skills adicionais copiadas e verificadas do monitor:** `git-workflow`, `github-ops`, `writing-guidelines`, `backend-patterns`, `error-handling`, `frontend-patterns`, `accessibility`, `e2e-testing`, `secrets-management`, `sql-code-review`, `jwt-validate`, `linux-administration`, `api-health-monitoring`, `api-ratelimit-helper`, `api-security-patterns`, `deprecation-and-migration`, `perf-lighthouse`, `backup-recovery`, `python-code-style`, `python-anti-patterns`, `web-design-guidelines`, `frontend-design`.

**Verificação de origem e ressalvas:** essas cópias provêm das versões já catalogadas em `grnet-monitor/.claude/skills/`; antes de executar quaisquer scripts ou comandos, consultar as instruções e revisar efeitos colaterais. A cópia de `api-ratelimit-helper` e `api-security-patterns` tem seu campo `name` corrigido para coincidir com a pasta. Skills com dependências de arquivos adicionais ainda não integradas permanecem em `sem_arquivo`. Uma skill de uso do produto não deve ser tratada automaticamente como validação de implementação.

## Uso e governança

1. Identificar o domínio pelo caminho no mapa; consultar os `SKILL.md` efetivamente disponíveis, em `skills/` e, quando instalados, `.claude/skills/`.
2. Respeitar primeiro o `AGENTS.md`, as instruções locais de cada módulo, o fluxo de testes e a revisão independente. As skills não concedem permissão automática para alterar código.
3. O mapa contém referências em `sem_arquivo` para registrar lacunas com transparência. **Não usar** uma skill referenciada que ainda não esteja instalada.
4. Antes de baixar nova skill, consultar o catálogo central `grnet-monitor/SKILLS.md`. Se não houver recurso adequado, usar `find-skill` para localizar fontes. Verificar segurança, licença e conteúdo antes da instalação.
5. Toda nova instalação exige origem registrada no `SKILLS.md` central. Se houver recurso autorizado para favoritar o repositório de origem no GitHub, registrar a estrela; não declarar estrela sem confirmação da plataforma.

O mapeamento não modifica as skills de produto em `skills/` e não altera a lógica de execução do OmniRoute.
