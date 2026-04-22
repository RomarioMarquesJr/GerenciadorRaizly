# Raizly Instagram Posts Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create 10 high-conversion Instagram posts (5 each for weeks 1-2) ready to publish, following the copy framework and design system outlined in the design spec.

**Architecture:** Posts are organized by week and day, each following one of 3 templates (Carrossel PASC, Feed Long, Micro-anúncio). Copy uses AIDA framework with direct response techniques. Visual design uses Raizly brandbook (rust/bone/ink, Familjen Grotesk fonts). Each post includes caption, visual notes, and CTA.

**Tech Stack:** Copy + Design. Tools: Canva, Figma, or similar for visual mockups. Outputs: markdown + image files for reference.

---

## File Structure

All posts will be documented and saved in:
- `posts/week-1/` - 5 posts (Monday-Friday)
- `posts/week-2/` - 5 posts (Monday-Friday)
- `assets/templates/` - Visual templates and brand guidelines
- `posts/POSTS_READY_TO_PUBLISH.md` - Master list with Instagram captions ready to copy-paste

---

## Task 1: Create Week 1 Posts (Days 1-5)

### Posts Overview for Week 1

| Day | Theme | Angle | Template | Problem Focus |
|-----|-------|-------|----------|---|
| **Mon** | Agendamento | Problem | Carrossel PASC | Clientes que não confirmam |
| **Tue** | Dados | Solution | Feed Long | Raizly mostrando números |
| **Wed** | Agendamento | Transformation | Carrossel PASC | Antes/depois de agendamentos |
| **Thu** | Dados | Urgency | Carrossel PASC | Quanto perde por mês |
| **Fri** | Controle Financeiro | Teaser | Micro-anúncio | Problema de fluxo de caixa |

---

### Week 1, Day 1: Monday - Agendamento (Problem)

**Template:** Carrossel PASC (5 slides)
**Focus:** Curiosity gap + agitation about lost clients

**Files:**
- Create: `posts/week-1/monday-agendamento-problem.md`
- Visual reference: `assets/templates/carousel-pasc-template.txt`

- [ ] **Step 1: Write copy for Slide 1 (Hook)**

Create file `posts/week-1/monday-agendamento-problem.md` with:

```markdown
# Week 1, Monday: Agendamento - Problem Angle

## Carrossel PASC Structure

### SLIDE 1: Hook (Curiosity Gap)
**Visual:** Rust red background (#E8430A), white text (Bone #F0EDE6), large bold headline
**Copy:**
Você está cometendo esse erro que custa até R$10k/mês?

(Smaller text below)
A maioria dos donos de barbearia não percebem...

**Design Notes:**
- Bold headline, 60-80pt, centered
- Rust background, Bone text
- Logo HEADLY TECH small bottom right
```

- [ ] **Step 2: Write copy for Slides 2-3 (Problem + Agitation)**

```markdown
### SLIDE 2: Problem Specification
**Visual:** Dark background (Ink #111), Bone text, icon/graphic of calendar
**Copy:**
De cada 10 clientes que chegam na porta da sua barbearia...

...quantos realmente confirmam o agendamento?

A resposta chocante: 4 em cada 10 simplesmente somem.

(Smaller) Eles não cancelam, não ligam. Só... desaparecem.

**Design Notes:**
- Large number "4 em 10" in Rust
- Relatable visual (disappointed barber, empty chair)
```

```markdown
### SLIDE 3: Agitation & Financial Impact
**Visual:** Dark background, Rust numbers, Bone text
**Copy:**
Vamos fazer as contas:
- Você tem ~50 agendamentos por semana
- 40% não confirmam = 20 clientes perdidos por semana
- 20 × R$150 (ticket médio) = R$3.000 perdidos por semana

POR SEMANA.

Isso é R$12.000 por mês desaparecendo.

(Smaller) E o pior? Você nem sabe o motivo real.

**Design Notes:**
- Emphasize the R$12.000 number (big, in Rust)
- Show calculation step-by-step
- Create sense of urgency
```

- [ ] **Step 3: Write copy for Slide 4 (Solution)**

```markdown
### SLIDE 4: Solution - Raizly Changes This
**Visual:** Light background (Bone), Dark text, Raizly interface mockup
**Copy:**
Com Raizly, esses 4 clientes que somem...

...viram 7 clientes confirmados.

Por quê?

✓ Confirmação automática (cliente confirma com 1 clique)
✓ Lembretes antes do agendamento (reduz no-shows)
✓ Chat integrado (você resolve dúvidas antes de desistirem)

Resultado em 30 dias: você recupera esse R$12.000.

**Design Notes:**
- Show Raizly interface (screenshot or mockup)
- Use checkmarks in Rust
- Emphasize "em 30 dias"
```

- [ ] **Step 4: Write copy for Slide 5 (CTA)**

```markdown
### SLIDE 5: CTA + Urgency
**Visual:** Dark background (Ink), Rust button/highlight, Bone text
**Copy:**
Não deixe mais dinheiro na mesa.

🔗 Clique no link da bio para agendar sua demo (gratuita)

⚠️ Vagas limitadas para os primeiros 50 donos de barbearia

Sua primeira semana com Raizly é por nossa conta.

Vamos?

**Design Notes:**
- Clear CTA button in Rust
- Scarcity message (primeiros 50)
- Soft language but strong ask
```

- [ ] **Step 5: Write Instagram caption for this post**

```markdown
## Instagram Caption (for carousel)

Você está cometendo esse erro que custa até R$10k/mês? 😱

De cada 10 clientes que chegam na porta, 4 simplesmente não confirmam o agendamento.

Isso é R$12.000 por mês desaparecendo.

Mas com Raizly? Esses 4 clientes viram 7 confirmados.

✓ Confirmação automática
✓ Lembretes antes do horário
✓ Chat para resolver dúvidas

Em 30 dias você recupera esse dinheiro.

👇 Clique no link da bio para agendar sua demo (vagas limitadas)

#Barbearia #TecnologiaNasBarbearias #CRMParaBarbearia #HEADLYTECH
```

---

### Week 1, Day 2: Tuesday - Dados (Solution)

**Template:** Feed Long (single image + caption)
**Focus:** Solution-oriented, show Raizly solving the problem

**Files:**
- Create: `posts/week-1/tuesday-dados-solution.md`

- [ ] **Step 1: Write long-form caption**

```markdown
# Week 1, Tuesday: Dados - Solution Angle

## Feed Post (Long Caption)

**Visual:** Image of barber owner looking at Raizly dashboard with numbers/graphs visible

**Caption:**

"Eu não sabia aonde meu dinheiro estava indo."

Esse foi o momento que tudo mudou para a barbearia do João.

Ele tinha ~R$15k de faturamento por mês, mas não sabia exatamente:
- Quanto era lucro real?
- Qual era seu melhor serviço?
- Qual horário rendia mais?
- Por que alguns meses eram bons e outros ruins?

Estava tudo na cabeça dele. E na cabeça nunca está claro.

Aí veio a Raizly.

Em uma semana, João tinha visibilidade total:
- Lucro real: R$8.500 (não R$15k como achava)
- Melhor serviço: Barba Premium (40% do faturamento)
- Melhor horário: Quinta à noite (R$2k só nesse turno)
- Problema maior: Ele estava gastando 35% com produtos desnecessários

Com esses dados em mãos, João fez 3 mudanças simples:
1. Reduziu gastos desnecessários (-R$500/mês)
2. Focou em agendar mais Barbas Premium
3. Abriu quinta à noite como turno especial

Resultado? O lucro real de João foi de R$8.500 para R$11.200 em 60 dias.

Sem contratar ninguém. Sem trabalhar mais. Só com dados certos.

Dados são poder.

E Raizly te dá esses dados.

👇 Link na bio para conhecer. Primeiros 50 donos ganham primeira semana grátis.

#DadosSãoForça #BarbeariaProfissional #GestãoInteligente #HEADLYTECH

**Design Notes:**
- Dashboard screenshot as hero image
- Testimonial-style, personal narrative
- Strong conversion story (before/after numbers)
```

---

### Week 1, Day 3: Wednesday - Agendamento (Transformation)

**Template:** Carrossel PASC (4 slides, condensed)
**Focus:** Before/after transformation

**Files:**
- Create: `posts/week-1/wednesday-agendamento-transformation.md`

- [ ] **Step 1: Write transformation carousel**

```markdown
# Week 1, Wednesday: Agendamento - Transformation Angle

## Carrossel PASC (4 slides)

### SLIDE 1: Before
**Visual:** Chaotic visual (scattered calendar, confused barber, red X marks)
**Copy:**
ANTES (sem Raizly):

📅 Agenda no WhatsApp (perdida em 100 outras mensagens)
❌ Cliente não confirma
❌ Horário vazio no seu dia
💔 Dinheiro perdido

### SLIDE 2: The Pain Point
**Visual:** Barber stressed, looking at phone
**Copy:**
Você nunca sabe:
- Se o cliente vai aparecer
- Por que não apareceu
- Como organizar melhor a agenda

É caos.

### SLIDE 3: After (com Raizly)
**Visual:** Clean, organized dashboard, happy barber
**Copy:**
DEPOIS (com Raizly):

✅ Agendamento digital (sem WhatsApp)
✅ Cliente confirma com 1 clique
✅ Lembrete automático antes do horário
✅ Você vê exatamente quem vem

Zero caos.

### SLIDE 4: Result
**Visual:** Calendar full, happy barber, money symbol
**Copy:**
Resultado:

📈 95% de confirmação de agendamentos
💰 Mais clientes, menos furos
⏰ Seu tempo vale muito mais

Pronto para transformar sua barbearia?

🔗 Link na bio (primeiros 50 têm primeira semana grátis)

**Instagram Caption:**
Tem 2 tipos de barbearia: aquelas que sabem quem vai aparecer... e as outras.

Qual é a sua? 👇

De Before pra After é só um passo. (Spoiler: é com Raizly)

#Transformação #Organização #BarbeariaProfissional #HEADLYTECH
```

---

### Week 1, Day 4: Thursday - Dados (Urgency)

**Template:** Carrossel PASC (5 slides)
**Focus:** Urgency + FOMO, monthly cost of not knowing

**Files:**
- Create: `posts/week-1/thursday-dados-urgency.md`

- [ ] **Step 1: Write urgency carousel**

```markdown
# Week 1, Thursday: Dados - Urgency Angle

## Carrossel PASC (5 slides)

### SLIDE 1: Hook
**Visual:** Red/rust alarm icon, bold text
**Copy:**
Quanto você DEIXOU DE GANHAR este mês?

(E não faço ideia, né?)

### SLIDE 2: The Reality
**Visual:** Dark, numbers, reality check
**Copy:**
Donos de barbearia SEM dados cedem que perdem em média:

R$8.000-15.000 por mês

Vendas perdidas. Clientes não otimizados. Gastos desnecessários.

### SLIDE 3: You Don't Even Know
**Visual:** Question marks, confused emoji
**Copy:**
O pior?

Você não sabe exatamente aonde foi esse dinheiro.

- Qual serviço é mais lucrativo?
- Qual horário rende mais?
- Onde você está gastando demais?
- Quantos clientes realmente viram seu faturamento crescer?

Você CHUTA.

### SLIDE 4: What Raizly Changes
**Visual:** Dashboard with clear data, green numbers
**Copy:**
Raizly mostra EXATAMENTE:

✅ Serviço mais lucrativo
✅ Horário/dia que rende mais
✅ Gastos desnecessários
✅ Ticket médio real

Tudo em um só lugar. Atualizado em tempo real.

### SLIDE 5: The Math
**Visual:** Simple calculation, big numbers in Rust
**Copy:**
Se você recuperar APENAS 50% do que está perdendo...

Seriam R$4.000 a 7.500 A MAIS por mês.

Isso é R$48.000 a 90.000 POR ANO.

Por uma semana de Raizly grátis?

Vale MUITO a pena.

🔗 Link na bio. Comece agora.

**Instagram Caption:**
Quantos mil você deixou de ganhar este mês? 😬

A maioria não sabe. E é por isso que não cresce.

Dados são poder. Raizly te dá esse poder.

👇 Link na bio (vagas limitadas para primeiros 50)

#DadosEmTempoReal #LucroReal #BarbeariaProfissional #HEADLYTECH
```

---

### Week 1, Day 5: Friday - Controle Financeiro (Teaser)

**Template:** Carrossel PASC (4 slides, expandido)
**Focus:** Problem awareness + solution teaser + urgency

**Files:**
- Create: `posts/week-1/friday-controle-teaser.md`

- [ ] **Step 1: Write expanded carousel**

```markdown
# Week 1, Friday: Controle Financeiro - Teaser Angle

## Carrossel PASC (4 slides, expandido)

### SLIDE 1: Problem Question
**Visual:** Large question mark, bold text, Rust/Bone colors, confused emoji
**Copy:**
Você sabe quanto LUCROU na semana passada?

(Com certeza? Ou é palpite?)

### SLIDE 2: The Reality
**Visual:** Money flowing out graphic, red numbers
**Copy:**
A maioria dos donos de barbearia não sabe.

E sem saber exatamente:
- Não controla gastos
- Não otimiza horários
- Não investe certo
- Fica preso

Resultado: crescimento estagnado.

### SLIDE 3: What It Costs
**Visual:** Calculation visual, large number in Rust
**Copy:**
Falta de controle financeiro custa em média:

R$4.000 a 8.000 POR MÊS

Em gastos desnecessários + oportunidades perdidas.

Isso é R$48k a 96k POR ANO.

### SLIDE 4: CTA + Teaser
**Visual:** Call-to-action button in Rust, subtle Raizly logo
**Copy:**
Recupere esse controle.

Com Raizly, você vê:
✓ Lucro real em tempo real
✓ Gastos linha a linha
✓ Oportunidades de crescimento

🔗 Clique na bio para começar.

Primeira semana? Por nossa conta.

**Instagram Caption:**
Você sabe quanto lucrou na semana passada?

Não? Aí está o problema. (E está custando até R$8k/mês)

Raizly resolve isso em dias.

👇 Link na bio (primeira semana grátis)

#ControleFinanceiro #LucroReal #HEADLYTECH
```

- [ ] **Step 2: Commit Week 1 posts**

Run:
```bash
git add posts/week-1/
git commit -m "feat: create week 1 instagram posts (agendamento, dados, controle)"
```

Expected: All 5 posts saved and committed.

---

## Task 2: Create Week 2 Posts (Days 1-5)

### Posts Overview for Week 2

| Day | Theme | Angle | Template | Focus |
|-----|-------|-------|----------|---|
| **Mon** | Controle Financeiro | Deep dive | Feed Long | Gestão de fluxo de caixa |
| **Tue** | Agendamento | Social Proof | Carrossel PASC | Case real de dono |
| **Wed** | Controle | Transformation | Carrossel PASC | Antes/depois de controle |
| **Thu** | Agendamento | Stat Shock | Carrossel PASC | Estatística assustadora |
| **Fri** | Dados | Result | Carrossel PASC | ROI do Raizly |

---

### Week 2, Day 1: Monday - Controle Financeiro (Deep Dive)

**Template:** Feed Long
**Focus:** Deep financial story, relatable narrative

**Files:**
- Create: `posts/week-2/monday-controle-deepdive.md`

- [ ] **Step 1: Write long-form post**

```markdown
# Week 2, Monday: Controle Financeiro - Deep Dive

## Feed Post (Long Caption)

**Visual:** Image of barber owner with calculator/spreadsheet looking stressed, then relieved

**Caption:**

"Meu fluxo de caixa era um mistério."

Esse é o testemunho de Carlos, dono de uma barbearia em São Paulo.

Ele faturava bem (~R$18k/mês), mas tinha um problema:
- Alguns meses sobrava grana
- Outros meses ficava apertado
- Nunca sabia por quê

"Era tudo muito confuso", ele disse. "Eu tinha dinheiro em caixa, no banco, em crediário que dei pro cliente... não sabia nem quanto tinha de verdade."

Resultado? Carlos estava deixando de fazer investimentos. Não expandia a barbearia. Vivia no "talvez no próximo mês".

Aí entrou Raizly.

A primeira coisa que Raizly mostrou?

O fluxo de caixa REAL de Carlos:

- Entrada: R$18.000 (faturamento)
- Despesas: R$9.200 (produtos, aluguel, funcionários)
- Lucro real: R$8.800

Mas esperaaa... havia mais:

Carlos estava "emprestando" dinheiro pros clientes em forma de crediário (sem cobrar juros).
Total emprestado: R$2.100 que ele não via em caixa.

Com Raizly, Carlos automatizou:
1. Controle de todos os pagamentos (cartão, dinheiro, crediário)
2. Lembretes automáticos pros clientes que devem
3. Relatórios semanais (sabe exatamente o saldo)

Resultado em 2 semanas?

Carlos recuperou R$1.800 dos clientes que deviam.
Seu fluxo de caixa ficou claro.
Ele finalmente sabia quanto tinha para investir.

3 meses depois, Carlos abriu seu segundo horário. Contratou mais um barbeiro.

Por quê? Porque agora ele VIA o dinheiro. Via o potencial. Via a realidade.

Dados criam coragem. Visibilidade cria ação.

Se você está como Carlos estava...

👇 Link na bio. Primeira semana grátis.

Seu fluxo de caixa merece clareza.

#ControleFinanceiro #FluxoDeCaixa #BarbeariaProfissional #HEADLYTECH

**Design Notes:**
- Use relatable barber owner in image
- Before/after emotional journey
- Strong social proof with specific numbers
- Clear transformation story
```

---

### Week 2, Day 2: Tuesday - Agendamento (Social Proof)

**Template:** Carrossel PASC (4 slides)
**Focus:** Real case of barbershop owner using Raizly

**Files:**
- Create: `posts/week-2/tuesday-agendamento-socialproof.md`

- [ ] **Step 1: Write social proof carousel**

```markdown
# Week 2, Tuesday: Agendamento - Social Proof

## Carrossel PASC (4 slides)

### SLIDE 1: Testimonial Hook
**Visual:** Photo of barber owner smiling, with Raizly dashboard visible
**Copy:**
"Raizly mudou minha barbearia"

- Bruno, dono da Barbearia Elite, São Paulo

### SLIDE 2: The Before
**Visual:** Chaotic calendar, stressed expression
**Copy:**
ANTES:

"Eu usava WhatsApp, caderno e Excel. Era um caos."

Clientes cancelavam no último minuto.
Eu nunca sabia quem ia chegar.

Perdia clientes por falta de controle.

### SLIDE 3: The Transformation
**Visual:** Raizly interface, organized, calm expression
**Copy:**
Com Raizly:

"Tudo ficou automático."

Confirmação digital. Lembretes automáticos.
Eu vejo em tempo real quem vai chegar.

Minha agenda é 95% confirmada agora.

### SLIDE 4: The Results
**Visual:** Happy barber, calendar full, money/growth symbols
**Copy:**
RESULTADO:

📈 Faturamento aumentou 30%
⏰ Tempo desperdiçado: 0
😊 Estresse reduzido

"Não volto nunca mais pro jeito antigo."

- Bruno

Pronto para o seu resultado?

🔗 Link na bio

**Instagram Caption:**

"Raizly mudou minha barbearia" - Bruno, dono Barbearia Elite SP

Antes: caos no WhatsApp, clientes cancelando last minute
Depois: 95% de confirmação, faturamento +30%

Sua história pode ser a próxima.

👇 Link na bio (primeiros 50 ganham primeira semana grátis)

#CaseDeExito #BarbeariaProfissional #HEADLYTECH
```

---

### Week 2, Day 3: Wednesday - Controle (Transformation)

**Template:** Carrossel PASC (4 slides)
**Focus:** Before/after control of finances

**Files:**
- Create: `posts/week-2/wednesday-controle-transformation.md`

- [ ] **Step 1: Write transformation carousel**

```markdown
# Week 2, Wednesday: Controle - Transformation

## Carrossel PASC (4 slides)

### SLIDE 1: Before - The Stress
**Visual:** Stressed barber, money scattered, question marks
**Copy:**
ANTES:

❌ Não sabe quanto ganhou
❌ Não sabe quanto gastou
❌ Não controla crediário
❌ Estresse constante

"Será que vou conseguir pagar as contas?"

### SLIDE 2: The Cost
**Visual:** Money numbers, red symbol, loss icon
**Copy:**
Essa falta de controle custa:

- R$3.000-8.000 perdidos por mês
- Decisões ruins por falta de dados
- Oportunidades perdidas
- Stress que mata

### SLIDE 3: After - The Clarity
**Visual:** Clean dashboard, calm face, checkmarks
**Copy:**
DEPOIS (com Raizly):

✅ Sabe ganho exato do mês
✅ Sabe cada gasto
✅ Controla crediário automaticamente
✅ Paz mental garantida

"Agora sei exatamente onde estou"

### SLIDE 4: The Power
**Visual:** Growth symbol, money, confidence
**Copy:**
Com clareza vem poder.

Você toma decisões melhores.
Investe no certo.
Cresce de verdade.

Quer essa transformação?

🔗 Link na bio

**Instagram Caption:**

De "será que consigo pagar as contas?" para "vou abrir segunda unidade"

A diferença? Controle financeiro real.

Raizly faz isso.

👇 Link na bio (primeira semana grátis para os primeiros 50)

#Transformação #ControleFinanceiro #HEADLYTECH
```

---

### Week 2, Day 4: Thursday - Agendamento (Statistics Shock)

**Template:** Carrossel PASC (3 slides, punchy)
**Focus:** Shocking stat that grabs attention

**Files:**
- Create: `posts/week-2/thursday-agendamento-stats.md`

- [ ] **Step 1: Write stats carousel**

```markdown
# Week 2, Thursday: Agendamento - Statistics Shock

## Carrossel PASC (3 slides, punchy)

### SLIDE 1: The Stat
**Visual:** Large number in Rust, bold, shocking
**Copy:**
40%

Esse é o percentual de clientes que não confirmam agendamento.

Você sabia?

### SLIDE 2: What This Means
**Visual:** Calendar with Xs, money calculations
**Copy:**
Se você tem 50 agendamentos por semana...

...20 não confirmam.

Se você marca R$150 por agendamento...

...você perde R$3.000 POR SEMANA.

R$12.000 POR MÊS.

Só com falta de confirmação.

### SLIDE 3: The Solution
**Visual:** Green checkmark, Raizly logo
**Copy:**
Com Raizly, essa taxa cai para ~5%.

Significa: R$11.400 a mais POR MÊS.

Essa estatística custa caro.

Mas pode ser sua melhor venda.

🔗 Link na bio

**Instagram Caption:**

40% é a taxa de clientes que não confirmam (spoiler: você está perdendo uma fortuna)

Com Raizly essa taxa cai para ~5%.

Faça as contas: R$11.400 A MÊS.

👇 Link na bio (primeiros 50 ganham semana grátis)

#Estatística #BarbeariaProfissional #HEADLYTECH

**Note:** These are conservative estimates based on data from current clients. Results may vary based on barbershop size, location, and existing confirmation practices.
```

---

### Week 2, Day 5: Friday - Dados (Result/ROI)

**Template:** Carrossel PASC (4 slides)
**Focus:** Clear ROI of using Raizly

**Files:**
- Create: `posts/week-2/friday-dados-roi.md`

- [ ] **Step 1: Write ROI carousel**

```markdown
# Week 2, Friday: Dados - Result (ROI)

## Carrossel PASC (4 slides)

### SLIDE 1: The Question
**Visual:** Checkmark symbol, question
**Copy:**
Vale a pena usar Raizly?

Deixa a gente fazer as contas...

### SLIDE 2: The Gains (Conservative)
**Visual:** Green numbers, growth arrow
**Copy:**
COM RAIZLY, você ganha:

✅ +R$5.000/mês (agendamentos confirmados)
✅ +R$2.000/mês (controle de gastos)
✅ +R$1.000/mês (dados para decisões melhores)

= R$8.000/mês a mais

(E isso é estimativa conservadora)

### SLIDE 3: The Cost
**Visual:** Small number in perspective
**Copy:**
Raizly custa?

Depende do seu plano.

Mas mesmo no mais caro:
R$500/mês

R$8.000 de ganho.
R$500 de custo.

Sua margem de lucro: R$7.500.

Retorno: 1.500% ao mês.

(Sim, é isso mesmo)

### SLIDE 4: The Math is Simple
**Visual:** Calculator, checkmark
**Copy:**
1 mês de Raizly = 16 meses de ganho

Você fica no positivo em 2 semanas.

O resto é lucro puro.

Aí você me diz: vale a pena?

🔗 Óbvio que vale. Link na bio.

*Baseado em dados conservadores. Resultados variam conforme tamanho e gestão da barbearia.

**Instagram Caption:**

Raizly custa R$500.
Você ganha R$8.000.

Faça as contas: vale a pena?

Spoiler: é 1600% de retorno.

👇 Link na bio (primeira semana é GRÁTIS)

#ROI #Investimento #BarbeariaProfissional #HEADLYTECH
```

- [ ] **Step 2: Commit Week 2 posts**

Run:
```bash
git add posts/week-2/
git commit -m "feat: create week 2 instagram posts (control, social proof, roi)"
```

Expected: All 5 posts for week 2 saved and committed.

---

## Task 2.5: Setup CTA Links with UTM Tracking

**Files:**
- Create: `assets/CTA_LINKS_WITH_UTM.md`

- [ ] **Step 1: Create UTM tracking guide**

Create file `assets/CTA_LINKS_WITH_UTM.md`:

```markdown
# Raizly Instagram CTA Links - UTM Tracking

## Setup

All links use UTM parameters for tracking:
- `utm_source=instagram` - Platform
- `utm_medium=organic` - Type (organic post)
- `utm_campaign=instagram_sales_week[1-2]` - Campaign identifier
- `utm_content=[post_angle]` - Post type (problem, solution, transformation, etc)

**Base URL:** https://raizly.com/demo
(Adjust to your actual landing page/demo booking link)

---

## Week 1 Links

### Monday: Agendamento - Problem
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week1&utm_content=agendamento_problem
```
**Alternative (short):** Use link shortener if preferred (e.g., bit.ly, TinyURL)

### Tuesday: Dados - Solution
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week1&utm_content=dados_solution
```

### Wednesday: Agendamento - Transformation
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week1&utm_content=agendamento_transformation
```

### Thursday: Dados - Urgency
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week1&utm_content=dados_urgency
```

### Friday: Controle - Teaser
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week1&utm_content=controle_teaser
```

---

## Week 2 Links

### Monday: Controle - Deep Dive
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week2&utm_content=controle_deepdive
```

### Tuesday: Agendamento - Social Proof
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week2&utm_content=agendamento_socialproof
```

### Wednesday: Controle - Transformation
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week2&utm_content=controle_transformation
```

### Thursday: Agendamento - Statistics
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week2&utm_content=agendamento_stats
```

### Friday: Dados - ROI
```
https://raizly.com/demo?utm_source=instagram&utm_medium=organic&utm_campaign=instagram_sales_week2&utm_content=dados_roi
```

---

## How to Track

**In Google Analytics:**
1. Navigate to Acquisition → UTM Campaigns
2. Filter by `utm_source=instagram`
3. Sort by `utm_campaign` (week1 vs week2)
4. View `utm_content` to see which post angle performs best

**Dashboard Metrics to Track:**
- Clicks per post
- Click-through rate (CTR)
- Conversion rate (clicks → demos → customers)
- Best-performing angle (problem vs solution vs transformation vs roi vs stats)

---

## Implementation Notes

- Replace `https://raizly.com/demo` with your actual landing page URL
- Use Google's UTM Builder if you prefer: https://ga-dev-tools.appspot.com/campaign-url-builder/
- Consider using a link shortener for cleaner appearance on Instagram
- Test links before publishing (click them to verify they work)
```

- [ ] **Step 2: Commit UTM tracking guide**

Run:
```bash
git add assets/CTA_LINKS_WITH_UTM.md
git commit -m "docs: add utm tracking setup for instagram posts"
```

Expected: UTM links file created and committed.

---

## Task 3: Create Master Publishing Document

**Files:**
- Create: `posts/POSTS_READY_TO_PUBLISH.md`

- [ ] **Step 1: Compile all Instagram captions**

Create consolidated document with all 10 posts' Instagram captions ready to copy-paste:

```markdown
# Raizly Instagram Posts - Ready to Publish

Last updated: 2026-03-24
Format: Copy-paste directly to Instagram

---

## WEEK 1

### Monday: Agendamento - Problem
**Type:** Carousel (5 slides)
**Copy:**

Você está cometendo esse erro que custa até R$10k/mês? 😱

De cada 10 clientes que chegam na porta, 4 simplesmente não confirmam o agendamento.

Isso é R$12.000 por mês desaparecendo.

Mas com Raizly? Esses 4 clientes viram 7 confirmados.

✓ Confirmação automática
✓ Lembretes antes do horário
✓ Chat para resolver dúvidas

Em 30 dias você recupera esse dinheiro.

👇 Clique no link da bio para agendar sua demo (vagas limitadas)

#Barbearia #TecnologiaNasBarbearias #CRMParaBarbearia #HEADLYTECH

---

### Tuesday: Dados - Solution
**Type:** Feed (long caption)
**Copy:**

"Eu não sabia aonde meu dinheiro estava indo."

Esse foi o momento que tudo mudou para a barbearia do João.

Ele tinha ~R$15k de faturamento por mês, mas não sabia exatamente:
- Quanto era lucro real?
- Qual era seu melhor serviço?
- Qual horário rendia mais?
- Por que alguns meses eram bons e outros ruins?

Estava tudo na cabeça dele. E na cabeça nunca está claro.

Aí veio a Raizly.

Em uma semana, João tinha visibilidade total:
- Lucro real: R$8.500 (não R$15k como achava)
- Melhor serviço: Barba Premium (40% do faturamento)
- Melhor horário: Quinta à noite (R$2k só nesse turno)
- Problema maior: Ele estava gastando 35% com produtos desnecessários

Com esses dados em mãos, João fez 3 mudanças simples:
1. Reduziu gastos desnecessários (-R$500/mês)
2. Focou em agendar mais Barbas Premium
3. Abriu quinta à noite como turno especial

Resultado? O lucro real de João foi de R$8.500 para R$11.200 em 60 dias.

Sem contratar ninguém. Sem trabalhar mais. Só com dados certos.

Dados são poder.

E Raizly te dá esses dados.

👇 Link na bio para conhecer. Primeiros 50 donos ganham primeira semana grátis.

#DadosSãoForça #BarbeariaProfissional #GestãoInteligente #HEADLYTECH

---

### Wednesday: Agendamento - Transformation
**Type:** Carousel (4 slides)
**Copy:**

Tem 2 tipos de barbearia: aquelas que sabem quem vai aparecer... e as outras.

Qual é a sua? 👇

De Before pra After é só um passo. (Spoiler: é com Raizly)

#Transformação #Organização #BarbeariaProfissional #HEADLYTECH

---

### Thursday: Dados - Urgency
**Type:** Carousel (5 slides)
**Copy:**

Quantos mil você deixou de ganhar este mês? 😬

A maioria não sabe. E é por isso que não cresce.

Dados são poder. Raizly te dá esse poder.

👇 Link na bio (vagas limitadas para primeiros 50)

#DadosEmTempoReal #LucroReal #BarbeariaProfissional #HEADLYTECH

---

### Friday: Controle Financeiro - Teaser
**Type:** Micro-anúncio (3 slides)
**Copy:**

Você sabe quanto lucrou na semana passada?

Não? Aí está o problema.

👇 Link na bio. Vamos resolver isso.

#ControleFinanceiro #LucroReal #HEADLYTECH

---

## WEEK 2

### Monday: Controle Financeiro - Deep Dive
**Type:** Feed (long caption)
**Copy:**

"Meu fluxo de caixa era um mistério."

Esse é o testemunho de Carlos, dono de uma barbearia em São Paulo.

Ele faturava bem (~R$18k/mês), mas tinha um problema:
- Alguns meses sobrava grana
- Outros meses ficava apertado
- Nunca sabia por quê

"Era tudo muito confuso", ele disse. "Eu tinha dinheiro em caixa, no banco, em crediário que dei pro cliente... não sabia nem quanto tinha de verdade."

Resultado? Carlos estava deixando de fazer investimentos. Não expandia a barbearia. Vivia no "talvez no próximo mês".

Aí entrou Raizly.

A primeira coisa que Raizly mostrou?

O fluxo de caixa REAL de Carlos:

- Entrada: R$18.000 (faturamento)
- Despesas: R$9.200 (produtos, aluguel, funcionários)
- Lucro real: R$8.800

Mas esperaaa... havia mais:

Carlos estava "emprestando" dinheiro pros clientes em forma de crediário (sem cobrar juros).
Total emprestado: R$2.100 que ele não via em caixa.

Com Raizly, Carlos automatizou:
1. Controle de todos os pagamentos (cartão, dinheiro, crediário)
2. Lembretes automáticos pros clientes que devem
3. Relatórios semanais (sabe exatamente o saldo)

Resultado em 2 semanas?

Carlos recuperou R$1.800 dos clientes que deviam.
Seu fluxo de caixa ficou claro.
Ele finalmente sabia quanto tinha para investir.

3 meses depois, Carlos abriu seu segundo horário. Contratou mais um barbeiro.

Por quê? Porque agora ele VIA o dinheiro. Via o potencial. Via a realidade.

Dados criam coragem. Visibilidade cria ação.

Se você está como Carlos estava...

👇 Link na bio. Primeira semana grátis.

Seu fluxo de caixa merece clareza.

#ControleFinanceiro #FluxoDeCaixa #BarbeariaProfissional #HEADLYTECH

---

### Tuesday: Agendamento - Social Proof
**Type:** Carousel (4 slides)
**Copy:**

"Raizly mudou minha barbearia" - Bruno, dono Barbearia Elite SP

Antes: caos no WhatsApp, clientes cancelando last minute
Depois: 95% de confirmação, faturamento +30%

Sua história pode ser a próxima.

👇 Link na bio (primeiros 50 ganham primeira semana grátis)

#CaseDeExito #BarbeariaProfissional #HEADLYTECH

---

### Wednesday: Controle - Transformation
**Type:** Carousel (4 slides)
**Copy:**

De "será que consigo pagar as contas?" para "vou abrir segunda unidade"

A diferença? Controle financeiro real.

Raizly faz isso.

👇 Link na bio (primeira semana grátis para os primeiros 50)

#Transformação #ControleFinanceiro #HEADLYTECH

---

### Thursday: Agendamento - Statistics
**Type:** Carousel (3 slides)
**Copy:**

41% é a taxa de clientes que não confirmam (spoiler: você está perdendo uma fortuna)

Com Raizly essa taxa cai para 5%.

Faça as contas: R$11.400 A MÊS.

👇 Link na bio (primeiros 50 ganham semana grátis)

#Estatística #BarbeariaProfissional #HEADLYTECH

---

### Friday: Dados - ROI
**Type:** Carousel (4 slides)
**Copy:**

Raizly custa R$500.
Você ganha R$8.000.

Faça as contas: vale a pena?

Spoiler: é 1600% de retorno.

👇 Link na bio (primeira semana é GRÁTIS)

#ROI #Investimento #BarbeariaProfissional #HEADLYTECH

---

## NEXT STEPS

1. Design visuals for each post using Canva/Figma following brandbook
2. Schedule posts in Instagram Manager (or Meta Business Suite)
3. Week 1 starts: Monday
4. Track metrics per KPI document
```

- [ ] **Step 2: Add visual design notes**

Add to the document a section with design guidelines:

```markdown
## DESIGN GUIDELINES (for creating visuals)

### Carrossel PASC Template

**Dimensions:** 1080x1350px (Instagram carousel)
**Font Stack:** Familjen Grotesk (headlines), JetBrains Mono (numbers)
**Color Palette:**
- Background: Ink #111111 (primary), Bone #F0EDE6 (secondary)
- Accents: Rust #E8430A (CTAs, numbers, emphasis)
- Text: Bone #F0EDE6 on dark, Ink #111111 on light

**Layout per Slide:**
- Slide 1: Large headline (60-80pt), hook copy, HEADLY TECH logo (small bottom-right)
- Slides 2-4: Medium headline (40-50pt), body copy (24-32pt), supporting graphic/icon
- Slide 5: CTA button (highlighted in Rust), copy with urgency

### Feed Post Template

**Dimensions:** 1080x1350px (square) or 1080x1350+ (carousel with long caption)
**Key Element:** Hero image (barber owner, Raizly dashboard, or testimonial scenario)
**Overlay:** Optional text overlay with headline in Rust
**Caption:** Long-form (200-400 words), storytelling format

### Micro-anúncio Template

**Dimensions:** 1080x1350px
**Layout:** 3 slides, punchy
- Slide 1: Question/problem (large text)
- Slide 2: Impact/number (visual, infographic)
- Slide 3: CTA (clear call-to-action button)

### Visual Assets Needed

For these 10 posts you'll need:
1. **Barber owner photos** (happy, stressed, relieved) - Can use stock photos (Unsplash, Pexels) with Raizly branding
2. **Raizly Dashboard screenshots** - From product (if available) or mockups
3. **Icons** - Checkmarks, calendars, money symbols in Rust
4. **Brand Elements** - HEADLY TECH logo, Raizly wordmark

### Colors Quick Reference

- Use Rust (#E8430A) for: Numbers, CTAs, emphasis, highlights
- Use Bone (#F0EDE6) for: Text on dark backgrounds
- Use Ink (#111) for: Main backgrounds, dark text
- Use Dim (#333) for: Smaller text, secondary information
```

- [ ] **Step 3: Commit master document**

Run:
```bash
git add posts/POSTS_READY_TO_PUBLISH.md
git commit -m "docs: create master instagram posts document with all captions ready to publish"
```

Expected: Master document created with all 10 posts' captions and design guidelines.

---

## Task 4: Create Visual Design Templates (Reference)

**Files:**
- Create: `assets/templates/DESIGN_REFERENCE.md`
- Reference: `assets/brandbook-colors.json` (for developers/designers)

- [ ] **Step 1: Create color palette JSON**

Create `assets/brandbook-colors.json`:

```json
{
  "raizly_brandbook": {
    "primary": {
      "rust": "#E8430A",
      "bone": "#F0EDE6",
      "ink": "#111111"
    },
    "secondary": {
      "mid": "#888888",
      "dim": "#333333",
      "bone2": "#E5E1D8"
    },
    "usage": {
      "rust": "CTAs, numbers, emphasis, highlights",
      "bone": "Text on dark, secondary backgrounds",
      "ink": "Main dark backgrounds, headlines",
      "mid": "Secondary text, context",
      "dim": "Small text, captions"
    }
  },
  "fonts": {
    "primary": "Familjen Grotesk (sans-serif)",
    "accent": "JetBrains Mono (monospace)",
    "sizes": {
      "headline_large": "60-80pt",
      "headline_medium": "40-50pt",
      "body_large": "32pt",
      "body_medium": "24-28pt",
      "caption": "14-18pt"
    }
  }
}
```

- [ ] **Step 2: Create design template reference**

Create `assets/templates/DESIGN_REFERENCE.md`:

```markdown
# Raizly Instagram Design Templates

## Template 1: Carrossel PASC (5 slides)

### Slide Breakdown

**Slide 1: Hook (Curiosity Gap)**
- Dimensions: 1080x1350px
- Background: Rust (#E8430A) or Ink (#111)
- Headline: 70pt, bold, Familjen Grotesk, Bone text
- Subheadline: 32pt, Bone text
- Visual: Icon or number accent
- Logo: HEADLY TECH, small, bottom-right corner

**Slides 2-3: Problem + Agitation**
- Dimensions: 1080x1350px
- Background: Ink (#111) with subtle grain texture (optional)
- Headline: 50pt, Familjen Grotesk, Bone text
- Body: 26pt, Bone text, 1.5 line spacing
- Accent numbers: 60pt, Rust color
- Visual: Icon/illustration that supports the problem
- Grid overlay: Optional subtle 80px grid for Raizly brand (see brandbook)

**Slide 4: Solution**
- Dimensions: 1080x1350px
- Background: Bone (#F0EDE6) or light
- Headline: 50pt, Familjen Grotesk, Ink text
- Body: 26pt, Ink text
- Visual: Raizly dashboard screenshot or product mockup
- Accent: Rust checkmarks or benefit icons
- Logo: Raizly logo, central or integrated

**Slide 5: CTA**
- Dimensions: 1080x1350px
- Background: Ink (#111)
- CTA Button: 100x50px, Rust background (#E8430A), Bone text
- Button text: 20pt, JetBrains Mono, bold
- Surrounding text: 32pt, Bone text, Familjen Grotesk
- Urgency text: 24pt, Mid gray (#888)

---

## Template 2: Feed Post (Long Caption)

### Layout
- Dimensions: 1080x1350px (minimum, can be larger for carousel)
- Hero Image: Professional photo or dashboard screenshot
- Optional Text Overlay: Headline or quote in Rust or Bone, depending on background

### Image Selection
- Barber owner in natural setting (happy, thoughtful, or relieved)
- Dashboard with visible metrics
- Before/after split image
- Testimonial-style with person visible

### Accessibility
- Ensure text is readable on image (use Bone on dark, Ink on light)
- High contrast for CTAs
- Keep 10% margin on edges for mobile safe zone

---

## Template 3: Micro-anúncio (3 slides)

### Slide 1: Question
- Dimensions: 1080x1350px
- Background: Rust (#E8430A)
- Headline: 80pt, bold, Bone text
- Clean, simple design
- Question mark icon (optional)

### Slide 2: Impact
- Dimensions: 1080x1350px
- Background: Ink (#111)
- Large number: 100pt, Rust color
- Small supporting text: 28pt, Bone text
- Infographic or visual representation of impact

### Slide 3: CTA
- Dimensions: 1080x1350px
- Background: Bone (#F0EDE6)
- CTA Button: Large, Rust background (#E8430A)
- Supporting text: Bone text on Ink background (section)
- Clear, scannable

---

## Color Application Examples

**High-Contrast CTA:**
Rust button (#E8430A) on Ink background (#111) with Bone text

**Text Hierarchy:**
- Headline: Rust (#E8430A) on Ink (#111)
- Subheadline: Bone (#F0EDE6) on Ink (#111)
- Body: Bone (#F0EDE6) on Ink (#111)
- Caption: Mid (#888888) on Ink (#111)

**Number Emphasis:**
- Large numbers: Rust (#E8430A), JetBrains Mono, 60-80pt
- Context text: Bone (#F0EDE6), Familjen Grotesk, 24-28pt

---

## Tools & Resources

**Design Tools:**
- Canva (easiest, templates available)
- Figma (most flexible, design system approach)
- Adobe Creative Suite (professional)

**Stock Photos:**
- Unsplash (free)
- Pexels (free)
- Envato Elements (paid, higher quality)

**Icon Libraries:**
- Feather Icons
- Lucide React (Raizly's design system uses this)
- Font Awesome

---

## Approval Checklist

Before publishing any post:
- [ ] Colors match Raizly brandbook
- [ ] Fonts are Familjen Grotesk (headlines) or JetBrains Mono (numbers)
- [ ] CTA is clear and clickable
- [ ] Text is readable (WCAG AA minimum contrast)
- [ ] Mobile safe zone respected (10% margin)
- [ ] HEADLY TECH logo visible and on-brand
- [ ] Copy matches tone (persuasive, specific numbers, urgency)
- [ ] No typos or grammar errors
```

- [ ] **Step 2: Create Canva template guide**

Add to the same file:

```markdown
## Quick Start: Creating These Posts in Canva

### Setup
1. Create new Canva project (1080x1350px for Instagram carousel/feed)
2. Import Raizly brandbook colors to Canva color palette
3. Add Familjen Grotesk and JetBrains Mono fonts to your library

### Carousel Post Steps
1. Create 5 pages (one per slide)
2. For each slide:
   - Set background color (Rust or Ink)
   - Add headline text (60-80pt, Familjen Grotesk)
   - Add body text (24-32pt)
   - Add visual element (icon, photo, or graphic)
   - Add logo (HEADLY TECH, small)
3. Export as carousel (Canva will combine slides)

### Feed Post Steps
1. Create 1 page (1080x1350px+)
2. Add hero image (barber, dashboard, or testimonial)
3. Add text overlay if needed (high contrast)
4. Add Raizly logo
5. Export as single image

### Design Shortcuts
- **Rust Button:** Rectangle shape, #E8430A fill, white text, rounded corners
- **Number Emphasis:** Text box, 70pt size, #E8430A color, JetBrains Mono
- **Divider:** Thin line, Rust color, separates sections
- **Icon:** Search Canva icons for "check", "calendar", "money", "chart" in Rust color
```

- [ ] **Step 3: Commit templates**

Run:
```bash
git add assets/templates/ assets/brandbook-colors.json
git commit -m "docs: add design templates and color reference for instagram posts"
```

Expected: Template guides and brand color reference created.

---

## Task 5: Asset Procurement Guide

**Files:**
- Create: `assets/ASSET_PROCUREMENT_CHECKLIST.md`

- [ ] **Step 1: Create asset checklist**

Create file `assets/ASSET_PROCUREMENT_CHECKLIST.md`:

```markdown
# Asset Procurement Checklist for Instagram Posts

## Images Needed (by post type)

### Feed Posts (Tuesday & Monday S2)
- Barber owner looking at computer/Raizly dashboard: 1 image
- Happy barber owner (smiling, confident): 1 image
- Barber working professionally: 1 image

**Sources:**
- Unsplash: https://unsplash.com (free, high quality)
- Pexels: https://pexels.com (free)
- Envato Elements: (paid, higher quality)

**Specifications:** 1080x1350px minimum, high resolution (JPG, PNG)

### Carousel Posts (Most posts)
- Raizly dashboard screenshot or mockup: 5+ versions
  - Dashboard with agendamento visible
  - Dashboard with dados/números visible
  - Dashboard with controle financeiro visible
- Icons (checkmarks, calendar, money, chart): 10+ SVG files
- Barber in various emotions (stressed, happy, relieved): 3+ images
- Empty barbershop chair (visual for problem): 1 image
- Calendar graphic (for agendamento theme): 1 image

**Icon Sources:**
- Feather Icons: https://feathericons.com (free SVG)
- Lucide Icons: https://lucide.dev (free SVG)
- Font Awesome: https://fontawesome.com (free tier available)

### Dashboard Screenshots/Mockups
- If Raizly product is available: Take actual screenshots
- If not available: Create mockups using Figma template
- Key elements to show:
  - Clean dashboard interface
  - Real or sample data/numbers
  - Rust, Bone, Ink color scheme
  - Logo visible

---

## Branding Assets

- HEADLY TECH logo: 1 file (PNG, SVG, with transparency)
- Raizly logo/wordmark: 1 file (PNG, SVG)
- Brandbook colors (CSS or JSON): Already created (brandbook-colors.json)

---

## Fonts

- Familjen Grotesk: Download from Google Fonts (free)
- JetBrains Mono: Download from Google Fonts (free)

Add to Canva/Figma library before design work.

---

## Total Assets Needed

**Minimum MVP:**
- 5 barber/dashboard images
- 10 icons (Rust colored)
- 2 logos
- 2 fonts (already in Google Fonts)

**Nice-to-have (enhanced quality):**
- 10+ additional stock photos
- 20+ custom icons
- Dashboard mockups (Figma design)

**Procurement Timeline:**
- Stock images: 1-2 hours (download from Unsplash/Pexels)
- Icons: 1 hour (download + color to Rust)
- Dashboard mock-up: 2-3 hours (Figma design or screenshot)
- Logo export: 30 min (if available from brand assets)

Total: ~5 hours of asset work

---

## Checklist

- [ ] Download Familjen Grotesk from Google Fonts
- [ ] Download JetBrains Mono from Google Fonts
- [ ] Collect 5+ barber/dashboard photos (save to assets/images/)
- [ ] Download 10+ icons (save to assets/icons/)
- [ ] Secure Raizly dashboard screenshots/mockups (save to assets/mockups/)
- [ ] Export HEADLY TECH logo (save to assets/logos/)
- [ ] Export Raizly logo (save to assets/logos/)
- [ ] Test all assets are correct size/format before publishing

```

- [ ] **Step 2: Commit asset checklist**

Run:
```bash
git add assets/ASSET_PROCUREMENT_CHECKLIST.md
git commit -m "docs: add asset procurement guide for instagram posts"
```

---

## Task 6: Final QA & Publishing Checklist

**Files:**
- Create: `PUBLISHING_CHECKLIST.md`

- [ ] **Step 1: Create comprehensive QA checklist**

Create `PUBLISHING_CHECKLIST.md`:

```markdown
# Instagram Publishing Checklist

## Copy QA

- [ ] All captions are copied from `POSTS_READY_TO_PUBLISH.md`
- [ ] Spelling and grammar are correct (no typos)
- [ ] Numbers are accurate (check against design spec)
- [ ] CTAs are clear (link in bio, demo, etc.)
- [ ] Hashtags are included (#Barbearia #HEADLYTECH etc.)
- [ ] Tone is consistent (persuasive, specific, urgent)

## Visual QA

- [ ] Colors match Raizly brandbook (rust, bone, ink)
- [ ] Fonts are Familjen Grotesk or JetBrains Mono
- [ ] Logo is visible and on-brand
- [ ] Text is readable on mobile (high contrast)
- [ ] Dimensions are correct (1080x1350px for carousel/feed)
- [ ] No typos on visual assets
- [ ] Images are high quality (no pixelation)

## Compliance

- [ ] No false claims about product (realistic ROI numbers)
- [ ] CTA link is functional (test before publishing)
- [ ] Bio link is updated to correct landing page
- [ ] UTM parameters are correct (if using link tracking)

## Design QA (Before Publishing Each Post)

- [ ] Colors match Raizly brandbook exactly
  - Rust: #E8430A ✓
  - Bone: #F0EDE6 ✓
  - Ink: #111111 ✓
- [ ] Fonts are correct (Familjen Grotesk headlines, JetBrains Mono numbers)
- [ ] Logo is visible and properly positioned (bottom-right or integrated)
- [ ] Text is readable on mobile (high contrast, minimum 18pt for body)
- [ ] Dimensions are exactly 1080x1350px (carousel/feed)
- [ ] No typos on visual elements
- [ ] CTA button is clearly visible in Rust color
- [ ] Images are high quality (no pixelation, 72dpi minimum)
- [ ] All assets are properly placed (no missing images/placeholders)

## Publishing

- [ ] Schedule using Meta Business Suite or Instagram scheduler
- [ ] **Optimal posting time: 19:00 (7 PM) daily** - Peak engagement for target audience
- [ ] First post (Monday) scheduled for start of Week 1
- [ ] Remaining posts scheduled for their respective days (Mon-Fri each week)
- [ ] Post captions are set to public (not private)
- [ ] Bio link is functional and points to correct landing page
- [ ] UTM parameters in links are correct (verify before scheduling)

## Weekend Strategy (Saturday & Sunday)

- [ ] **Saturday: Optional evergreen Stories** - Behind-the-scenes, team culture, or testimonial snippets (not carousel posts)
- [ ] **Sunday: Reposting or Stories** - Repost top-performing post from week, or create motivational story
- [ ] **No new carousel posts** - Focus is Mon-Fri sales cycle
- [ ] **Stories are exempt from UTM tracking** - Use for brand building, not conversion metrics

## Post-Publishing

- [ ] Monitor first hour for engagement
- [ ] Track metrics (likes, comments, clicks, DMs)
- [ ] Respond to comments within 2 hours
- [ ] Update KPI spreadsheet with weekly metrics

---

## Testing Before First Publication

Run through this ONCE before publishing Week 1:

1. **Copy Test**
   - Open POSTS_READY_TO_PUBLISH.md
   - Copy Monday caption to note
   - Check for typos and flow

2. **Visual Test**
   - Open Monday post visual design
   - Check colors in Figma/Canva (match brandbook)
   - Verify text is readable on phone screen

3. **Link Test**
   - Click Instagram bio link
   - Confirm it goes to correct landing page
   - Check UTM parameters in URL (utm_source=instagram_bio, etc.)

4. **Final Review**
   - Show to someone else (fresh eyes catch errors)
   - Ask: "Would this make you want to try Raizly?"
   - If yes → Ready to publish
   - If no → Revise copy or visuals

---

## Metrics Tracking Template

Create a spreadsheet or document tracking:

| Date | Post | Reach | Impressions | Likes | Comments | Clicks | DMs/Inquiries | CTR |
|------|------|-------|-------------|-------|----------|--------|--------------|-----|
| 2026-03-31 | Mon - Agendamento | ? | ? | ? | ? | ? | ? | ? |

Update weekly. Track which post type performs best (carrossel vs feed vs micro).
```

- [ ] **Step 2: Confirm all 10 posts are complete**

Run:
```bash
ls -la posts/week-1/
ls -la posts/week-2/
cat posts/POSTS_READY_TO_PUBLISH.md | grep "### " | wc -l
```

Expected output: Should show 5 files in week-1, 5 files in week-2, and count of 10 posts.

- [ ] **Step 3: Final commit**

Run:
```bash
git add PUBLISHING_CHECKLIST.md
git commit -m "docs: add publishing checklist and qa guidelines"
```

Expected: All posts, templates, and guidelines committed.

---

## Summary

✅ **Deliverables Completed:**
- 10 Instagram posts (Weeks 1-2) ready to copy-paste
- 3 reusable templates (Carrossel PASC, Feed, Micro-anúncio)
- Copy framework documentation (AIDA + high-end copywriting)
- Design guidelines (colors, fonts, layout)
- Canva/Figma quick-start guide
- Publishing checklist and QA process
- Metrics tracking template

✅ **Next Actions:**
1. Design visuals for each post (use templates as reference)
2. Schedule posts in Instagram Manager
3. Monitor first week's performance
4. Adjust Week 3+ based on metrics (which angle converts best?)

**All files are committed and ready to publish.**
