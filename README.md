# Segundo Cérebro com Claude Code + Obsidian

Uma skill do Claude Code que monta e opera um segundo cérebro em que **a IA é a bibliotecária, nunca a autora**.
Ela organiza, você pensa.

- **O seu espaço** (as suas notas) a IA lê, busca e sugere links, mas não escreve.
- **O espaço da IA** (a pasta `Claude/`, dentro do seu cofre) ela usa com autonomia: outputs, logs, memória, decisões.
- **A fronteira** entre os dois fica escrita num `CLAUDE.md` na raiz do cofre.

A skill conduz tudo com uma pergunta por vez. Você pode responder falando, por ditado de voz.

## Dois pontos de partida

Na primeira vez que você roda, a skill pergunta por onde começar:

| Caminho | Pra quem | O que ela faz |
|---|---|---|
| **Cofre do zero** | quem está começando | setup completo: pastas, a pasta da IA, a fronteira, o primeiro ciclo com uma nota sua e o ritual de revisão (40–60 min) |
| **Só a fronteira** | quem já tem um cofre do Obsidian organizado | cria a pasta `Claude/` e o `CLAUDE.md` com as regras, **sem mover, renomear ou editar nenhuma nota sua** (15–20 min) |

## O que você precisa

- **Claude Code**, no terminal ou na aba *Code* do app desktop do Claude, com um plano pago (Pro ou Max)
- **Obsidian** (grátis, [obsidian.md](https://obsidian.md)). Recomendado, mas opcional: são só arquivos markdown

## Instalar

A pasta da skill tem que ficar em `.claude/skills/segundo-cerebro/`, com o `SKILL.md` direto dentro dela.

**Com git:**

```bash
# Mac / Linux
git clone https://github.com/pietroow/segundo-cerebro ~/.claude/skills/segundo-cerebro
```

```powershell
# Windows (PowerShell)
git clone https://github.com/pietroow/segundo-cerebro "$HOME\.claude\skills\segundo-cerebro"
```

**Sem git:** em *Code → Download ZIP*, extraia e renomeie a pasta `segundo-cerebro-main` para `segundo-cerebro`.
Depois copie para:

| Sistema | Destino |
|---|---|
| Windows | `C:\Users\<seu-usuario>\.claude\skills\segundo-cerebro\` |
| Mac / Linux | `~/.claude/skills/segundo-cerebro/` |

> A pasta `.claude` é oculta. Se ela ou a `skills` não existirem, crie.
> Windows: Explorador de Arquivos → Exibir → Mostrar → Itens ocultos. Mac: no Finder, `Cmd + Shift + .`

## Usar

1. Abra o Claude Code **dentro da pasta do seu cofre** (no app desktop, escolha essa pasta como diretório de trabalho).
   Isso importa: o `CLAUDE.md` com as regras só é carregado quando o Claude é aberto nessa pasta.
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

- **`/segundo-cerebro` não aparece:** confira se o `SKILL.md` está em `.claude/skills/segundo-cerebro/SKILL.md`,
  e não numa pasta a mais (tipo `segundo-cerebro/segundo-cerebro-main/`). Feche e abra o Claude Code de novo.
- **A IA escreveu numa nota minha:** confira se você abriu o Claude Code na pasta do cofre (onde está o `CLAUDE.md`).
  Rode `/segundo-cerebro revisar`: ele encontra notas fora de `Claude/` com `autor: ia`.

## Créditos

A metodologia dos três fluxos vem do vídeo "Segundo Cérebro com IA: Ganhe SUPER-PODERES (Claude Code + Obsidian)",
do canal **Ana Jords**. Os nomes das pastas, as fases e a skill são adaptação de **Pietro Reis**, criada para a
turma Moonlight Expert e apresentada no GDG Londrina 2026.
