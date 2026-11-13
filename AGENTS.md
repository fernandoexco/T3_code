# AGENTS.md

Instruções para qualquer agente de IA (Codex, OpenCode, Copilot, Antigravity, Grok, Claude Code etc.).

## O que há neste repositório

Procedimento para configurar o **T3 Code** (app desktop, Windows) para uso remoto pelo celular.

| Arquivo | Conteúdo |
|---|---|
| `skills/t3-code-acesso-remoto/SKILL.md` | Passo a passo completo (fonte principal) |
| `docs/registro-2026-11-12.md` | Registro do que foi feito, decisões e lições |

## Como usar

- Quando o usuário pedir para usar o T3 Code pelo celular, parear, ou configurar T3 Connect/Tailscale: **leia `skills/t3-code-acesso-remoto/SKILL.md` e siga os passos**. O texto é Markdown comum e não depende de nenhuma ferramenta específica; o frontmatter YAML pode ser ignorado por agentes que não usam skills.
- Para contexto histórico, leia `docs/registro-2026-11-12.md`.

## Regras importantes

- **Login (T3 Connect) e instalação do app no celular são feitos pelo usuário.** Nunca digite credenciais.
- **Não altere configurações de energia/sistema do Windows**; passe o comando ao usuário (`powercfg /change standby-timeout-ac 0`).
- Trate links/códigos de pareamento como senhas: não os registre em logs, commits ou screenshots.
- Não inclua dados pessoais (e-mail, nome do computador, IP) em commits ou documentos.

## Copiar a skill para o seu agente (opcional)

- Claude Code: `~/.claude/skills/t3-code-acesso-remoto/`
- Demais agentes: basta apontar para o `SKILL.md` ou colar o conteúdo no contexto.
