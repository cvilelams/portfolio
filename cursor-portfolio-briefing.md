# Portfolio Design Briefing — Carolina Vilela
**For use in Cursor or any AI code editor**

This document is the single source of truth for the visual system of this portfolio.
Every page, component, and style decision must derive from the tokens and principles defined here.
Do not improvise outside this system.

---

## 1. Design Intent

**Aesthetic direction:** Moderna e técnica — referências Vercel, Linear, Stripe.
**Emotional register:** Precisa, confiante, séria sem ser fria. Comunica sênioridade de produto.
**What a recruiter/design lead should feel:** "Essa pessoa pensa em sistemas, não só em telas."
**Typography personality:** Estrutural. Display bold com auxiliar monospace — contraste entre expressão e precisão.
**Color philosophy:** 95% neutro. Um único acento cromático (azul) usado apenas em métricas-chave, estado ativo e CTAs primários.

---

## 2. Typography System

### Font Families
```css
--font-display: 'DM Sans', sans-serif;         /* headlines, h1–h3, nav logo */
--font-mono:   'DM Mono', monospace;        /* labels, tags, metadata, body copy, captions */
```

**Import (in `<head>` or CSS `@import`):**
```css
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,700&family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300&display=swap');
```

### Type Scale
| Role | Font | Size | Weight | Letter-spacing | Line-height |
|---|---|---|---|---|---|
| Hero H1 | DM Sans | 62px | 700 | -0.03em | 1.0 |
| Hero H1 em (italic voice) | DM Sans | 62px | 400 | -0.03em | 1.0 |
| Section headline | DM Sans | 32px | 700 | -0.025em | 1.2 |
| Project title (card) | DM Sans | 20px | 700 | -0.02em | 1.2 |
| Experience role | DM Sans | 17px | 600 | -0.01em | 1.3 |
| Body / hero sub | DM Mono | 16px | 300 | 0 | 1.65 |
| Project description | DM Mono | 12px | 300 | 0 | 1.6 |
| Labels / tags / nav | DM Mono | 10–12px | 400 | 0.06–0.12em | 1.5 |
| Meta values (sidebar) | DM Mono | 11px | 400 | 0.04em | 1.5 |
| Caption / footer | DM Mono | 11px | 400 | 0.06em | 1.5 |

### Typography Rules
- Headlines sempre em `font-family: var(--font-display)`. Nunca usar display em body/labels.
- Todos os labels, tags, timestamps, badges: `font-family: var(--font-mono); text-transform: uppercase; letter-spacing: 0.06–0.12em`.
- `font-weight: 700` apenas no hero H1. Seções usam 700. Nunca usar 800 fora do hero.
- Métricas de impacto (ex: "28s → 12s"): `font-family: var(--font-mono); color: var(--accent)`.
- Itálico no hero H1 é intencional — comunicar voz, não ênfase. Não replicar em outros headings.

---

## 3. Color System

```css
:root {
  /* Base */
  --ink:            #0f1117;   /* texto primário — headings, conteúdo principal */
  --ink-muted:      #6b7280;   /* texto secundário — descrições, subtítulos */
  --ink-faint:      #9ca3af;   /* texto terciário — labels, metadados, captions */

  /* Surfaces */
  --surface:        #ffffff;   /* background principal */
  --surface-2:      #f8f9fb;   /* sidebar hero, hero-right, about-right */
  --surface-3:      #f1f3f6;   /* tags, placeholders de imagem, skill dots bg */

  /* Borders */
  --border:         #e5e7eb;   /* divisórias principais, bordas de cards */
  --border-strong:  #d1d5db;   /* bordas com mais peso, botão ghost underline */

  /* Accent — USE SPARINGLY */
  --accent:         #2563eb;   /* métricas de impacto, estado ativo, badge "Current", CTA primário */
  --accent-pale:    #eff4ff;   /* background do badge "Current" */
}
```

### Regras de cor (não negociáveis)
1. **O acento azul aparece em no máximo 3 lugares por página.** Mais que isso, perde força.
2. **Nunca usar `--accent` em texto de corpo ou headings.** Apenas em métricas, badges funcionais e CTA primário.
3. **Backgrounds coloridos são proibidos.** A única exceção é `--surface-2` e `--surface-3` (neutros quase-brancos).
4. **Hover states:** `background: var(--surface-2)` — nunca cor de acento em hover de card.
5. **Bordas:** sempre `1px solid var(--border)`. Nunca `2px`. Nunca `border-radius` em elementos com `border-left`/`border-top` isolados.

---

## 4. Spacing System

Base unit: **8px**. Todos os espaçamentos são múltiplos de 8.

```css
--space-1:   8px
--space-2:  16px
--space-3:  24px
--space-4:  32px
--space-5:  40px
--space-6:  48px
--space-8:  64px
--space-10: 80px
```

**Padding de seção (horizontal):** sempre `48px` (lateral) — mantém o ritmo de grid em toda a página.
**Padding de seção (vertical):** `64px` para hero, `40–48px` para seções menores.
**Padding interno de cards de projeto:** `28px 32px 32px`.

---

## 5. Layout & Grid

### Estrutura da página
Largura máxima do container: `900px`, centralizado, `margin: 0 auto`.

### Grid de componentes

| Componente | Grid |
|---|---|
| Hero | `grid-template-columns: 1fr 320px` |
| Projects | `grid-template-columns: 1fr 1fr` |
| Experience row | `grid-template-columns: 200px 1fr 160px` |
| About strip | `grid-template-columns: 1fr 1fr` |
| Skills grid (inside about) | `grid-template-columns: 1fr 1fr` |

### Bordas como elemento de layout
A divisão entre seções é feita com `border-bottom: 1px solid var(--border)` — **não com margin/padding sozinhos**.
Colunas são divididas por `border-right: 1px solid var(--border)`.
Isso cria a linguagem de "grid editorial" do sistema — consistente em toda a página.

---

## 6. Components

### Navigation
```css
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 28px 48px;
  border-bottom: 1px solid var(--border);
}
.nav-logo {
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--ink-muted);
  letter-spacing: 0.04em;
}
.nav-links a {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-muted);
  letter-spacing: 0.06em;
  text-transform: uppercase;
  text-decoration: none;
}
.nav-links a.active { color: var(--ink); }
.nav-links a:hover  { color: var(--ink); }
```
Gap entre links: `32px`.

---

### Hero
Estrutura: grid 2 colunas (`1fr 320px`). Coluna esquerda tem `border-right`. Coluna direita tem `background: var(--surface-2)`.

**Hero tag (acima do H1):**
```css
.hero-tag {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--accent);
  letter-spacing: 0.12em;
  text-transform: uppercase;
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 32px;
}
.hero-tag::before {
  content: '';
  display: inline-block;
  width: 20px;
  height: 1px;
  background: var(--accent);
}
```

**H1 com voz dupla:**
```html
<h1 class="hero-h1">
  I'm Carolina,<br>
  <em>I design for<br>real outcomes.</em>
</h1>
```
O `<em>` recebe `color: var(--ink-muted); font-weight: 400` — não é itálico padrão.

**Hero sidebar (coluna direita):**
- Foto circular (ou iniciais como placeholder) em aspect-ratio 1:1
- Tabela de metadados abaixo: status, role, location, focus
- Cada linha: `display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border)`
- Label: `var(--font-mono) 10px var(--ink-faint) uppercase tracking-wide`
- Value: `var(--font-mono) 11px var(--ink-muted)`

---

### Project Cards
```css
.project-card {
  border-right: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  cursor: pointer;
  transition: background 0.15s;
}
.project-card:nth-child(even) { border-right: none; }
.project-card:hover { background: var(--surface-2); }
```

**Thumbnail:** `width: 100%; aspect-ratio: 16/9; background: var(--surface-3); overflow: hidden`

**Tags:** `font-family: var(--font-mono); font-size: 10px; background: var(--surface-3); padding: 4px 10px; text-transform: uppercase; letter-spacing: 0.06em`. Sem border-radius.

**Métrica de impacto (no rodapé do card):**
```css
.project-metric {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--accent);  /* único uso do accent no card */
}
```

**Arrow hover:**
```css
.project-arrow {
  font-size: 18px;
  color: var(--ink-muted);
  opacity: 0;
  transition: opacity 0.15s, transform 0.15s;
}
.project-card:hover .project-arrow {
  opacity: 1;
  transform: translateX(4px);
}
```

---

### Experience Section
Grid de 3 colunas por linha: `200px 1fr 160px`. Gap: `32px`.

| Coluna | Conteúdo | Estilo |
|---|---|---|
| 1 | Período (ex: "Sep 2025 — Present") | `var(--font-mono) 11px var(--ink-faint)` |
| 2 | Role + Company + Description | Role: DM Sans 17px 600; Company: mono 12px muted; Desc: mono 12px faint 300 |
| 3 | Badge (ex: "Current") | `var(--font-mono) 10px uppercase; background: var(--accent-pale); color: var(--accent); padding: 5px 12px` |

Cada linha separada por `border-bottom: 1px solid var(--border)`. Última linha sem borda.

---

### Buttons

**Primary (CTA):**
```css
.btn-primary {
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  background: var(--ink);
  color: #fff;
  padding: 12px 24px;
  border: none;
  cursor: pointer;
  border-radius: 0;  /* sem arredondamento — faz parte da linguagem técnica */
}
.btn-primary:hover { opacity: 0.85; }
```

**Ghost / text link:**
```css
.btn-ghost {
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  background: none;
  color: var(--ink-muted);
  padding: 12px 0;
  border: none;
  border-bottom: 1px solid var(--border-strong);
  cursor: pointer;
}
.btn-ghost:hover { color: var(--ink); }
```

---

### Section Headers
Faixa horizontal com `border-bottom: 1px solid var(--border)` e `padding: 40px 48px 32px`. Dois elementos: título (esquerda) e contador (direita).
```css
.section-title {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--ink-faint);
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
```

---

## 7. Motion & Interaction

Princípio: **motion funcional, não decorativo.** Apenas dois tipos de transição na página inteira.

```css
/* 1. Card hover — background shift */
.project-card { transition: background 0.15s ease; }

/* 2. Arrow reveal no hover */
.project-arrow { transition: opacity 0.15s ease, transform 0.15s ease; }

/* 3. Link color transitions */
a, button { transition: color 0.15s ease, opacity 0.15s ease; }
```

Sem animações de scroll, sem parallax, sem fade-in de elementos. A página carrega estática — a qualidade está no detalhe, não no movimento.

---

## 8. Pages to Build

### `index.html` — Home (priority)
Seções em ordem:
1. `<nav>` — logo esquerda, links direita
2. `<section class="hero">` — grid 2 colunas
3. Section header "Selected Work" + grid de 2 cards
4. Section header "Experience" + linhas de experiência
5. About strip — grid 2 colunas (texto + skills)
6. `<footer>` — copyright + links

### `about.html`
- Hero text-only (sem foto) com headline grande
- Bio longa
- Skills detalhadas
- Processo de trabalho (pode usar uma linha do tempo simples com bordas)

### `contact.html`
- Minimal: email em destaque (DM Sans 32px), links para LinkedIn/resume
- Sem formulário — link direto para `mailto:`

### Case study pages (`/work/batch-printing.html`, etc.)
- Header do case: título grande + tags + métrica de impacto
- Corpo em grid editorial de uma coluna (máx 640px de largura de texto)
- Imagens full-width dentro do container de 900px
- Seções: Context · Problem · Process · Solution · Outcome

---

## 9. File Structure Recomendada

```
portfolio/
├── index.html
├── about.html
├── contact.html
├── work/
│   ├── batch-printing.html
│   └── expired-tags-research.html
├── css/
│   └── design-system.css     ← todos os tokens e componentes base
└── assets/
    └── images/
```

O arquivo `design-system.css` deve conter todas as variáveis CSS do item 3 deste briefing, as classes de tipografia do item 2, e os componentes do item 6. Todas as páginas importam apenas esse arquivo.

---

## 10. Quality Checklist

Antes de qualquer entrega, verificar:

- [ ] Apenas DM Sans e DM Mono — nenhuma outra fonte na página
- [ ] `--accent` (`#2563eb`) aparece em no máximo 3 lugares
- [ ] Todos os labels/tags em `uppercase` com `letter-spacing` ≥ 0.06em
- [ ] Border-radius = 0 em todos os elementos (botões, tags, cards) — sem arredondamento
- [ ] Padding lateral de 48px consistente em todas as seções
- [ ] Nenhum `box-shadow` visível (bordas fazem o trabalho)
- [ ] Hover de card usa apenas `background: var(--surface-2)` — não muda borda nem sombra
- [ ] `font-weight: 700` apenas no hero H1
- [ ] Imagens de projeto em `aspect-ratio: 16/9` com `object-fit: cover`
- [ ] Rodapé de card de projeto sempre tem: tags + título + descrição + métrica + arrow
