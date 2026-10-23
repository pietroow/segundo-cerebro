# Segundo Cérebro com IA + Obsidian

Uma skill que monta e opera um segundo cérebro em que **a IA é a bibliotecária, nunca a autora**.
Ela organiza, você pensa. Funciona com o **Claude Code** e com o **Codex**.

- **O seu espaço** (as suas notas) a IA lê, busca e sugere links, mas não escreve.
- **O espaço da IA** (a pasta `_agents/`, dentro do seu cofre) ela usa com autonomia: outputs, logs, memória, decisões.
- **A fronteira** entre os dois fica escrita num `AGENTS.md` na raiz do cofre. O Codex lê esse arquivo direto;
  para o Claude Code, a skill cria um `CLAUDE.md` de uma linha (`@AGENTS.md`) que importa as mesmas regras.

A skill conduz tudo com uma pergunta por vez. Você pode responder falando, por ditado de voz.

## Dois pontos de partida

Na primeira vez que você roda, a skill pergunta por onde começar:

| Caminho | Pra quem | O que ela faz |
|---|---|---|
| **Cofre do zero** | quem está começando | setup completo: pastas, a pasta da IA, a fronteira, o primeiro ciclo com uma nota sua e o ritual de revisão (40–60 min) |
| **Só a fronteira** | quem já tem um cofre do Obsidian organizado | cria a pasta `_agents/` e o `AGENTS.md` com as regras, **sem mover, renomear ou editar nenhuma nota sua** (15–20 min) |

## O que você precisa

- Um agente de IA que rode na sua máquina: **Claude Code** (terminal ou aba *Code* do app desktop do Claude, plano Pro ou Max)
  ou **Codex** (plano do ChatGPT que inclua o Codex)
- **Obsidian** (grátis, [obsidian.md](https://obsidian.md)). Recomendado, mas opcional: são só arquivos markdown

## Instalar

A pasta da skill tem que ficar na pasta de skills do seu agente, com o `SKILL.md` direto dentro dela:

| Agente | Mac / Linux | Windows |
|---|---|---|
| Claude Code | `~/.claude/skills/segundo-cerebro/` | `C:\Users\<seu-usuario>\.claude\skills\segundo-cerebro\` |
| Codex | `~/.codex/skills/segundo-cerebro/` | `C:\Users\<seu-usuario>\.codex\skills\segundo-cerebro\` |

**Com git** (exemplo para o Claude Code; para o Codex, troque `.claude` por `.codex`):

```bash
# Mac / Linux
git clone https://github.com/pietroow/segundo-cerebro ~/.claude/skills/segundo-cerebro
```

```powershell
# Windows (PowerShell)
git clone https://github.com/pietroow/segundo-cerebro "$HOME\.claude\skills\segundo-cerebro"
```

**Sem git:** em *Code → Download ZIP*, extraia, renomeie a pasta `segundo-cerebro-main` para `segundo-cerebro`
e copie para o destino da tabela.

> As pastas `.claude` e `.codex` são ocultas. Se ela ou a `skills` não existirem, crie.
> Windows: Explorador de Arquivos → Exibir → Mostrar → Itens ocultos. Mac: no Finder, `Cmd + Shift + .`

## Usar

1. Abra o agente **dentro da pasta do seu cofre** (no app desktop do Claude, escolha essa pasta como diretório de trabalho).
   Isso importa: as regras do cofre só são carregadas quando o agente é aberto nessa pasta.
2. Rode:

   ```
   /segundo-cerebro
   ```

Dá pra parar quando quiser. Rode `/segundo-cerebro` de novo e ela continua de onde parou.

## Depois do setup

| Comando | Quando usar |
|---|---|
| `/segundo-cerebro processar` | transformar um item do Inbox em nota sua |
| `/segundo-cerebro conectar <tema>` | ver o que você já sabe sobre um tema, as lacunas e a ordem de estudo |
| `/segundo-cerebro revisar` | revisão semanal (20 min) |
| `/segundo-cerebro status` | ver a saúde do sistema |

## Problemas comuns

- **`/segundo-cerebro` não aparece:** confira se o `SKILL.md` está direto em `.../skills/segundo-cerebro/SKILL.md`,
  e não numa pasta a mais (tipo `segundo-cerebro/segundo-cerebro-main/`). Feche e abra o agente de novo.
- **A IA escreveu numa nota minha:** confira se você abriu o agente na pasta do cofre (onde estão o `AGENTS.md` e o `CLAUDE.md`).
  Rode `/segundo-cerebro revisar`: ele encontra notas fora de `_agents/` com `autor: ia`.

## Créditos

A metodologia dos três fluxos vem do vídeo "Segundo Cérebro com IA: Ganhe SUPER-PODERES (Claude Code + Obsidian)",
do canal **Ana Jords**. Os nomes das pastas, as fases e a skill são adaptação de **Pietro Reis**, criada para a
turma Moonlight Expert e apresentada no GDG Londrina 2026.
