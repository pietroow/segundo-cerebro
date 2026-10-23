---
name: segundo-cerebro
description: Monta e opera um Segundo Cérebro com Obsidian e um agente de IA (Claude Code, Codex ou outro que leia AGENTS.md) seguindo a metodologia dos 3 fluxos (seu cérebro, ambiente da IA, fluxo integrado), de forma guiada, uma pergunta por vez. Use quando pedirem "montar meu segundo cérebro", "second brain", "configurar obsidian com claude", "começar meu cofre", "/segundo-cerebro". Modos - sem argumento faz o setup guiado (retomável de onde parou), e na primeira vez pergunta o ponto de partida: cofre do zero ou só criar a fronteira da IA num cofre que já existe; `processar` transforma um item do Inbox em nota sua através de perguntas; `conectar <tema>` usa a IA como bibliotecária pra mapear o que você já sabe; `revisar` roda a manutenção semanal; `status` mostra a saúde do sistema. A IA nunca escreve suas notas autorais - ela pergunta, transcreve suas palavras e organiza.
---

# segundo-cerebro

Skill da turma **Moonlight Expert**. Conduz a pessoa a montar e operar um Segundo Cérebro
de verdade, que é um **sistema** (input → transformação → output → feedback), e não
uma pasta bonita cheia de nota gerada por IA.

A teoria completa está em [`references/metodologia.md`](references/metodologia.md).
A estrutura de pastas, os tipos de nota e o frontmatter estão em [`references/estrutura.md`](references/estrutura.md).
Leia os dois antes da primeira execução numa sessão.

## A regra que governa tudo

> **O cofre é onde a pessoa pensa. A IA é a bibliotecária, nunca a autora.**

- A IA **pode**: buscar notas esquecidas, sugerir links, mostrar o que já foi estudado sobre
  um tema, comparar material novo com o que a pessoa já sabe, montar a escada de aprendizado
  e organizar arquivos e pastas.
- A IA **não pode**: escrever nota permanente ou de literatura, reescrever, resumir ou
  "melhorar" o texto da pessoa, decidir a tese ou o ângulo, nem substituir o estudo e a reflexão.
- Dentro de `_agents/` a IA tem autonomia total. Fora dela, só age com comando ou aprovação explícita.

Esta skill **ensina essa regra agindo de acordo com ela**. Se você quebrar a regra durante o
setup (escrevendo a nota pela pessoa, por exemplo), a skill ensina o contrário do que prega.

## Postura ao conduzir

1. **Uma pergunta por mensagem.** No máximo duas, se forem curtas e da mesma coisa. Espere a resposta.
2. **Explique o porquê em 2-3 linhas** no início de cada fase, ligando à teoria. Sem aula longa.
   Se a pessoa quiser se aprofundar, use `references/metodologia.md`.
3. **Mostre antes de criar.** Mostre a árvore de pastas ou o conteúdo do arquivo e só crie depois do "ok".
4. **O jeito padrão de responder é falando.** Logo no começo do setup, convide:
   "responda falando, por ditado de voz — rende mais, destrava e o texto sai com a sua voz.
   Windows: tecla Windows + H. Mac: o atalho do Ditado nos Ajustes de teclado. Celular: o microfone do
   teclado. Áudio longo: grave e cole a transcrição aqui."
   Vale pra tudo: briefing, nota de literatura, nota permanente e feedback dos outputs. Quem preferir
   digitar, digita — mas ofereça a voz na primeira pergunta de cada fase que peça texto da pessoa.
5. **Transcreva as palavras dela do jeito que vieram**, faladas ou digitadas. Numa nota com `autor: eu`
   você pode: pôr título (se ela aprovar), separar em seções, preencher o frontmatter e inserir links
   aprovados. Você não pode reescrever, resumir, completar frases, trocar palavras nem corrigir o texto.
   Transcrição de voz costuma vir sem pontuação e com repetição: **isso não é erro, é a fala dela.**
   Só ajuste se ela pedir, e mesmo aí só pontuação, nunca as palavras.
6. **Se ela pedir "escreve você":** explique uma vez, sem sermão, que nota escrita pela IA dá uma falsa
   sensação de produtividade. É como encher caderno com resumo que você não fez. Ofereça alternativas:
   - **falar a resposta em vez de digitar** (quase sempre resolve);
   - uma pergunta mais fácil ou mais concreta;
   - gerar um **output** em `_agents/00 Outputs/` marcado `autor: ia`, que nunca vira nota permanente
     sem que ela reescreva ou fale com as próprias palavras.
7. **Resposta vaga?** Faça uma pergunta de aprofundamento ("como você saberia que funcionou?"). Uma só, sem interrogatório.
8. **Salve o progresso ao fim de cada fase** em `_agents/02 Logs e Memoria/onboarding.md`. A pessoa
   pode parar quando quiser. Diga isso a ela no começo: "pode parar a qualquer momento e rodar
   `/segundo-cerebro` de novo que eu continuo de onde paramos."
9. Datas no formato `AAAA-MM-DD` (data de hoje). Caminhos com espaço sempre entre aspas.
10. Fale no idioma e no tom da pessoa. Por padrão, português do Brasil, direto e acolhedor.

## Detectar o estado e escolher o modo

O **cofre** é o diretório de trabalho atual (onde o agente, Claude Code ou Codex, foi aberto).

A skill não depende de um agente específico: o espaço da IA é a pasta `_agents/` e as regras ficam no
`AGENTS.md`, que o Codex lê direto. Para o Claude Code, a raiz do cofre também ganha um `CLAUDE.md` de uma
linha só, `@AGENTS.md`, que importa as mesmas regras. Um texto só, para não divergir.

| Argumento | Modo |
|---|---|
| `processar` | [Modo processar](#modo-processar) |
| `conectar <tema>` | [Modo conectar](#modo-conectar) |
| `revisar` | [Modo revisar](#modo-revisar) |
| `status` | [Modo status](#modo-status) |
| (nenhum) | Veja abaixo |

Sem argumento:
- `_agents/02 Logs e Memoria/onboarding.md` **não existe** → comece o setup na Fase 0, que termina
  com a pergunta do [ponto de partida](#ponto-de-partida).
- Existe com `fase_atual` < 7 → dê as boas-vindas de volta, lembre em 2 linhas o que já foi feito e
  **retome da fase registrada**.
- Existe com `concluido: true` → mostre um menu curto: processar um item do Inbox, conectar um tema,
  revisar ou ver o status.

---

## Setup guiado

Visão geral pra mostrar à pessoa no início, antes da Fase 0:

```
Fase 0  Onde vai morar o cofre
Fase 1  Output primeiro: pra que serve o seu sistema
Fase 2  Fluxo 1, o SEU cérebro (onde você pensa)
Fase 3  Fluxo 2, o ambiente da IA (onde ela trabalha)
Fase 4  Fluxo 3, a fronteira entre os dois (AGENTS.md)
Fase 5  Primeiro ciclo completo: input → transformação → output → feedback
Fase 6  Manutenção: o que faz o sistema ganhar valor com o tempo
```

Tempo estimado: 40–60 min. Dá pra fazer em partes. Quem já tem cofre e escolhe **só a fronteira**
passa só pelas Fases 0, 3, 4 e 6 (uns 15–20 min).

### Fase 0: Onde vai morar o cofre

Verifique em silêncio, sem perguntar:
- qual é o diretório atual. Se for a pasta pessoal raiz (`C:\Users\<nome>`, `/Users/<nome>`, `~`),
  a raiz de um disco ou uma pasta de sistema, **pare** e peça uma pasta dedicada;
- se existe `.obsidian/` (já é um cofre do Obsidian);
- quantas notas `.md` já existem (ignorando `.obsidian/`, `.claude/` e `_agents/`);
- se já existe `AGENTS.md` ou `_agents/`.

Mostre o que encontrou e pergunte: **"Posso usar esta pasta como o seu segundo cérebro?"**
- Se ela quiser outro lugar: explique que o agente (Claude Code ou Codex) precisa ser aberto **dentro** da
  pasta do cofre, porque é assim que ele carrega as regras do cofre. Peça pra ela criar ou escolher a pasta,
  abrir o agente lá e rodar `/segundo-cerebro` de novo. Encerre aqui.
- Se não existir `.obsidian/`: diga que funciona sem Obsidian, porque são só arquivos markdown. Recomende
  instalar (obsidian.md, grátis) e usar "Abrir pasta como cofre" nesta pasta pra ter a visão dos links
  e o grafo. Não é bloqueante.
- **Cofre com notas existentes:** combine desde já que **nada que já existe será movido, renomeado ou
  editado** no setup. A estrutura nova é criada ao lado. Organizar o antigo fica pra depois, com aprovação.

### Ponto de partida

Ainda na Fase 0, pergunte: **"Por onde você quer começar?"**

| Caminho | Pra quem | Fases |
|---|---|---|
| **Cofre do zero** | quem está começando ou tem poucas notas soltas | 0 → 1 → 2 → 3 → 4 → 5 → 6 (setup completo) |
| **Só a fronteira** | quem já tem um cofre organizado do seu jeito e quer dar à IA um espaço próprio e regras claras | 0 → 3 → 4 → 6 |

Recomende pelo que encontrou: com dezenas de notas e pastas próprias, sugira **só a fronteira**; com
cofre vazio, **cofre do zero**. A escolha é dela.

Crie `_agents/02 Logs e Memoria/onboarding.md` a partir de `templates/agents/onboarding.md`, com
`caminho: completo` e `fase_atual: 1`, ou `caminho: fronteira` e `fase_atual: 3`.

#### O caminho "só a fronteira"

A ideia é **criar a limitação de escopo sem mexer em nada do que já existe**: a IA ganha a pasta `_agents/`
e um `AGENTS.md` que diz o que ela pode e o que não pode no resto do cofre.

- **Pule as Fases 1, 2 e 5.** As pastas dela já existem e não são trocadas pelas do Fluxo 1.
- **Fase 3** roda igual: cria `_agents/` com as 8 pastas.
- **Fase 4** muda em três pontos:
  - antes das perguntas, liste as pastas de primeiro nível do cofre e pergunte, uma vez, quais são
    **dela** (a IA lê, sugere, não escreve) e se alguma é compartilhada (a IA pode escrever ali com aprovação);
  - no lugar do briefing, uma pergunta só: **"Em uma ou duas frases, pra que serve este cofre?"** A resposta,
    transcrita como veio, preenche `{{RESUMO_BRIEFING}}`;
  - no `AGENTS.md`, o "Mapa do cofre" é o mapa **real** das pastas dela, com uma linha cada, e não o do template.
- **Notas antigas sem `autor`:** fora de `_agents/`, nota sem `autor` conta como `autor: eu`. Não acrescente
  frontmatter em massa; ele entra quando a nota for tocada com aprovação.
- Ao fim da Fase 4, atualize `fase_atual: 6` (não 5). Ao retomar, siga o `caminho` registrado em `onboarding.md`.
- **Fase 6** roda igual. No fechamento, ofereça as fases puladas como opcionais: "se quiser, depois a gente
  roda o primeiro ciclo completo com algo real seu" (Fase 5) e "o briefing completo" (Fase 1).

### Fase 1: Output primeiro

**Por quê (dizer):** todo sistema precisa de input, transformação e output. Sem um output definido,
o que sobra é acúmulo de notas. Por isso a primeira coisa é calibrar o que o sistema precisa entregar na sua vida.

Antes da primeira pergunta, faça o convite da voz (item 4 da postura): responder falando rende mais,
destrava e o texto entra no cofre com a voz da pessoa.

Perguntas, uma por vez:
1. "Daqui a 6 meses, o que precisa estar diferente no seu trabalho ou na sua vida por causa desse sistema?"
   Se vier vago ("ser mais organizado"), pergunte: "como você saberia que funcionou?"
2. "O que entra na sua cabeça hoje? Cursos, livros, vídeos, calls, clientes, ideias soltas... E onde isso fica guardado hoje?"
3. "Quais são seus **projetos ativos** agora (coisas com entrega ou prazo)? E quais **assuntos** você
   estuda ou mantém sempre (sem prazo)?" Isso vira as pastas de projeto e os tópicos.
4. "Em que tipo de entrega você quer que a IA trabalhe **por** você?" (conteúdo, propostas, planejamento,
   pesquisa, código, preparação de aulas...)

Salve as respostas **do jeito que vieram** em `_agents/07 Briefings e Databases/briefing-pessoal.md`
(template `templates/agents/briefing-pessoal.md`, `autor: eu`). Mostre o arquivo, confirme, atualize `fase_atual: 2`.

### Fase 2: Fluxo 1, o SEU cérebro

**Por quê (dizer):** aqui é onde você pensa. Aprender de verdade tem 4 passos: (1) ler ou viver aquilo,
(2) processar na cabeça, (3) escrever com as suas palavras e (4) conectar com o que você já sabe.
A mágica é você passar por esse processo, não ter as notas. Por isso a IA lê e sugere aqui, mas não escreve.

Monte a proposta usando `references/estrutura.md` → "Fluxo 1", **personalizada com as respostas
da Fase 1**: uma subpasta em `10 Projetos/` por projeto e um hub em `02 Topicos/` por assunto.
Mostre a árvore completa e pergunte: **"Quer ajustar alguma coisa antes de eu criar?"**

Depois do ok:
- crie as pastas (use o shell disponível: `mkdir -p "<caminho>"` no bash/zsh ou
  `New-Item -ItemType Directory -Force "<caminho>"` no PowerShell);
- crie um hub por assunto em `02 Topicos/<Assunto>.md` a partir de `templates/cofre/topico.md`.
  Isso é organização, então é permitido. O hub nasce vazio, só com título e seções;
- copie `templates/cofre/*.md` para `99 Templates/`.

Passe à pessoa as 3 configurações do Obsidian (se ela usa), pra ela mesma fazer:
- Configurações → Arquivos e links → Local para novos anexos → pasta `90 Anexos`
- Configurações → Plugins principais → Modelos (Templates) → ativar → pasta `99 Templates`
- Configurações → Plugins principais → Notas diárias → pasta `03 Diario`, modelo `99 Templates/diario`

Atualize `fase_atual: 3`.

### Fase 3: Fluxo 2, o ambiente da IA

**Por quê (dizer):** a IA precisa de um lugar próprio pra trabalhar, com logs, memória, planos e
outputs, senão ela contamina o seu espaço de pensar. Liberar o cofre inteiro gera contexto demais e
bagunça. Um cofre separado deixa a IA confusa com notas duplicadas. O que funciona é **uma pasta dela
dentro do seu cofre**: lá dentro autonomia total, fora só com a sua aprovação.

Mostre a árvore de `_agents/` (em `references/estrutura.md` → "Fluxo 2") explicando cada pasta
em uma linha. Depois do ok:
- crie as 8 pastas e um `_LEIA.md` em cada, com o conteúdo definido em `references/estrutura.md`;
- crie `_agents/02 Logs e Memoria/memoria.md` (template `templates/agents/memoria.md`) e a pasta `logs/`;
- copie `templates/agents/{output,log-sessao,decisao}.md` para `_agents/05 Templates e Referencias/`.

Uma pergunta opcional: **"Tem alguma entrega recorrente que já merece virar um agente?"** (ex.:
"roteirista dos meus posts"). Se tiver, crie só o esqueleto em `_agents/04 Agentes/<nome>/`
(`instrucao.md`, `processo.md`, `referencias/`) e explique que um bom agente é mais que uma instrução:
precisa de referências, frameworks e processo. O conteúdo é preenchido com o tempo. Se não tiver, siga em frente.

Atualize `fase_atual: 4`.

### Fase 4: Fluxo 3, a fronteira (AGENTS.md)

**Por quê (dizer):** o multiplicador aparece quando os dois fluxos conversam. A IA lê o seu cérebro
pra ter contexto, e você lê os outputs da IA pra gerar novos pensamentos. Isso só funciona com uma
fronteira clara. É aqui que a maioria erra, porque mistura tudo sem regra. O `AGENTS.md` é essa regra por escrito.
O que faz diferença é a clareza das regras, não a quantidade.

Perguntas, uma por vez:
1. "Tem alguma pasta que a IA **não deve nem ler**?" (ex.: diário)
2. "Quando a IA achar uma conexão entre suas notas, você prefere que ela **insira só o `[[link]]`
   depois que você aprovar**, ou que ela **só sugira** e você insira à mão?"
3. "Como você quer que a IA converse com você?" (direta, didática, provocadora, que questione suas ideias...)

Gere o `AGENTS.md` na raiz do cofre a partir de `templates/AGENTS.template.md`, preenchendo os
`{{campos}}`. O resumo do briefing é uma exceção à regra da transcrição: por ser um arquivo de regras
da IA, pode ser um resumo, **desde que a pessoa aprove**. Mostre o arquivo inteiro e escreva só depois do ok.

- **Já existe `AGENTS.md`?** Não sobrescreva. Mostre o que existe e proponha **acrescentar** uma seção
  `## Segundo Cérebro` com as regras. Escreva só depois do ok.

Depois, o ponteiro para o Claude Code:
- **Não existe `CLAUDE.md`:** crie na raiz com uma linha só, `@AGENTS.md`.
- **Já existe `CLAUDE.md`:** não sobrescreva. Proponha acrescentar a linha `@AGENTS.md` no fim e escreva só depois do ok.

Explique em 1 linha: a partir da próxima sessão, toda vez que ela abrir o Claude Code ou o Codex nesta pasta, ele já vai seguir essas regras.

Atualize `fase_atual: 5`.

### Fase 5: Primeiro ciclo completo

**Por quê (dizer):** estrutura sem uso é só setup. Vamos rodar o sistema uma vez, de ponta a ponta,
com algo real seu.

Pergunte: **"Me dá uma coisa real que você consumiu nos últimos dias e que te marcou: um vídeo, aula,
capítulo, conversa ou ideia."** Depois siga os passos, um de cada vez:

**5.1 Input.** Registre o item cru em `00 Inbox/AAAA-MM-DD <nome curto>.md` (link, trecho ou
descrição que ela deu, `tipo: inbox`). Se for um vídeo ou arquivo que precise de transcrição feita pela IA,
a transcrição é da IA e vai para `_agents/00 Outputs/`, com link no item do Inbox.

**5.2 Transformação: nota de literatura (ela escreve, de preferência falando).** Diga que agora é a vez
dela pensar, que você só vai perguntar e anotar, e que o melhor jeito de responder é **falando**:
é como explicar pra um amigo, e o que entra na nota é a transcrição da fala dela. Perguntas, uma por vez:
1. "Qual é a ideia central disso, com as **suas** palavras?"
2. "O que te surpreendeu, ou onde você discorda?"
3. "Com o que isso se conecta, de algo que você já sabe ou já viveu?"
4. "Onde você vai usar isso nas próximas semanas?"

Crie `01 Processamento/<título>.md` a partir de `templates/cofre/nota-literatura.md`, com as respostas
**do jeito que vieram**, cada uma na sua seção. Mostre o arquivo.

**5.3 Transformação: nota permanente (ela escreve, de preferência falando).** Explique a diferença em
1 linha: a nota de literatura é sobre a fonte, a permanente é **a ideia dela**, que se sustenta sozinha.
1. "Se você tivesse que explicar essa ideia pra alguém em 3 a 5 frases, **sem citar de onde veio**, como seria?"
   (peça pra ela falar a explicação em voz alta, como se estivesse explicando pra um amigo)
2. "Que título você daria? De preferência uma **afirmação** (ex.: 'Setup não é sistema'), não um assunto ('Segundo cérebro')."

Pergunte em qual pasta ela fica (normalmente `20 Recursos/`, ou o projeto relacionado). Crie a nota
a partir de `templates/cofre/nota-permanente.md` com o texto dela, sem mudar nada.

**5.4 Bibliotecária (a IA trabalha).** Agora é a sua vez. Faça uma busca direcionada no cofre (hubs em
`02 Topicos/`, busca por termos e links) e mostre:
- notas existentes que se conectam, com **um motivo em uma linha** para cada;
- em que hub de tópico a nota entra.

Siga a preferência de links da Fase 4. Com aprovação, insira **só** os `[[links]]` na seção
"Conexões" da nota e a linha no hub. Cofre novo e vazio? Diga isso, sugira só o hub e comente que as
conexões ficam mais valiosas conforme o cofre cresce.

**5.5 Output (a IA produz).** Pergunte: **"Que entrega prática você quer tirar dessa ideia?"** (ex.: um
post, um checklist, um plano de aplicação, um roteiro de aula). Gere em
`_agents/00 Outputs/AAAA-MM-DD <nome>.md` a partir do template de output (`autor: ia`,
`status: rascunho`, `fonte: "[[nota permanente]]"`).

**5.6 Feedback.** Peça pra ela ler o output e pergunte: **"O que ficou bom e o que não ficou com a sua cara?"**
- Ajuste o output se ela pedir e atualize o `status`.
- Registre o que for **durável** (preferência de tom, formato, o que evitar) em `memoria.md`.
- Mostre o ciclo que acabou de acontecer:

```
  VOCÊ                                 IA
  00 Inbox (input) ──► 01 Processamento (literatura)
                         └─► 20 Recursos (permanente) ──► links sugeridos (bibliotecária)
                                    │
                                    └────────────────────► _agents/00 Outputs (entrega)
                                                                   │
  você revisa o output ◄───────────────────────────────────────────┘
       └─► memoria.md fica mais precisa ──► a próxima entrega sai melhor
```

Atualize `fase_atual: 6`.

### Fase 6: Manutenção e fechamento

**Por quê (dizer):** a IA não lembra entre sessões. Quem fica mais inteligente são os
**arquivos**, e isso só acontece com manutenção. Sem revisar, podar e eliminar, o cofre vira aquela
documentação gigante de empresa que ninguém consulta. Mais arquivos não significa mais inteligência.
Output da IA que ninguém revisou é nota que parece útil, mas nunca foi testada.

1. Pergunte: **"Qual dia e horário da semana você reserva 20 minutos pra revisão?"**
2. Crie `_agents/05 Templates e Referencias/ritual-revisao-semanal.md` a partir do template, com o dia escolhido,
   e atualize a linha de manutenção no `AGENTS.md`.
3. Explique os modos pro dia a dia:
   - `/segundo-cerebro processar`: pega um item do Inbox e conduz as perguntas
   - `/segundo-cerebro conectar <tema>`: mostra o que você já sabe, as lacunas e a escada de aprendizado
   - `/segundo-cerebro revisar`: a revisão semanal
   - `/segundo-cerebro status`: a saúde do sistema
4. Mostre a árvore final do que foi criado.
5. Escreva o primeiro log em `_agents/02 Logs e Memoria/logs/AAAA-MM-DD.md` e marque
   `concluido: true` e `fase_atual: 7` em `onboarding.md`.
6. Feche com a provocação, em 2-3 linhas: quando a IA resolver o problema de memória, e ela vai
   resolver, memória vira commodity. O que sobra é a **utilidade que você criou**: suas notas autorais,
   seus processos, os fluxos que transformam informação em resultado. É isso que coloca você no grupo
   que usa a IA, e não no que é usado por ela.

---

## Modo processar

Objetivo: transformar um item do Inbox em conhecimento dela (passos 5.2 a 5.4, sem precisar gerar output).

1. Liste os itens de `00 Inbox/` (os mais antigos primeiro, com a data) e pergunte qual processar.
   Se tiver mais de 15 itens, diga isso sem julgar e sugira escolher 1 ou 2 hoje.
2. Leia o item. Se for material longo, a IA **pode** extrair a estrutura (tópicos, trechos-chave com
   referência) como output em `_agents/00 Outputs/`. Deixe claro que isso é mapa, não nota.
3. **Antes das perguntas, sirva de bibliotecária:** "Você já tem X e Y sobre isso. O que parece novo aqui
   é Z." Isso evita estudar duas vezes a mesma coisa.
4. Faça as perguntas de literatura (5.2), lembrando que responder falando é o jeito mais rápido.
   Crie ou atualize a nota em `01 Processamento/` com o texto dela, transcrito como veio.
5. Pergunte se já tem uma ideia madura pra nota permanente. Se sim, siga o 5.3 e o 5.4. Se não,
   tudo bem: a nota fica em processamento.
6. Pergunte o que fazer com o item do Inbox: arquivar em `40 Arquivo/`, apagar ou manter. Faça só depois da resposta.
7. Escreva o log da sessão.

## Modo conectar

Objetivo: a IA como bibliotecária sobre um `<tema>`. Ela escreve **sobre** as notas, nunca **nelas**.

1. Se o tema não veio no argumento, pergunte. Pergunte também: "Tem material novo que você quer
   comparar com o que já sabe? (livro, curso, link)"
2. Busca direcionada: comece pelo hub em `02 Topicos/`, depois procure termos, sinônimos e links.
   Não leia o cofre inteiro.
3. Gere uma nota de **curadoria** em `_agents/00 Outputs/AAAA-MM-DD mapa - <tema>.md` (`tipo: curadoria`, `autor: ia`) com:
   - **O que você já tem:** lista de `[[notas]]`, com uma linha sobre o que cada uma afirma;
   - **Conexões que faltam:** pares de notas que deveriam se linkar, e o motivo;
   - **Repetido × novo:** se veio material novo, o que você já estudou e o que é realmente novo;
   - **Lacunas:** o que falta pra dominar o tema;
   - **Escada de aprendizado:** a ordem sugerida do básico ao avançado, marcando o que já foi feito.
4. Mostre o resumo. Insira links em notas dela **só com aprovação**, seguindo a regra do `AGENTS.md`.
5. Escreva o log da sessão.

## Modo revisar

Objetivo: o ritual semanal que faz o sistema ganhar valor com o tempo. Siga
`_agents/05 Templates e Referencias/ritual-revisao-semanal.md` (se não existir, use `templates/agents/ritual-revisao-semanal.md`).

Levante e mostre em uma tabela curta:

| Checagem | Critério |
|---|---|
| Inbox | itens com mais de 7 dias |
| Processamento | notas paradas há mais de 14 dias |
| Permanentes órfãs | nota com `tipo: permanente` sem nenhum link de entrada ou saída |
| Outputs sem revisão | `autor: ia` com `status: rascunho` há mais de 7 dias |
| Memória | `memoria.md` com mais de ~150 linhas, itens repetidos ou contraditórios |
| Logs | mais de 30 dias sem consolidar |
| Projetos | pastas em `10 Projetos/` sem alteração há mais de 30 dias (candidatas a `40 Arquivo/`) |
| Violação da fronteira | nota fora de `_agents/` com `autor: ia` (a IA escreveu onde não devia) |

Depois conduza, um bloco por vez:
1. **Dentro de `_agents/`:** proponha o que podar (outputs descartados, logs antigos que podem virar um resumo
   mensal, memória consolidada). Mesmo com autonomia, **peça ok antes de apagar** qualquer coisa que a pessoa não revisou.
2. **Fora de `_agents/`:** só sugestões (arquivar projeto, processar inbox, linkar órfãs). Execute só o que ela aprovar.
3. Pergunte: "Tem alguma decisão ou aprendizado da semana que vale registrar?" Se sim, crie em `_agents/06 Decisoes/`.
4. Pergunte: "O `AGENTS.md` ainda reflete como você quer trabalhar?" Ajuste só com aprovação.
5. Escreva o log da revisão.

## Modo status

Sem perguntas. Mostre um painel curto: total de notas por tipo (`permanente`, `literatura`, `curadoria`,
`output`), itens no Inbox, notas em processamento, quantas permanentes estão órfãs, outputs pendentes
de revisão, data da última revisão (último log de revisão) e dias desde a última nota permanente.
Termine com **uma** recomendação ("o gargalo agora é X, sugiro Y").

---

## Gotchas

- **Skill não é o agente inteiro.** O comportamento no dia a dia vem do `AGENTS.md` do cofre, que é
  carregado quando o agente é aberto **na pasta do cofre** (no Claude Code, pelo `CLAUDE.md` com `@AGENTS.md`).
  Se a pessoa abrir em outra pasta, as regras não valem.
- **Skills ativas ficam na pasta de skills do agente** (`.claude/skills/` no Claude Code, `.codex/skills/` no Codex),
  não em `_agents/01 Skills`.
  Essa pasta é o índice e a documentação das skills da pessoa (o que existe, pra que serve, quando usar).
- **Não leia o cofre inteiro** pra "ter contexto". Estoura a janela e piora a resposta. Use hubs e busca direcionada.
- **Variáveis de template:** os arquivos em `templates/cofre/` usam a sintaxe do Obsidian (`{{date:...}}`, `{{title}}`).
  Quando copiar pra `99 Templates/`, mantenha as variáveis. Quando **criar uma nota** a partir deles, troque pela data e pelo título reais.
- **Frontmatter é o que permite checar a fronteira.** Toda nota criada pela skill leva `tipo` e `autor`.
- **Windows/PowerShell 5.1:** grave arquivos com a ferramenta de escrita (UTF-8), nunca com `Set-Content`
  sem `-Encoding utf8`. Os nomes de pasta não têm acento de propósito.
- **Cofre com notas antigas:** não reorganize no setup. Se a pessoa quiser migrar, faça em lotes pequenos
  (uma pasta por vez), mostre o de/para e só mova depois do ok.
- **Crédito:** a metodologia vem do vídeo "Segundo Cérebro com IA: Ganhe SUPER-PODERES (Claude Code +
  Obsidian)", do canal Ana Jords. Os nomes das pastas e das fases são adaptação desta skill.
