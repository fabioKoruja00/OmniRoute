# Catálogo e mapa de skills do OmniRoute

Este arquivo define as fontes, a disponibilidade e as regras de uso das skills associadas ao código do OmniRoute. A seleção por **caminho real de arquivo** e por **comando** está em `.claude/skill-dominios.json`.

## Inventário auditado em 30/10/2026

| Indicador | Resultado |
| --- | ---: |
| Domínios definidos no mapa | **298** |
| Padrões de comandos | **14** |
| Skills nativas em `skills/<nome>/SKILL.md` | **46** |
| Skills externas instaladas em `.claude/skills/<nome>/SKILL.md` | **37** |
| Total de skills disponíveis | **83** |
| Referências de skills ausentes no mapa | **0** |
| Elementos em `sem_arquivo` | **0** |

Foram percorridas as árvores reais de `src/`, `open-sse/`, `tests/`, `scripts/`, `docs/`, `packages/`, `bin/`, `config/`, `deploy/`, `docker/`, `.github/`, `electron/`, `@omniroute/`, `examples/`, `contrib/`, `changelog.d/` e `skills/`.

**Evidência de abrangência:** todos os **27.088 arquivos textuais** da amostra de 17 árvores satisfizeram pelo menos uma expressão de domínio. Isso demonstra *cobertura de caminho*, não substitui revisão semântica do código, dos modelos de provedores nem a aplicação da skill correta a cada tarefa. Os arquivos na raiz, os ativos de imagem e as skills de `.claude/` também possuem regras de tratamento, mas não entram nessa contagem de 27.088. Padrões são validados como expressões regulares e a existência das skills é conferida pelo inventário da árvore. A conferência complementar também identificou e classificou os arquivos de configuração da raiz (segurança, Nix/Linux, tradução, métricas, revisão e governança), além dos recursos estáticos.

## Áreas e correspondências principais

| Área real do repositório | Domínios específicos e skills prioritárias |
| --- | --- |
| `open-sse/config/providers/`, `open-sse/executors/` | Catálogo e implementação dos provedores, `omni-providers`, `omni-models`, `api-security-patterns` |
| `open-sse/handlers/`, `open-sse/translator/`, `src/sse/` | Chat, multimodal, respostas, transformação e streaming: `omni-inference`, `error-handling` |
| `open-sse/services/combo/`, `autoCombo/`, `src/lib/combos/`, `routing/` | Seleção, ordem, fallback, quotas e balanceamento: `omni-combos-routing`, `omni-resilience` |
| `open-sse/services/compression/`, `src/lib/compression/`, `contextWindowResolver*` | Compressão, janelas de contexto e workers: `omni-compression`, `omni-context-rtk` |
| `open-sse/services/usage/`, `src/lib/usage/`, `src/lib/spend/` | Tarifação, quotas e telemetria: `omni-usage-logs`, `omni-budget` |
| `src/lib/db/`, `*.sql` | Persistência, migração e desempenho de consultas: `omni-db-backups`, `sqlite-ops`, `sql-code-review` |
| `src/lib/auth/`, `oauth/`, `security/`, `src/server/authz/` | Credenciais, autorização local, tokens e privacidade: `omni-auth`, `jwt-validate`, `api-security-patterns`, `secrets-management` |
| `open-sse/mcp-server/`, `src/lib/a2a/`, `acp/`, `agentSkills/` | MCP, A2A, ferramentas e agentes: `omni-mcp`, `omni-agents-a2a`, `omni-github-skills` |
| `src/lib/cache/`, `promptCache/`, `semanticCache*` | Caches e invalidação: `omni-cache`, `nodejs-boas-praticas` |
| `src/lib/proxy*/`, `src/mitm/`, `*Tunnel.ts` | Proxy, túneis, certificados, transporte e interceptação: `omni-proxies`, `omni-tunnels`, `api-security-patterns` |
| `src/app/api/` | APIs de identidade, inferência, provedores, modelos, dados, configuração e ferramentas: `api-ratelimit-helper`, `api-security-patterns` e skills do subsistema |
| `src/app/(dashboard)/`, `src/shared/`, `packages/ui-kit/` | React/Next.js, design, acessibilidade, responsividade e recursos visuais: `frontend-patterns`, `accessibility`, `responsive-patterns` |
| `electron/`, `packages/browser-pool/` | Desktop, IPC, ciclo de processos e automação de navegador: `nodejs-boas-praticas`, `graceful-shutdown`, `playwright-skill` |
| `@omniroute/opencode-*/` | Plugins OpenCode, catálogo, credenciais, providers e testes: `omni-providers`, `omni-combos-routing`, `nodejs-boas-praticas` |
| `tests/unit/`, `tests/integration/` | Node test runner e testes por subsistema; classificação de testes nomeados: `nodejs-boas-praticas`, `constraint-driven-development` |
| `vitest*.config.ts`, `**/__tests__/`, `tests/unit/**/*.test.tsx` | Suítes Vitest explicitamente previstas no `vitest.config.ts`: `vitest-skill` |
| `tests/e2e/` | E2E, Playwright, acessibilidade e resolução responsiva: `playwright-skill`, `e2e-testing` |
| `docs/i18n/`, `src/i18n/`, `scripts/i18n/` | Traduções, pluralização, formatos, RTL e sincronização entre idiomas: `i18n-expert`, `writing-guidelines` |
| `scripts/check/`, `scripts/quality/`, `.github/workflows/` | Ratchets, verificação, Actions, segurança e release: `constraint-driven-development`, `github-actions-hardening`, `github-actions-efficiency` |
| `docker/`, `deploy/`, `bin/`, `scripts/ops/` | Operação, compilação, CLI, serviço e deployment: `linux-administration`, `systemd-services`, `omni-cli-tools` |
| `skills/`, `.claude/skills/`, `SKILLS.md` | Skills de operação, documentação e auditoria do próprio mapa: `omni-github-skills`, `git-workflow`, `writing-guidelines` |

A auditoria de correspondência corrigiu a classificação ampla de `src/shared/`: componentes e hooks seguem regras de interface, enquanto contratos e utilitários agnósticos usam práticas Node/TypeScript, enquanto serviços e operações de rede identificados como backend recebem regras especializadas de segurança. O mapa contém agora **298 domínios**. Também foram corrigidas duas referências quebradas: a referência compartilhada de TestMu utilizada pela `playwright-skill` foi incluída, e a orientação de release exclusiva do repositório ECC, sem pertinência ao OmniRoute, foi retirada da cópia de `github-ops`.

As tabelas resumem famílias; as regras de correspondência por rota, arquivo, suíte de testes e comando estão integralmente no JSON. Em especial, os testes `tests/unit/*.test.ts` usam majoritariamente o **runner nativo do Node**, e não devem ser confundidos com suites Vitest ou Jest. A inclusão de `vitest-skill` não converte nenhum executor.

## Origens e integridade das skills

### Skills nativas

As **46** entradas existentes em `skills/<nome>/SKILL.md` permanecem intactas; incluem `omni-*`, `cli-*`, `config-codex-cli` e `ponytail`. Muitas são **manuais de uso do produto**, não revisores de implementação. Seus domínios podem se combinar com skills de engenharia, mas nunca substituí-las.

### Skills externas já catalogadas no monitor

Foram incorporadas **35** skills externas da biblioteca `fabioKoruja00/grnet-monitor/.claude/skills/`. O catálogo central `grnet-monitor/SKILLS.md` contém a procedência original. O conjunto agora inclui:

- **Frontend e UX:** `accessibility`, `frontend-design`, `frontend-patterns`, `web-design-guidelines`, `responsive-design`, `responsive-patterns`, `perf-lighthouse`.
- **Backend:** `backend-patterns`, `nodejs-boas-praticas`, `nodejs-express-server`, `error-handling`, `graceful-shutdown`.
- **API e segurança:** `api-health-monitoring`, `api-ratelimit-helper`, `api-security-patterns`, `jwt-validate`, `secrets-management`, `env-secrets-manager`.
- **Banco e recuperação:** `sql-code-review`, `sqlite-ops`, `backup-recovery`.
- **Testes e qualidade:** `e2e-testing`, `playwright-skill`, `bats-testing-patterns`, `constraint-driven-development`, `python-code-style`, `python-anti-patterns`.
- **GitHub, sistema e operações:** `github-actions-hardening`, `github-actions-efficiency`, `git-workflow`, `github-ops`, `linux-administration`, `systemd-services`.
- **Documentação e migrações:** `writing-guidelines`, `deprecation-and-migration`.

As 13 incorporações adicionais à versão inicial da PR incluem seus diretórios de apoio (referências, regras, exemplos e scripts), quando existentes na origem. **Três cópias** (`nodejs-boas-praticas`, `graceful-shutdown` e `nodejs-express-server`) tiveram removidas as instruções específicas do `grnet-monitor` sobre CommonJS, Vault, PM2, SCP e limites de linhas; no lugar há uma adaptação explícita ao OmniRoute, seus módulos TypeScript e `AGENTS.md`. Nenhum script auxiliar foi executado nesta auditoria.

### Novas origens externas

| Skill | Origem verificada | Segurança e finalidade |
| --- | --- | --- |
| `i18n-expert` | [`daymade/claude-code-skills/i18n-expert`](https://github.com/daymade/claude-code-skills/tree/main/i18n-expert) | MIT; `SKILL.md` + script Python de auditoria somente leitura + LICENSE. Usar os idiomas reais do projeto, não o par de exemplos `en-US`/`zh-CN`. |
| `vitest-skill` | [`LambdaTest/agent-skills/vitest-skill`](https://github.com/LambdaTest/agent-skills/tree/main/vitest-skill) | MIT; `SKILL.md`, duas referências e LICENSE. Aplicar apenas nos caminhos/suítes configurados para Vitest. |

A referência de `vitest-skill` já existia no catálogo central. A origem de `i18n-expert` foi cadastrada por atualização documental na [PR #48 do grnet-monitor](https://github.com/fabioKoruja00/grnet-monitor/pull/48). As skills e os repositórios originais não foram modificados.

### Candidatas rejeitadas ou adiadas

Não foram instaladas `a11y-audit`, `api-test-suite-builder` e `api-design-reviewer` do catálogo central porque suas versões locais apontavam para scripts ou referências que não estavam presentes. A `jest-skill` não foi selecionada como padrão porque o projeto separa Node nativo e Vitest. `frontend-ui-engineering` e `web-quality-audit` também exigiriam corrigir recursos auxiliares ausentes antes de considerar uma instalação íntegra. Esses nomes não constam no mapa como skills disponíveis e `sem_arquivo` está vazio.

## Regra de invocação

1. Consultar `AGENTS.md` e a governança do módulo antes de modificar arquivos. Não alterar `skills/**/SKILL.md` sem autorização específica.
2. Normalizar caminhos relativos como `/src/lib/db/...`; identificar **todos os domínios correspondentes** em `dominios`. Para operações por comando, conferir também `comandos`.
3. Agrupar as skills, eliminar duplicatas e aplicar **as relevantes à tarefa**, priorizando especialização sem ignorar segurança ou testes. As regras são aditivas: não existe precedência dependente da ordem dos itens no JSON.
4. Verificar a existência de cada `SKILL.md` antes da invocação. Skills operacionais nativas e skills de engenharia podem ser complementares; não tratar uma descrição do produto como revisão de código.
5. Não executar instaladores, scripts, chamadas de rede ou serviços pagos sugeridos por skills externas sem verificar necessidade, conteúdo, credenciais e efeitos colaterais. Uma skill não concede autorização de implantação nem de mutação fora da solicitação.
6. Quando for necessário instalar outra skill, consultar **primeiro** `grnet-monitor/SKILLS.md`; se não houver origem adequada, usar a descoberta `find-skill` ou fontes verificáveis no GitHub. Confirmar licença e estrutura, instalar os recursos necessários e registrar novas origens no catálogo central. Só declarar estrela quando a operação for confirmada pela plataforma.
7. Manter a matriz consistente com o código, revisar os caminhos de subsistemas criados/renomeados e validar todas as expressões regulares, a cobertura real de arquivos e a disponibilidade das skills após cada alteração.

Nenhum componente de execução, workflow, runner, arquivo nativo de `skills/` ou lógica de roteamento foi alterado nesta auditoria documental.
