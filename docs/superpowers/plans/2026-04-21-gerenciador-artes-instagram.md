# Gerenciador de Artes Instagram — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Reescrever `gerenciador-artes.html` com preview fullscreen navegável por slide, download PNG 1080×1350px por slide e download de carrossel em ZIP, usando copy honesto baseado nas funcionalidades reais do Raizly.

**Architecture:** Arquivo HTML único com CSS inline e JS inline. Slides renderizados a partir de um array de dados JS (sem hardcode de HTML repetido). Modal fullscreen com navegação por setas/dots/teclado. Download via html2canvas (scale=3 → 1080×1350px) + JSZip para pacote ZIP.

**Tech Stack:** HTML5 + CSS3 + JS vanilla · html2canvas 1.4.1 (CDN) · JSZip 3.10 (CDN) · Google Fonts (Familjen Grotesk + JetBrains Mono)

---

## File Structure

```
gerenciador-artes.html   ← único arquivo de output (substitui versão atual)
  ├── <head>             CDN imports, CSS variables, reset
  ├── <style>            page layout + slide template A + modal
  ├── <body>             header + semana 1 + semana 2 + modal overlay
  └── <script>           DATA (posts array) + renderSlides() + modal JS + download JS
```

---

## Task 1: Esqueleto da página + CSS base

**Files:**
- Create: `gerenciador-artes.html`

- [ ] **Step 1: Criar o arquivo com head, CDN e CSS de reset/variáveis**

Criar `gerenciador-artes.html` com o seguinte conteúdo completo:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Raizly — Gerenciador de Artes</title>
  <link href="https://fonts.googleapis.com/css2?family=Familjen+Grotesk:wght@400;500;700;800&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --rust: #E8430A;
      --bone: #F0EDE6;
      --ink:  #111111;
      --mid:  #888888;
      --dim:  #333333;
      --card-bg: #1a1a1a;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--ink);
      color: var(--bone);
      font-family: 'Familjen Grotesk', sans-serif;
      min-height: 100vh;
    }

    /* ── HEADER ── */
    .page-header {
      position: sticky; top: 0; z-index: 50;
      background: rgba(17,17,17,0.96);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--dim);
      padding: 18px 40px;
      display: flex; align-items: center; justify-content: space-between;
    }
    .h-brand { display: flex; align-items: center; gap: 10px; }
    .h-brand-wm { font-weight: 800; font-size: 20px; letter-spacing: -1px; }
    .h-meta { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--mid); }

    /* ── HERO ── */
    .hero {
      padding: 48px 40px 36px;
      text-align: center;
      border-bottom: 1px solid var(--dim);
    }
    .hero h1 { font-size: clamp(26px,4vw,46px); font-weight: 800; margin-bottom: 10px; }
    .hero h1 em { color: var(--rust); font-style: normal; }
    .hero p { font-size: 15px; color: var(--mid); max-width: 500px; margin: 0 auto 24px; line-height: 1.6; }
    .notice {
      display: inline-flex; align-items: flex-start; gap: 8px;
      background: rgba(232,67,10,0.1); border: 1px solid rgba(232,67,10,0.25);
      border-radius: 8px; padding: 10px 16px;
      font-size: 13px; color: var(--bone); line-height: 1.5;
      max-width: 560px; text-align: left;
    }

    /* ── WEEK SECTION ── */
    .week-section { padding: 36px 40px 52px; }
    .week-header { display: flex; align-items: center; gap: 12px; margin-bottom: 8px; }
    .week-badge {
      font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700;
      background: var(--rust); color: white;
      padding: 4px 12px; border-radius: 100px; text-transform: uppercase; letter-spacing: 1px;
    }
    .week-title { font-size: 18px; font-weight: 700; }
    .week-divider { border: none; border-top: 1px solid var(--dim); margin: 16px 0 24px; }

    /* ── CARD GRID ── */
    .arts-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 20px;
    }

    /* ── ART CARD ── */
    .art-card {
      background: var(--card-bg);
      border-radius: 12px; overflow: hidden;
      border: 1px solid rgba(255,255,255,0.05);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .art-card:hover { transform: translateY(-3px); box-shadow: 0 20px 50px rgba(0,0,0,0.5); }

    /* slide thumbnail — proporção 1080/1350 */
    .slide-thumb-wrap {
      width: 100%; aspect-ratio: 1080/1350;
      overflow: hidden; cursor: pointer; position: relative;
    }
    .slide-thumb-wrap:hover .thumb-overlay { opacity: 1; }
    .thumb-overlay {
      position: absolute; inset: 0;
      background: rgba(0,0,0,0.45);
      display: flex; align-items: center; justify-content: center;
      opacity: 0; transition: opacity 0.2s;
      font-size: 13px; font-weight: 700; color: white; gap: 6px;
    }

    /* ── CARD FOOTER ── */
    .card-foot { padding: 12px 14px 14px; }
    .card-meta { display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px; }
    .card-title { font-size: 13px; font-weight: 700; }
    .card-tag {
      font-family: 'JetBrains Mono', monospace; font-size: 9px;
      color: var(--mid); background: rgba(255,255,255,0.06);
      padding: 2px 8px; border-radius: 100px; text-transform: uppercase;
    }
    .card-desc { font-size: 11px; color: var(--mid); line-height: 1.5; margin-bottom: 12px; }

    .dl-row { display: flex; gap: 6px; }
    .btn-zip {
      flex: 1; background: var(--rust); color: white; border: none;
      border-radius: 8px; padding: 10px; font-family: 'Familjen Grotesk', sans-serif;
      font-size: 13px; font-weight: 700; cursor: pointer; transition: opacity .2s;
    }
    .btn-zip:hover { opacity: 0.88; }
    .btn-zip.loading { opacity: 0.6; pointer-events: none; }
    .btn-ind {
      background: #2a2a2a; color: var(--bone); border: none;
      border-radius: 8px; padding: 10px 12px;
      font-family: 'Familjen Grotesk', sans-serif; font-size: 12px;
      cursor: pointer; white-space: nowrap; transition: background .2s;
    }
    .btn-ind:hover { background: #333; }

    /* ── PAGE FOOTER ── */
    .page-footer { border-top: 1px solid var(--dim); text-align: center; padding: 28px 40px; }
    .page-footer p { font-size: 12px; color: var(--mid); line-height: 1.7; }

    /* ── TOAST ── */
    #toast {
      position: fixed; bottom: 24px; left: 50%;
      transform: translateX(-50%) translateY(80px);
      background: #1e1e1e; border: 1px solid var(--rust);
      color: var(--bone); padding: 10px 20px;
      border-radius: 100px; font-size: 13px; font-weight: 600;
      transition: transform 0.25s; z-index: 999; white-space: nowrap;
    }
    #toast.show { transform: translateX(-50%) translateY(0); }
  </style>
</head>
<body>
  <div id="toast"></div>
  <p style="padding:40px;color:#888;text-align:center">Carregando...</p>
</body>
</html>
```

- [ ] **Step 2: Abrir no browser e verificar**

```bash
open "/Users/romariomarques/Downloads/Raizly/Raizly Downloads/Redes Sociais Raizly/gerenciador-artes.html"
```

Esperado: página escura, fonte carregada, sem erros no console.

---

## Task 2: CSS do Slide Template A (zonas fixas)

**Files:**
- Modify: `gerenciador-artes.html` — adicionar CSS dentro do `<style>` existente, antes do `</style>`

- [ ] **Step 1: Adicionar CSS do template de slide**

Inserir antes de `</style>`:

```css
    /* ══════════════════════════════════════
       SLIDE TEMPLATE A — ZONAS FIXAS
       Proporção 1080×1350 (Instagram)
       Header 14% · Body flex:1 · Footer 13%
    ══════════════════════════════════════ */

    /* container do slide — usado no thumb E no modal */
    .slide-canvas {
      width: 100%; height: 100%;
      display: flex; flex-direction: column;
      overflow: hidden; position: relative;
      font-family: 'Familjen Grotesk', sans-serif;
    }

    /* HEADER — numerador + tag */
    .sl-header {
      height: 14%; flex-shrink: 0;
      background: rgba(0,0,0,0.22);
      display: flex; align-items: center; justify-content: space-between;
      padding: 0 clamp(12px, 4%, 28px);
    }
    .sl-num {
      font-family: 'JetBrains Mono', monospace;
      font-size: clamp(8px, 1.6vw, 13px);
      color: rgba(255,255,255,0.55);
      letter-spacing: 0.5px;
    }
    .sl-tag {
      font-family: 'JetBrains Mono', monospace;
      font-size: clamp(7px, 1.4vw, 11px);
      color: rgba(255,255,255,0.4);
      text-transform: uppercase; letter-spacing: 1px;
    }

    /* BODY — conteúdo principal */
    .sl-body {
      flex: 1;
      display: flex; flex-direction: column;
      justify-content: center; align-items: center;
      text-align: center;
      padding: clamp(14px, 4%, 40px) clamp(14px, 5%, 44px);
      gap: clamp(8px, 2%, 16px);
    }

    .sl-icon { font-size: clamp(28px, 7vw, 52px); line-height: 1; }

    .sl-headline {
      font-weight: 800;
      font-size: clamp(13px, 3.2vw, 28px);
      line-height: 1.15;
    }

    .sl-body-text {
      font-size: clamp(10px, 2.2vw, 16px);
      line-height: 1.5;
      opacity: 0.85;
    }

    /* lista de features (slide 2) */
    .sl-features {
      display: flex; flex-direction: column; gap: clamp(6px, 1.5%, 10px);
      width: 100%; text-align: left;
    }
    .sl-feat {
      display: flex; align-items: flex-start; gap: 8px;
      font-size: clamp(10px, 2vw, 14px); line-height: 1.4;
    }
    .sl-feat-dot {
      width: clamp(6px, 1.2vw, 8px); height: clamp(6px, 1.2vw, 8px);
      border-radius: 50%; flex-shrink: 0; margin-top: 4px;
    }

    /* CTA strip (slide 4) */
    .sl-cta-url {
      font-family: 'JetBrains Mono', monospace;
      font-size: clamp(9px, 1.8vw, 14px);
      background: rgba(0,0,0,0.25);
      padding: clamp(6px,1.5%,10px) clamp(12px,3%,20px);
      border-radius: 6px;
      color: rgba(255,255,255,0.9);
    }

    /* FOOTER — logo + dots */
    .sl-footer {
      height: 13%; flex-shrink: 0;
      display: flex; align-items: center; justify-content: space-between;
      padding: 0 clamp(12px, 4%, 28px);
      border-top: 1px solid rgba(255,255,255,0.08);
    }

    /* logo raizly inline no footer */
    .sl-logo {
      display: flex; align-items: center; gap: clamp(4px, 1%, 7px);
    }
    .sl-logo-wm {
      font-weight: 800; letter-spacing: -0.5px;
      font-size: clamp(9px, 1.8vw, 14px);
      color: rgba(255,255,255,0.5);
    }
    .sl-dots { display: flex; gap: clamp(3px, 0.8vw, 5px); }
    .sl-dot {
      width: clamp(4px, 0.9vw, 6px); height: clamp(4px, 0.9vw, 6px);
      border-radius: 50%; background: rgba(255,255,255,0.2);
    }
    .sl-dot.active { background: var(--rust); }

    /* ── FUNDOS DE SLIDE ── */
    .bg-rust { background: linear-gradient(135deg, #E8430A 0%, #c43208 100%); color: var(--bone); }
    .bg-ink  { background: linear-gradient(to bottom, #111111 0%, #1a1a1a 100%); color: var(--bone); }
    .bg-bone {
      background: var(--bone); color: var(--ink);
    }
    .bg-bone .sl-header { background: rgba(17,17,17,0.08); }
    .bg-bone .sl-num, .bg-bone .sl-tag { color: rgba(17,17,17,0.4); }
    .bg-bone .sl-footer { border-top: 1px solid rgba(17,17,17,0.08); }
    .bg-bone .sl-logo-wm { color: rgba(17,17,17,0.4); }
    .bg-bone .sl-dot { background: rgba(17,17,17,0.15); }
    .bg-bone .sl-dot.active { background: var(--rust); }
    .bg-bone .sl-feat-dot { background: var(--rust); }
    .bg-bone .sl-body-text { color: rgba(17,17,17,0.7); }
    .bg-bone .sl-headline { color: var(--ink); }

    .bg-rust .sl-feat-dot { background: rgba(255,255,255,0.8); }
    .bg-ink  .sl-feat-dot { background: var(--rust); }
```

- [ ] **Step 2: Verificar no browser**

Recarregar a página. Não há slides ainda, mas verificar que não houve erro de parse CSS no console.

---

## Task 3: CSS do Modal

**Files:**
- Modify: `gerenciador-artes.html` — adicionar CSS do modal antes de `</style>`

- [ ] **Step 1: Inserir CSS do modal**

Inserir antes de `</style>`:

```css
    /* ══════════════════════════════════════
       MODAL FULLSCREEN
    ══════════════════════════════════════ */
    #modal {
      display: none;
      position: fixed; inset: 0; z-index: 200;
      background: rgba(0,0,0,0.93);
      align-items: center; justify-content: center;
      gap: clamp(12px, 3vw, 32px);
      padding: 20px;
    }
    #modal.open { display: flex; }

    .modal-arrow {
      width: 48px; height: 48px; border-radius: 50%;
      background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.1);
      display: flex; align-items: center; justify-content: center;
      font-size: 22px; color: white; cursor: pointer; flex-shrink: 0;
      transition: background 0.2s;
      user-select: none;
    }
    .modal-arrow:hover { background: rgba(255,255,255,0.15); }
    .modal-arrow.hidden { visibility: hidden; }

    .modal-center {
      display: flex; flex-direction: column; align-items: center;
      gap: 16px; flex: 1; max-width: 480px;
    }

    .modal-info {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px; color: var(--mid); text-align: center;
    }

    /* slide no modal — proporção 1080/1350, ocupa ~75vh */
    .modal-slide-wrap {
      width: 100%;
      /* mantém proporção e limita altura a 75vh */
      aspect-ratio: 1080 / 1350;
      max-height: 75vh;
      max-width: calc(75vh * 1080 / 1350);
      border-radius: 12px; overflow: hidden;
      box-shadow: 0 32px 100px rgba(0,0,0,0.9);
    }

    .modal-dots {
      display: flex; gap: 8px; justify-content: center;
    }
    .modal-dot {
      width: 7px; height: 7px; border-radius: 50%;
      background: rgba(255,255,255,0.2); cursor: pointer;
      transition: background 0.2s;
    }
    .modal-dot.active { background: var(--rust); }

    .modal-actions { display: flex; gap: 8px; }
    .modal-btn-zip {
      background: var(--rust); color: white; border: none;
      border-radius: 9px; padding: 12px 22px;
      font-family: 'Familjen Grotesk', sans-serif; font-size: 14px; font-weight: 700;
      cursor: pointer; transition: opacity .2s;
    }
    .modal-btn-zip:hover { opacity: 0.88; }
    .modal-btn-zip.loading { opacity: 0.6; pointer-events: none; }
    .modal-btn-ind {
      background: #2a2a2a; color: var(--bone); border: none;
      border-radius: 9px; padding: 12px 16px;
      font-family: 'Familjen Grotesk', sans-serif; font-size: 13px;
      cursor: pointer; transition: background .2s;
    }
    .modal-btn-ind:hover { background: #333; }

    /* painel de slides individuais (expandível) */
    .ind-panel {
      display: none; flex-direction: column; gap: 6px;
      background: #1a1a1a; border-radius: 10px; padding: 12px;
      width: 100%; max-height: 200px; overflow-y: auto;
    }
    .ind-panel.open { display: flex; }
    .ind-row {
      display: flex; align-items: center; gap: 10px;
      font-size: 12px; color: var(--bone);
    }
    .ind-thumb {
      width: 32px; height: 40px; border-radius: 4px;
      flex-shrink: 0; overflow: hidden;
    }
    .ind-name { flex: 1; font-family: 'JetBrains Mono', monospace; font-size: 10px; color: var(--mid); }
    .ind-dl {
      background: var(--dim); color: var(--bone); border: none;
      border-radius: 5px; padding: 5px 10px; font-size: 11px;
      cursor: pointer; transition: background .2s;
    }
    .ind-dl:hover { background: var(--rust); }

    .modal-close {
      position: fixed; top: 16px; right: 20px;
      font-size: 24px; color: rgba(255,255,255,0.4); cursor: pointer;
      z-index: 201; line-height: 1; transition: color .2s;
    }
    .modal-close:hover { color: white; }
```

---

## Task 4: HTML do body + SVG da logo (helper)

**Files:**
- Modify: `gerenciador-artes.html` — substituir `<body>...</body>` completo

- [ ] **Step 1: Substituir o body pelo HTML estrutural**

Substituir todo o conteúdo entre `<body>` e `</body>` por:

```html
  <!-- ── OWL SVG TEMPLATE (clonado via JS em cada slide) ── -->
  <svg id="owl-tpl" style="display:none" viewBox="0 0 72 72" fill="none" xmlns="http://www.w3.org/2000/svg">
    <rect width="72" height="72" rx="14" fill="rgba(0,0,0,0.25)"/>
    <g transform="rotate(-22,36,36)">
      <rect x="24" y="6" width="24" height="60" rx="12" fill="#F0EDE6"/>
      <circle cx="36" cy="22" r="6.5" fill="#111"/>
      <circle cx="36" cy="22" r="3"   fill="#E8430A"/>
      <circle cx="37.5" cy="20.5" r="1.2" fill="white"/>
      <circle cx="36" cy="40" r="6.5" fill="#111"/>
      <circle cx="36" cy="40" r="3"   fill="#E8430A"/>
      <circle cx="37.5" cy="38.5" r="1.2" fill="white"/>
      <polygon points="36,29 33,33 39,33" fill="#111"/>
    </g>
    <polygon points="26,10 31,18 21,18" fill="#E8430A"/>
    <polygon points="46,10 51,18 41,18" fill="#E8430A"/>
  </svg>

  <!-- ── HEADER ── -->
  <header class="page-header">
    <div class="h-brand">
      <svg width="28" height="28" viewBox="0 0 72 72" fill="none">
        <rect width="72" height="72" rx="18" fill="#1a1a1a"/>
        <g transform="rotate(-22,36,36)">
          <rect x="24" y="6" width="24" height="60" rx="12" fill="#F0EDE6"/>
          <circle cx="36" cy="22" r="6.5" fill="#111"/><circle cx="36" cy="22" r="3" fill="#E8430A"/>
          <circle cx="37.5" cy="20.5" r="1.2" fill="white"/>
          <circle cx="36" cy="40" r="6.5" fill="#111"/><circle cx="36" cy="40" r="3" fill="#E8430A"/>
          <circle cx="37.5" cy="38.5" r="1.2" fill="white"/>
          <polygon points="36,29 33,33 39,33" fill="#111"/>
        </g>
        <polygon points="26,10 31,18 21,18" fill="#E8430A"/>
        <polygon points="46,10 51,18 41,18" fill="#E8430A"/>
      </svg>
      <span class="h-brand-wm">raizly</span>
    </div>
    <div class="h-meta">10 artes · 2 semanas · Instagram 1080×1350px</div>
  </header>

  <!-- ── HERO ── -->
  <div class="hero">
    <h1>Gerenciador de <em>Artes</em></h1>
    <p>Clique em qualquer arte para preview. Baixe em PNG 1080×1350px ou pacote ZIP do carrossel.</p>
    <div class="notice">
      <span>✓</span>
      <span>Copy baseado nas <strong>funcionalidades reais</strong> do Raizly — sem estatísticas inventadas.</span>
    </div>
  </div>

  <!-- ── SEMANA 1 ── -->
  <section class="week-section">
    <div class="week-header">
      <span class="week-badge">Semana 1</span>
      <span class="week-title">Segunda → Sexta</span>
    </div>
    <hr class="week-divider">
    <div class="arts-grid" id="grid-s1"></div>
  </section>

  <!-- ── SEMANA 2 ── -->
  <section class="week-section" style="padding-top:0">
    <div class="week-header">
      <span class="week-badge">Semana 2</span>
      <span class="week-title">Segunda → Sexta</span>
    </div>
    <hr class="week-divider">
    <div class="arts-grid" id="grid-s2"></div>
  </section>

  <!-- ── PAGE FOOTER ── -->
  <footer class="page-footer">
    <p><strong>raizly</strong> · Sistema de gestão para barbearias<br>
    Conteúdo honesto — baseado nas funcionalidades reais do produto</p>
  </footer>

  <!-- ── MODAL ── -->
  <div id="modal">
    <span class="modal-close" onclick="closeModal()">✕</span>
    <button class="modal-arrow" id="modal-prev" onclick="modalNav(-1)">‹</button>
    <div class="modal-center">
      <div class="modal-info" id="modal-info"></div>
      <div class="modal-slide-wrap" id="modal-slide-wrap"></div>
      <div class="modal-dots" id="modal-dots"></div>
      <div class="modal-actions">
        <button class="modal-btn-zip" id="modal-btn-zip">⬇ Baixar ZIP</button>
        <button class="modal-btn-ind" id="modal-btn-ind" onclick="toggleIndPanel()">slide a slide</button>
      </div>
      <div class="ind-panel" id="ind-panel"></div>
    </div>
    <button class="modal-arrow" id="modal-next" onclick="modalNav(1)">›</button>
  </div>

  <!-- ── TOAST ── -->
  <div id="toast"></div>
```

---

## Task 5: Dados dos posts (JS DATA array)

**Files:**
- Modify: `gerenciador-artes.html` — adicionar `<script>` antes de `</body>`

- [ ] **Step 1: Inserir script com array de dados dos posts**

Adicionar antes de `</body>`:

```html
  <script>
  /* ══════════════════════════════════════════════════════════
     DATA — 10 posts, 4 slides cada
     slide.bg: 'rust' | 'ink' | 'bone'
     slide.type: 'hook' | 'features' | 'benefit' | 'cta'
  ══════════════════════════════════════════════════════════ */
  const POSTS = [
    // ── SEMANA 1 ──────────────────────────────────────────
    {
      id: 's1-seg', week: 1,
      title: 'Segunda — Agendamento',
      desc: 'Link próprio, confirmação digital e histórico de clientes.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'rust', type: 'hook',
          num: '01', tag: 'agendamento',
          icon: '📅',
          headline: 'Agendamento online que o cliente confirma sozinho.',
          body: 'Sem ligação. Sem WhatsApp.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Como funciona:',
          features: [
            'Link de agendamento exclusivo da sua barbearia',
            'Cliente escolhe horário e barbeiro preferido',
            'Confirmação digital automática — sem você fazer nada',
            'Histórico completo de cada cliente no sistema'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Você sabe exatamente quem vai aparecer hoje.',
          body: 'Agenda clara, sem surpresa, sem mensagem perdida.'
        },
        {
          bg: 'rust', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Conheça o Raizly.',
          body: 'Sistema de gestão feito para barbearia.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's1-ter', week: 1,
      title: 'Terça — Agenda Digital',
      desc: 'Agenda centralizada no sistema. Sem WhatsApp, sem papel.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'ink', type: 'hook',
          num: '01', tag: 'agenda',
          icon: '💬',
          headline: 'Chega de agenda no WhatsApp. Existe um jeito melhor.',
          body: 'Agenda centralizada. Sem mensagem perdida.'
        },
        {
          bg: 'rust', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Com o Raizly:',
          features: [
            'Agenda centralizada no sistema — não no celular pessoal',
            'Cada barbeiro com sua própria fila de atendimento',
            'Cliente vê os horários disponíveis em tempo real',
            'Você enxerga o dia inteiro com 1 olhada'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Todas as informações em um lugar.',
          body: 'Sem procurar mensagem. Sem anotar em papel. Sem esquecer.'
        },
        {
          bg: 'ink', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Teste grátis.',
          body: 'Sem cartão. Sem compromisso.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's1-qua', week: 1,
      title: 'Quarta — Dashboard',
      desc: 'Faturamento, ticket médio e agendamentos em tempo real.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'bone', type: 'hook',
          num: '01', tag: 'dashboard',
          icon: '📊',
          headline: 'Veja os números da sua barbearia — agora.',
          body: 'Dashboard completo em tempo real.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'O que você vê:',
          features: [
            'Faturamento do dia, semana e mês',
            'Ticket médio por serviço e por barbeiro',
            'Agendamentos confirmados vs. pendentes',
            'Horário e serviço mais procurados'
          ]
        },
        {
          bg: 'rust', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Tome decisões com base em dados reais.',
          body: 'Não em chute. Não em memória. Dados que aparecem sozinhos.'
        },
        {
          bg: 'ink', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Acesse o dashboard.',
          body: 'Tudo que importa, em um só lugar.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's1-qui', week: 1,
      title: 'Quinta — Financeiro',
      desc: 'Caixa, despesas, crediário e relatórios automáticos.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'rust', type: 'hook',
          num: '01', tag: 'financeiro',
          icon: '💰',
          headline: 'Controle financeiro feito para barbearia.',
          body: 'Caixa, despesas, crediário e relatórios.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'O que o sistema controla:',
          features: [
            'Entradas e saídas do caixa por forma de pagamento',
            'Despesas categorizadas — produtos, aluguel, outros',
            'Crediário: controle de quem deve e quanto',
            'Relatório semanal e mensal gerado automaticamente'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Sabe quanto entrou, quanto saiu e quem deve.',
          body: 'Sem planilha. Sem chute. Sem surpresa no fim do mês.'
        },
        {
          bg: 'rust', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Comece a controlar.',
          body: 'Financeiro claro desde o primeiro dia.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's1-sex', week: 1,
      title: 'Sexta — Comunicação',
      desc: 'Chat integrado e lembretes automáticos sem WhatsApp pessoal.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'rust', type: 'hook',
          num: '01', tag: 'comunicação',
          icon: '💬',
          headline: 'Fale com seus clientes direto pelo sistema.',
          body: 'Sem usar o WhatsApp pessoal.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Comunicação integrada:',
          features: [
            'Chat direto com o cliente dentro do sistema',
            'Lembrete automático de agendamento enviado antes do horário',
            'Notificações de confirmação sem você precisar enviar',
            'Histórico de todas as conversas por cliente'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'A comunicação da sua barbearia fica organizada e profissional.',
          body: 'Separada do pessoal. Registrada. Sem perder mensagem.'
        },
        {
          bg: 'ink', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Veja como funciona.',
          body: 'Comunicação profissional com seus clientes.',
          cta_url: 'raizly.com.br'
        }
      ]
    },

    // ── SEMANA 2 ──────────────────────────────────────────
    {
      id: 's2-seg', week: 2,
      title: 'Segunda — Equipe',
      desc: 'Agenda individual por barbeiro, preferência do cliente e comissões.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'ink', type: 'hook',
          num: '01', tag: 'equipe',
          icon: '✂️',
          headline: 'Gerencie toda a sua equipe de barbeiros.',
          body: 'Cada um com sua agenda, fila e desempenho.'
        },
        {
          bg: 'rust', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Gestão de equipe:',
          features: [
            'Cada barbeiro com seus serviços e horários próprios',
            'Cliente escolhe o barbeiro preferido ao agendar',
            'Faturamento individual de cada profissional',
            'Controle de comissões direto no sistema'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Visibilidade total da equipe.',
          body: 'Quem atendeu mais. Quem gerou mais receita. Tudo claro.'
        },
        {
          bg: 'ink', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Configure sua equipe.',
          body: 'Cada barbeiro no lugar certo.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's2-ter', week: 2,
      title: 'Terça — Relatórios',
      desc: 'Serviço mais vendido, horário de pico e ticket médio automáticos.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'bone', type: 'hook',
          num: '01', tag: 'relatórios',
          icon: '📈',
          headline: 'Relatórios que o sistema gera. Você só olha.',
          body: 'Sem montar planilha. Sem exportar nada.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Gerado automaticamente:',
          features: [
            'Serviço mais agendado e mais rentável',
            'Horário e dia de maior movimento',
            'Ticket médio por serviço e por período',
            'Clientes novos vs. clientes recorrentes'
          ]
        },
        {
          bg: 'rust', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Informação pronta toda semana.',
          body: 'Você toma decisões melhores sem trabalhar mais para isso.'
        },
        {
          bg: 'bone', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Veja seus relatórios.',
          body: 'Dados do seu negócio, sempre atualizados.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's2-qua', week: 2,
      title: 'Quarta — Pagamentos',
      desc: 'Dinheiro, cartão, pix e crediário com controle automático.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'rust', type: 'hook',
          num: '01', tag: 'pagamentos',
          icon: '💳',
          headline: 'Dinheiro, cartão, pix e crediário — tudo no sistema.',
          body: 'Sem anotação em papel. Sem esquecer quem deve.'
        },
        {
          bg: 'ink', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'Formas de pagamento:',
          features: [
            'Dinheiro — registra na hora, entra no caixa',
            'Cartão (débito e crédito) — lançado com forma separada',
            'Pix — confirmação manual, entra no fluxo',
            'Crediário — controle de quem deve, quanto e quando'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'O sistema guarda cada centavo que entrou e saiu.',
          body: 'Sem papel. Sem post-it. Sem risco de esquecer.'
        },
        {
          bg: 'rust', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Conheça o módulo financeiro.',
          body: 'Controle completo do caixa da sua barbearia.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's2-qui', week: 2,
      title: 'Quinta — Automação',
      desc: 'Fluxo completo: agendamento → confirmação → lembrete → atendimento.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'ink', type: 'hook',
          num: '01', tag: 'automação',
          icon: '⚡',
          headline: 'O sistema avisa o cliente. Você não precisa fazer nada.',
          body: 'Lembrete automático antes do horário marcado.'
        },
        {
          bg: 'rust', type: 'features',
          num: '02', tag: 'funcionalidade',
          headline: 'O fluxo automático:',
          features: [
            '① Cliente agenda pelo link da sua barbearia',
            '② Recebe confirmação automática na hora',
            '③ Lembrete enviado antes do horário marcado',
            '④ Cliente aparece. Você atende. Sem trabalho extra.'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Menos no-show. Mais previsibilidade.',
          body: 'Sua agenda funciona sem você gerenciar cada agendamento manualmente.'
        },
        {
          bg: 'ink', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Ative a automação.',
          body: 'Configure uma vez. Funciona pra sempre.',
          cta_url: 'raizly.com.br'
        }
      ]
    },
    {
      id: 's2-sex', week: 2,
      title: 'Sexta — Raizly Completo',
      desc: 'Todas as funcionalidades integradas em um só sistema.',
      tag: 'Carrossel',
      slides: [
        {
          bg: 'ink', type: 'hook',
          num: '01', tag: 'raizly',
          icon: '💈',
          headline: 'Um sistema. Tudo que sua barbearia precisa.',
          body: 'Desenvolvido para o dia a dia do setor.'
        },
        {
          bg: 'rust', type: 'features',
          num: '02', tag: 'funcionalidades',
          headline: 'Tudo integrado:',
          features: [
            'Agendamento online com confirmação digital',
            'Financeiro completo: caixa, despesas, crediário',
            'Gestão de equipe e comissões',
            'Dashboard · Relatórios · Chat · Lembretes'
          ]
        },
        {
          bg: 'bone', type: 'benefit',
          num: '03', tag: 'resultado',
          headline: 'Feito para barbearia.',
          body: 'Cada funcionalidade pensada para o dia a dia do setor — não um sistema genérico adaptado.'
        },
        {
          bg: 'rust', type: 'cta',
          num: '04', tag: 'raizly',
          headline: 'Comece agora.',
          body: 'Gestão profissional para sua barbearia.',
          cta_url: 'raizly.com.br'
        }
      ]
    }
  ];
  </script>
```

---

## Task 6: Função renderSlide() e renderCards()

**Files:**
- Modify: `gerenciador-artes.html` — adicionar segundo `<script>` antes de `</body>`

- [ ] **Step 1: Inserir funções de render**

Adicionar novo `<script>` após o script de dados:

```html
  <script>
  /* ══════════════════════════════════
     RENDER — converte dados em HTML
  ══════════════════════════════════ */

  // SVG do owl raizly (inline, sem dependência externa)
  function owlSVG(size = 18, opacity = 0.5) {
    const fill = `rgba(255,255,255,${opacity})`;
    return `<svg width="${size}" height="${size}" viewBox="0 0 72 72" fill="none" style="flex-shrink:0">
      <rect width="72" height="72" rx="14" fill="rgba(0,0,0,0.25)"/>
      <g transform="rotate(-22,36,36)">
        <rect x="24" y="6" width="24" height="60" rx="12" fill="#F0EDE6"/>
        <circle cx="36" cy="22" r="6.5" fill="#111"/>
        <circle cx="36" cy="22" r="3" fill="#E8430A"/>
        <circle cx="37.5" cy="20.5" r="1.2" fill="white"/>
        <circle cx="36" cy="40" r="6.5" fill="#111"/>
        <circle cx="36" cy="40" r="3" fill="#E8430A"/>
        <circle cx="37.5" cy="38.5" r="1.2" fill="white"/>
        <polygon points="36,29 33,33 39,33" fill="#111"/>
      </g>
      <polygon points="26,10 31,18 21,18" fill="#E8430A"/>
      <polygon points="46,10 51,18 41,18" fill="#E8430A"/>
    </svg>`;
  }

  // Gera o HTML de um slide completo (Template A — zonas fixas)
  function renderSlide(slide, totalSlides, postId, slideIndex) {
    const dotsHTML = Array.from({length: totalSlides}, (_, i) =>
      `<div class="sl-dot${i === slideIndex ? ' active' : ''}"></div>`
    ).join('');

    let bodyContent = '';

    if (slide.type === 'hook') {
      bodyContent = `
        ${slide.icon ? `<div class="sl-icon">${slide.icon}</div>` : ''}
        <div class="sl-headline">${slide.headline}</div>
        <div class="sl-body-text">${slide.body}</div>
      `;
    } else if (slide.type === 'features') {
      const featsHTML = slide.features.map(f =>
        `<div class="sl-feat">
          <div class="sl-feat-dot"></div>
          <span>${f}</span>
        </div>`
      ).join('');
      bodyContent = `
        <div class="sl-headline" style="align-self:flex-start;text-align:left">${slide.headline}</div>
        <div class="sl-features">${featsHTML}</div>
      `;
    } else if (slide.type === 'benefit') {
      bodyContent = `
        <div class="sl-headline">${slide.headline}</div>
        <div class="sl-body-text">${slide.body}</div>
      `;
    } else if (slide.type === 'cta') {
      bodyContent = `
        <div class="sl-headline">${slide.headline}</div>
        <div class="sl-body-text">${slide.body}</div>
        <div class="sl-cta-url">${slide.cta_url}</div>
      `;
    }

    // logo no footer: cor invertida no fundo bone
    const logoWmColor = slide.bg === 'bone' ? 'rgba(17,17,17,0.4)' : 'rgba(255,255,255,0.5)';

    return `
      <div class="slide-canvas bg-${slide.bg}"
           data-post="${postId}" data-slide="${slideIndex}">
        <div class="sl-header">
          <span class="sl-num">slide ${slide.num} / ${String(totalSlides).padStart(2,'0')}</span>
          <span class="sl-tag">${slide.tag}</span>
        </div>
        <div class="sl-body">${bodyContent}</div>
        <div class="sl-footer">
          <div class="sl-logo">
            ${owlSVG(slide.bg === 'bone' ? 16 : 16, slide.bg === 'bone' ? 0.25 : 0.45)}
            <span class="sl-logo-wm" style="color:${logoWmColor}">raizly</span>
          </div>
          <div class="sl-dots">${dotsHTML}</div>
        </div>
      </div>`;
  }

  // Gera o card completo (thumb do slide 1 + footer com botões)
  function renderCard(post) {
    const s0 = post.slides[0];
    const slideHTML = renderSlide(s0, post.slides.length, post.id, 0);

    return `
      <div class="art-card" id="card-${post.id}">
        <div class="slide-thumb-wrap" onclick="openModal('${post.id}', 0)">
          ${slideHTML}
          <div class="thumb-overlay">👁 Visualizar</div>
        </div>
        <div class="card-foot">
          <div class="card-meta">
            <span class="card-title">${post.title}</span>
            <span class="card-tag">${post.tag}</span>
          </div>
          <p class="card-desc">${post.desc}</p>
          <div class="dl-row">
            <button class="btn-zip" onclick="downloadZip('${post.id}', this)">
              ⬇ ZIP (${post.slides.length} slides)
            </button>
            <button class="btn-ind" onclick="openModal('${post.id}', 0); setTimeout(()=>openIndPanel(),200)">
              slide a slide
            </button>
          </div>
        </div>
      </div>`;
  }

  // Injeta os cards nos grids
  function init() {
    const s1 = POSTS.filter(p => p.week === 1);
    const s2 = POSTS.filter(p => p.week === 2);
    document.getElementById('grid-s1').innerHTML = s1.map(renderCard).join('');
    document.getElementById('grid-s2').innerHTML = s2.map(renderCard).join('');
  }

  init();
  </script>
```

- [ ] **Step 2: Verificar no browser**

Recarregar. Esperado: grid com 5 cards em cada semana, cada card mostrando o slide 1 com proporção 1080/1350, logo raizly no rodapé de cada slide, sem sobreposição de elementos.

---

## Task 7: JavaScript do Modal

**Files:**
- Modify: `gerenciador-artes.html` — adicionar terceiro `<script>` antes de `</body>`

- [ ] **Step 1: Inserir lógica do modal**

```html
  <script>
  /* ══════════════════════════════════
     MODAL — open / navigate / close
  ══════════════════════════════════ */

  let _modalPost = null;   // post atual
  let _modalIdx  = 0;      // índice do slide atual

  function openModal(postId, slideIdx) {
    _modalPost = POSTS.find(p => p.id === postId);
    _modalIdx  = slideIdx;
    _renderModal();
    document.getElementById('modal').classList.add('open');
    document.body.style.overflow = 'hidden';
  }

  function closeModal() {
    document.getElementById('modal').classList.remove('open');
    document.body.style.overflow = '';
    // fecha painel individual se aberto
    document.getElementById('ind-panel').classList.remove('open');
  }

  function modalNav(dir) {
    const total = _modalPost.slides.length;
    _modalIdx = (_modalIdx + dir + total) % total;
    _renderModal();
  }

  function _renderModal() {
    const post  = _modalPost;
    const slide = post.slides[_modalIdx];
    const total = post.slides.length;

    // info
    document.getElementById('modal-info').textContent =
      `${post.title} · slide ${_modalIdx + 1} / ${total}`;

    // slide ampliado
    document.getElementById('modal-slide-wrap').innerHTML =
      renderSlide(slide, total, post.id, _modalIdx);

    // dots
    document.getElementById('modal-dots').innerHTML =
      Array.from({length: total}, (_, i) =>
        `<div class="modal-dot${i === _modalIdx ? ' active' : ''}" onclick="openModal('${post.id}',${i})"></div>`
      ).join('');

    // setas
    document.getElementById('modal-prev').classList.toggle('hidden', total <= 1);
    document.getElementById('modal-next').classList.toggle('hidden', total <= 1);

    // botão ZIP
    const btnZip = document.getElementById('modal-btn-zip');
    btnZip.textContent = `⬇ Baixar ZIP (${total} slides)`;
    btnZip.onclick = () => downloadZip(post.id, btnZip);

    // painel individual
    _buildIndPanel();
  }

  function _buildIndPanel() {
    const post = _modalPost;
    document.getElementById('ind-panel').innerHTML = post.slides.map((sl, i) => {
      const thumbHTML = renderSlide(sl, post.slides.length, post.id, i);
      return `<div class="ind-row">
        <div class="ind-thumb">${thumbHTML}</div>
        <span class="ind-name">${post.id}-slide-${i+1}.png</span>
        <button class="ind-dl" onclick="downloadSingle('${post.id}', ${i}, this)">⬇</button>
      </div>`;
    }).join('');
  }

  function openIndPanel() {
    document.getElementById('ind-panel').classList.toggle('open');
  }
  function toggleIndPanel() { openIndPanel(); }

  // Fechar com ESC e navegar com setas do teclado
  document.addEventListener('keydown', e => {
    if (!document.getElementById('modal').classList.contains('open')) return;
    if (e.key === 'Escape')      closeModal();
    if (e.key === 'ArrowLeft')   modalNav(-1);
    if (e.key === 'ArrowRight')  modalNav(1);
  });

  // Fechar ao clicar no overlay (fora do conteúdo)
  document.getElementById('modal').addEventListener('click', e => {
    if (e.target === document.getElementById('modal')) closeModal();
  });
  </script>
```

- [ ] **Step 2: Verificar no browser**

Recarregar. Clicar em qualquer card. Esperado:
- Modal abre com slide ampliado (~75vh)
- Setas funcionam para navegar entre os 4 slides
- Dots mudam de posição
- ESC e teclas ← → funcionam
- Clicar fora fecha
- Botão "slide a slide" abre painel com miniaturas

---

## Task 8: Download PNG individual (html2canvas 1080×1350)

**Files:**
- Modify: `gerenciador-artes.html` — adicionar quarto `<script>` antes de `</body>`

- [ ] **Step 1: Inserir funções de download**

```html
  <script>
  /* ══════════════════════════════════
     DOWNLOAD — PNG e ZIP
  ══════════════════════════════════ */

  // Renderiza 1 slide em um div temporário (1080×1350) e captura via html2canvas
  async function captureSlide(post, slideIdx) {
    const slide = post.slides[slideIdx];
    const total = post.slides.length;

    // Container temporário fora da tela, tamanho real do Instagram
    const container = document.createElement('div');
    container.style.cssText = `
      position: fixed;
      left: -9999px; top: -9999px;
      width: 1080px; height: 1350px;
      overflow: hidden;
      font-family: 'Familjen Grotesk', sans-serif;
    `;
    container.innerHTML = renderSlide(slide, total, post.id, slideIdx);
    document.body.appendChild(container);

    // Aplica classes de tamanho ao slide-canvas interno
    const canvas = container.querySelector('.slide-canvas');
    canvas.style.width  = '1080px';
    canvas.style.height = '1350px';
    // Ajusta font-sizes para resolução real (a proporção clamp usa vw — fix para off-screen)
    canvas.style.fontSize = '18px';

    try {
      const result = await html2canvas(container, {
        width:  1080,
        height: 1350,
        scale:  1,           // container já está em 1080×1350, scale=1 é o tamanho real
        useCORS: true,
        allowTaint: true,
        backgroundColor: null,
        logging: false,
      });
      return result.toDataURL('image/png');
    } finally {
      document.body.removeChild(container);
    }
  }

  // Download de 1 slide
  async function downloadSingle(postId, slideIdx, btn) {
    const post = POSTS.find(p => p.id === postId);
    const orig = btn ? btn.textContent : '';
    if (btn) { btn.textContent = '…'; btn.disabled = true; }

    try {
      const dataUrl = await captureSlide(post, slideIdx);
      const link = document.createElement('a');
      link.download = `${post.id}-slide-${slideIdx + 1}.png`;
      link.href = dataUrl;
      link.click();
      showToast(`✓ ${link.download} baixado`);
    } catch (err) {
      console.error(err);
      showToast('Erro ao gerar PNG');
    } finally {
      if (btn) { btn.textContent = orig; btn.disabled = false; }
    }
  }

  // Download ZIP com todos os slides
  async function downloadZip(postId, btn) {
    const post = POSTS.find(p => p.id === postId);
    const orig = btn ? btn.textContent : '';
    if (btn) { btn.classList.add('loading'); btn.textContent = 'Gerando…'; }

    try {
      const zip = new JSZip();
      for (let i = 0; i < post.slides.length; i++) {
        if (btn) btn.textContent = `Slide ${i+1}/${post.slides.length}…`;
        const dataUrl = await captureSlide(post, i);
        // remove prefixo "data:image/png;base64,"
        const base64 = dataUrl.split(',')[1];
        zip.file(`${post.id}-slide-${i+1}.png`, base64, { base64: true });
      }
      const blob = await zip.generateAsync({ type: 'blob' });
      const link = document.createElement('a');
      link.download = `${post.id}-carrossel.zip`;
      link.href = URL.createObjectURL(blob);
      link.click();
      URL.revokeObjectURL(link.href);
      showToast(`✓ ${link.download} baixado (${post.slides.length} slides)`);
    } catch (err) {
      console.error(err);
      showToast('Erro ao gerar ZIP');
    } finally {
      if (btn) { btn.classList.remove('loading'); btn.textContent = orig; }
    }
  }

  // Toast
  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 3200);
  }
  </script>
```

- [ ] **Step 2: Testar download de 1 slide**

Abrir o modal de qualquer post → "slide a slide" → clicar ⬇ no slide 1.

Esperado:
- Botão mostra `…` durante captura
- Arquivo `s1-seg-slide-1.png` baixa
- Dimensões do arquivo: 1080×1350px
- Logo raizly visível, sem sobreposição de elementos

- [ ] **Step 3: Testar download ZIP**

Clicar "⬇ ZIP (4 slides)" em qualquer card.

Esperado:
- Botão mostra "Slide 1/4…", "Slide 2/4…" etc.
- Arquivo `s1-seg-carrossel.zip` baixa
- ZIP contém 4 arquivos PNG, cada um 1080×1350px

---

## Task 9: Ajuste de font-size no captureSlide (off-screen fix)

**Files:**
- Modify: `gerenciador-artes.html` — melhorar a função `captureSlide`

O problema: `clamp()` com `vw` calcula com base na janela, não no container off-screen.
Fix: usar font-size base fixo no container e valores em `em` para os slides capturados.

- [ ] **Step 1: Substituir a função `captureSlide` pela versão com font-size fixo**

Localizar `async function captureSlide` e substituir por:

```javascript
  async function captureSlide(post, slideIdx) {
    const slide = post.slides[slideIdx];
    const total = post.slides.length;

    const container = document.createElement('div');
    container.style.cssText = `
      position: fixed; left: -9999px; top: -9999px;
      width: 1080px; height: 1350px;
      overflow: hidden;
      font-family: 'Familjen Grotesk', sans-serif;
      font-size: 18px;
    `;

    // Gera HTML do slide
    container.innerHTML = renderSlide(slide, total, post.id, slideIdx);

    const slideEl = container.querySelector('.slide-canvas');
    // Dimensões fixas — garante 1080×1350 no output
    slideEl.style.width  = '1080px';
    slideEl.style.height = '1350px';
    // Override de clamp() para valores fixos em px (escala 1080px)
    slideEl.querySelectorAll('.sl-headline').forEach(el => { el.style.fontSize = '36px'; el.style.lineHeight = '1.15'; });
    slideEl.querySelectorAll('.sl-body-text').forEach(el => { el.style.fontSize = '22px'; });
    slideEl.querySelectorAll('.sl-num, .sl-tag').forEach(el => { el.style.fontSize = '16px'; });
    slideEl.querySelectorAll('.sl-logo-wm').forEach(el => { el.style.fontSize = '18px'; });
    slideEl.querySelectorAll('.sl-feat').forEach(el => { el.style.fontSize = '20px'; });
    slideEl.querySelectorAll('.sl-cta-url').forEach(el => { el.style.fontSize = '18px'; });
    slideEl.querySelectorAll('.sl-icon').forEach(el => { el.style.fontSize = '64px'; });
    slideEl.querySelectorAll('.sl-dot').forEach(el => { el.style.width = '8px'; el.style.height = '8px'; });

    document.body.appendChild(container);
    try {
      const result = await html2canvas(container, {
        width: 1080, height: 1350, scale: 1,
        useCORS: true, allowTaint: true,
        backgroundColor: null, logging: false,
      });
      return result.toDataURL('image/png');
    } finally {
      document.body.removeChild(container);
    }
  }
```

- [ ] **Step 2: Testar download novamente**

Baixar 1 PNG e verificar:
- Texto legível e bem proporcionado
- Logo raizly (owl + wordmark) visível no rodapé
- Sem texto cortado ou sobreposto
- Fundo correto para cada slide

---

## Task 10: Revisão final e abertura no browser

**Files:**
- Modify: `gerenciador-artes.html` — sem mudanças, apenas verificação

- [ ] **Step 1: Abrir e verificar todos os 10 posts**

```bash
open "/Users/romariomarques/Downloads/Raizly/Raizly Downloads/Redes Sociais Raizly/gerenciador-artes.html"
```

Checklist visual:
- [ ] Header fixo com logo raizly
- [ ] 5 cards na Semana 1, 5 cards na Semana 2
- [ ] Cada card mostra o slide 1 com proporção 1080/1350
- [ ] Logo raizly (owl + "raizly") no rodapé de cada slide
- [ ] Sem sobreposição de elementos em nenhum slide
- [ ] Hover no card mostra "👁 Visualizar"
- [ ] Clique abre modal fullscreen com slide grande (~75vh)
- [ ] Setas de navegação funcionam
- [ ] ESC fecha o modal
- [ ] Botão ZIP baixa arquivo `.zip` com PNGs 1080×1350
- [ ] Botão "slide a slide" abre painel e permite baixar por slide
- [ ] Toast aparece após cada download
- [ ] Copy de todos os slides é honesto, sem estatísticas inventadas
- [ ] CTA de todo slide 4 aponta para `raizly.com.br`

- [ ] **Step 2: Verificar dimensões do PNG baixado**

Abrir qualquer PNG baixado no Preview (Mac) e confirmar: **1080 × 1350 pixels**.

---

## Self-Review

**Spec coverage:**
- ✓ Preview fullscreen com navegação → Task 7
- ✓ Slide grande no modal (~75vh) → Task 3 CSS `.modal-slide-wrap`
- ✓ Download ZIP → Task 8 `downloadZip()`
- ✓ Download por slide → Task 8 `downloadSingle()`
- ✓ 1080×1350px → Task 9 `captureSlide()` off-screen fix
- ✓ Template A zonas fixas → Task 2 CSS + Task 6 `renderSlide()`
- ✓ Logo raizly em todo slide → Task 6 `owlSVG()` no footer
- ✓ 10 posts × 4 slides → Task 5 POSTS array
- ✓ Copy honesto sem estatísticas → Task 5 conteúdo dos slides
- ✓ Teclado (ESC, ←, →) → Task 7

**Nenhum placeholder ou TBD encontrado.**

**Consistência de tipos:**
- `renderSlide(slide, total, postId, slideIdx)` — usado em Task 6, 7, 8 ✓
- `captureSlide(post, slideIdx)` — retorna `Promise<string>` (dataURL) ✓
- `downloadZip(postId, btn)` e `downloadSingle(postId, slideIdx, btn)` ✓
- `openModal(postId, slideIdx)` ✓
