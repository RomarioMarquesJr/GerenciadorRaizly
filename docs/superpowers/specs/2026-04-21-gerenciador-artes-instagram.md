# Spec — Gerenciador de Artes Instagram (Raizly)

**Data:** 2026-04-21  
**Status:** Aprovado

---

## Objetivo

Reescrever `gerenciador-artes.html` como uma página de gestão completa das 10 artes de Instagram da Raizly, com preview fullscreen navegável por slide, download em PNG 1080×1350px e download de carrossel em ZIP.

---

## Decisões de Design (aprovadas no brainstorm)

| Decisão | Escolha |
|---|---|
| Modal de preview | Fullscreen com setas de navegação + dots |
| Tamanho do slide no modal | Grande — ocupa ~80vh da tela |
| Download carrossel | ZIP (principal) + por slide (secundário) |
| Template de slide | Zonas fixas: Header · Body · Footer |
| Resolução de download | 1080×1350px (html2canvas scale=3) |
| Logo | SVG owl + wordmark "raizly" em todo slide |

---

## Estrutura de Cada Slide (Template A — Zonas Fixas)

```
┌─────────────────────────────┐  ← 14% altura
│  slide X / Y        [tema]  │  ← Header (fundo escuro translúcido)
├─────────────────────────────┤
│                             │
│       CONTEÚDO CENTRAL      │  ← Body (flex:1, centralizado)
│   título · subtítulo · CTA  │
│                             │
├─────────────────────────────┤  ← 13% altura
│  raizly [owl svg]   ● ○ ○ ○ │  ← Footer (logo + dots de posição)
└─────────────────────────────┘
```

**Regras:**
- Nenhum elemento posicionado absolutamente sobre outro
- Margem interna mínima: 40px horizontal, 24px vertical
- Fundo sempre sólido (sem transparência no body)
- Logo raizly (SVG owl + wordmark) presente em TODOS os slides

---

## 10 Posts — Estrutura de Slides (4 slides cada)

### Padrão de 4 slides por carrossel:
| Slide | Função | Fundo |
|---|---|---|
| 1 | Hook — pergunta ou provocação | Rust `#E8430A` |
| 2 | Funcionalidade — o que o sistema faz | Ink `#111111` |
| 3 | Benefício — o que o dono ganha | Bone `#F0EDE6` (texto ink) |
| 4 | CTA — chamada para testar | Rust `#E8430A` |

### Semana 1

**SEG — Agendamento (link próprio + confirmação)**
- S1: "Agendamento online que o cliente confirma sozinho. Sem ligação. Sem WhatsApp."
- S2: Link de agendamento próprio · Cliente escolhe horário e barbeiro · Confirmação digital automática
- S3: Você sabe exatamente quem vai aparecer hoje. Agenda clara, sem surpresa, sem mensagem perdida.
- S4: Conheça o Raizly · raizly.com.br

**TER — Agenda Digital (sem WhatsApp)**
- S1: "Chega de agenda no WhatsApp. Existe um jeito melhor."
- S2: Agenda centralizada no sistema · Cada barbeiro com sua fila · Cliente vê horários em tempo real
- S3: Todas as informações em um lugar. Sem procurar mensagem. Sem anotar em papel.
- S4: Teste grátis · raizly.com.br

**QUA — Dashboard (dados em tempo real)**
- S1: "Veja os números da sua barbearia — agora."
- S2: Faturamento do dia · Ticket médio por serviço · Agendamentos da semana — tudo atualizado ao vivo
- S3: Tome decisões com base em dados reais, não em chute. Seu negócio fica visível.
- S4: Acesse o dashboard · raizly.com.br

**QUI — Financeiro (caixa, despesas, crediário)**
- S1: "Controle financeiro feito para barbearia."
- S2: Registro de entradas e saídas · Despesas categorizadas · Crediário sem papel · Relatório automático
- S3: Sabe quanto entrou, quanto saiu e quem deve — sem planilha, sem chute.
- S4: Comece a controlar · raizly.com.br

**SEX — Comunicação (chat + lembretes)**
- S1: "Fale com seus clientes direto pelo sistema."
- S2: Chat integrado com o cliente · Lembrete automático de agendamento · Sem usar WhatsApp pessoal
- S3: A comunicação da sua barbearia fica organizada e profissional, sem misturar com o pessoal.
- S4: Veja como funciona · raizly.com.br

### Semana 2

**SEG — Equipe (gestão de barbeiros)**
- S1: "Gerencie toda a sua equipe de barbeiros."
- S2: Cada barbeiro com agenda própria · Cliente escolhe o preferido · Controle de comissões no sistema
- S3: Visibilidade total da equipe: quem atendeu mais, quem gerou mais receita.
- S4: Configure sua equipe · raizly.com.br

**TER — Relatórios (automáticos)**
- S1: "Relatórios que o sistema gera. Você só olha."
- S2: Serviço mais agendado · Horário de pico · Ticket médio · Clientes novos vs. retorno
- S3: Informação pronta toda semana, sem montar planilha, sem exportar nada.
- S4: Veja seus relatórios · raizly.com.br

**QUA — Pagamentos (crediário + formas)**
- S1: "Dinheiro, cartão, pix e crediário — tudo no sistema."
- S2: Registra cada pagamento na hora · Crediário com controle automático · Sabe quem deve sem anotar
- S3: Sem papel. Sem esquecimento. O sistema guarda cada centavo que entra e saiu.
- S4: Conheça o módulo financeiro · raizly.com.br

**QUI — Automação (fluxo de lembrete)**
- S1: "O sistema avisa o cliente. Você não precisa fazer nada."
- S2: Cliente agenda → recebe confirmação automática → lembrete antes do horário → aparece
- S3: Menos no-show. Mais previsibilidade. Sua agenda funciona sem você gerenciar manualmente.
- S4: Ative a automação · raizly.com.br

**SEX — Raizly Completo**
- S1: "Um sistema. Tudo que sua barbearia precisa."
- S2: Agendamento · Financeiro · Equipe · Dashboard · Comunicação · Relatórios — integrados
- S3: Desenvolvido para barbearia. Cada funcionalidade pensada para o dia a dia do setor.
- S4: Comece agora · raizly.com.br

---

## UX — Fluxo do Modal

```
Clique no card
  → overlay escuro (rgba 0,0,0,0.92)
  → slide ampliado centralizado (~80vh, proporção 1080/1350)
  → seta ‹ / › para navegar entre slides
  → dots indicam posição (slide X / total)
  → botão "⬇ Baixar ZIP (X slides)" — gera todos e compacta
  → botão "slide a slide" — abre lista para download individual
  → clique fora ou ✕ fecha
  → teclas ← → e ESC funcionam
```

---

## Tecnologia

- **HTML + CSS + JS** puro (sem build, sem framework)
- **html2canvas 1.4.1** via CDN — captura cada `.slide-canvas` em scale=3 → 1080×1350px
- **JSZip** via CDN — empacota os PNGs do carrossel em `.zip`
- **Fontes:** Google Fonts (Familjen Grotesk + JetBrains Mono)
- **Logo SVG** inline em cada slide (sem dependência externa)

---

## Critérios de Qualidade (Copywriting)

Aplicados a todos os 10 posts:
- ✓ Copy baseado em funcionalidades reais do sistema
- ✓ Sem estatísticas fabricadas
- ✓ Benefício claro em cada slide (não só feature)
- ✓ CTA direto com URL real
- ✓ Tom direto, sem buzzwords ("otimizar", "alavancar", "sinergia")
- ✓ Uma ideia por slide
- ✓ Linguagem do dono de barbearia, não de tech

---

## Arquivos

- **Output:** `gerenciador-artes.html` (substitui versão atual)
- **Sem dependências locais** — tudo via CDN ou inline
