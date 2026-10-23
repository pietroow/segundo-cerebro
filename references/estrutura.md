# Estrutura do cofre

Nomes de pasta **sem acento**, de propósito, pra evitar problema de encoding em terminal no Windows.
A numeração mantém a ordem no Obsidian.

## Fluxo 1: o SEU cérebro (onde você pensa)

```
<cofre>/
├── 00 Inbox/            tudo que chega, cru e sem organizar (links, prints, ideias, trechos)
├── 01 Processamento/    o que você está estudando agora (notas de literatura em construção)
├── 02 Topicos/          notas-hub por assunto, que ligam as suas notas
├── 03 Diario/           notas diárias de pensamento
├── 04 Backlog/          registros e ideias soltas pra depois
├── 10 Projetos/         uma subpasta por projeto ativo (tem entrega ou prazo)
│   └── <Projeto>/
├── 20 Recursos/         conhecimento consolidado: suas notas permanentes
├── 30 Sistemas/         seus processos, rotinas e frameworks que você usa de verdade
├── 40 Arquivo/          projetos concluídos e o que saiu de uso
├── 90 Anexos/           imagens e PDFs
├── 99 Templates/        modelos das suas notas
├── Claude/              ← ambiente da IA (Fluxo 2)
└── CLAUDE.md            ← a fronteira (Fluxo 3)
```

Quem escreve: **você**. A IA pode ler (menos as pastas bloqueadas no `CLAUDE.md`), buscar e sugerir.
Criar pastas, hubs vazios e templates é organização, então é permitido com aprovação. Conteúdo autoral, nunca.

> A estrutura vem do PARA (Tiago Forte) + Zettelkasten, como no vídeo de referência, que usa
> Projetos, Recursos, Arquivo e **Sistemas**. Quem preferir o PARA clássico pode acrescentar `15 Areas/`.

### Fluxo de uma ideia no lado seu

```
00 Inbox ──► 01 Processamento ──► 20 Recursos (ou 10 Projetos/<x>)
 (cru)        (literatura: sobre a fonte)   (permanente: a SUA ideia)
                                                   │
                                   02 Topicos/<assunto> linka tudo
```

## Fluxo 2: o ambiente da IA (onde ela trabalha)

```
Claude/
├── 00 Outputs/                 planos, rascunhos, transcrições, entregas, mapas de curadoria
├── 01 Skills/                  índice e documentação das suas skills
├── 02 Logs e Memoria/
│   ├── memoria.md              fatos duráveis (máx. ~150 linhas)
│   ├── onboarding.md           progresso do setup
│   └── logs/AAAA-MM-DD.md      registro de cada sessão relevante
├── 03 Projetos e Specs/        PRDs e planos de implementação
├── 04 Agentes/                 um agente por pasta: instrução + referências + frameworks + processo
├── 05 Templates e Referencias/ modelos que a IA usa (output, log, decisão, ritual de revisão)
├── 06 Decisoes/                decisões e histórico (AAAA-MM-DD-titulo.md)
└── 07 Briefings e Databases/   briefing pessoal, dados de referência, bases pra consulta
```

**Dentro de `Claude/`, autonomia total**: criar, editar, mover, deletar e organizar.
Exceção de bom senso: pedir ok antes de apagar algo que a pessoa ainda não revisou.

### Conteúdo dos `_LEIA.md` (um por pasta)

Crie cada `_LEIA.md` com este formato (título + 2 blocos curtos):

```markdown
# <nome da pasta>

**O que vai aqui:** <linha abaixo>
**Regra:** <linha abaixo>
```

| Pasta | O que vai aqui | Regra |
|---|---|---|
| `00 Outputs` | Entregas da IA: planos, rascunhos, transcrições, materiais e mapas de curadoria sobre as suas notas. | Todo arquivo com `autor: ia`, `status` e `fonte`. Nada daqui vira nota permanente sem você reescrever com as suas palavras. |
| `01 Skills` | Índice das skills que você usa: nome, pra que serve, quando rodar. | As skills ativas ficam em `.claude/skills/`. Aqui fica só a documentação. |
| `02 Logs e Memoria` | `memoria.md` (fatos duráveis) e `logs/` (o que foi feito em cada sessão). | A IA não lembra entre sessões, quem lembra são estes arquivos. Consolidar e podar na revisão semanal. |
| `03 Projetos e Specs` | PRDs, planos de implementação, especificações de projetos que a IA executa. | Um arquivo ou pasta por projeto. Linkar o projeto correspondente em `10 Projetos/` quando existir. |
| `04 Agentes` | Um agente por pasta: `instrucao.md`, `processo.md`, `referencias/` e frameworks. | Um bom agente é mais que uma instrução. Revisar os outputs dele antes de confiar. |
| `05 Templates e Referencias` | Modelos que a IA usa (output, log, decisão, ritual de revisão) e referências recorrentes. | Mudou um formato? Mude aqui, e ele vale pra todas as próximas vezes. |
| `06 Decisoes` | Decisões importantes e o porquê delas (`AAAA-MM-DD-titulo.md`). | Registrar o contexto, a decisão e o que foi descartado. Nunca apagar, só marcar como substituída. |
| `07 Briefings e Databases` | Briefing pessoal, briefings de clientes e projetos, bases de dados de referência. | Manter atualizado. Briefing velho gera output errado. |

## Fluxo 3: a fronteira

Vive no `CLAUDE.md` da raiz (template em `templates/CLAUDE.template.md`).

## Tipos de nota e frontmatter

| `tipo` | `autor` | Onde fica | Quem escreve |
|---|---|---|---|
| `inbox` | `eu` | `00 Inbox/` | você (ou a IA registrando o que você passou, sem mudar nada) |
| `literatura` | `eu` | `01 Processamento/` e depois junto da permanente | **você** |
| `permanente` | `eu` | `20 Recursos/`, `10 Projetos/<x>/`, `30 Sistemas/` | **você** |
| `topico` | `eu` | `02 Topicos/` | você; a IA adiciona links com aprovação |
| `diario` | `eu` | `03 Diario/` | **você** |
| `briefing` | `eu` | `Claude/07 Briefings e Databases/` | você (respostas transcritas literalmente) |
| `curadoria` | `ia` | `Claude/00 Outputs/` | IA, **sobre** as suas notas |
| `output` | `ia` | `Claude/00 Outputs/` | IA |

Campos:

```yaml
---
tipo: permanente        # inbox | literatura | permanente | topico | diario | briefing | curadoria | output
autor: eu               # eu | ia
criado: 2026-09-15
fonte: "[[...]]"        # de onde veio (URL, livro, nota)
status: rascunho        # só autor: ia -> rascunho | aprovado | descartar
topicos: ["[[Assunto]]"]
---
```

**Checagem da fronteira:** qualquer nota **fora** de `Claude/` com `autor: ia` é uma violação e deve aparecer na revisão.
