---
name: lorkindoc
description: >-
  Lorhard's in-house design system for formal, long-form HTML documents — contracts, consulting reports, research, sector notes, equity research, and client deliverables that must print or export to PDF cleanly.
  Trigger on: "draft an MSA", "SOW for <client>", "consulting report", "industry report", "white paper", "PDP research", "put this in Lorhard style", "Lorkindoc template", or requests for a printable document in serif body text with Letter / 1in margins.
  Opinionated single-template by design — one shared typographic system (serif body, #be9c72 gold rule, 580px measure, uppercase h2, italic h3) adapted to three scenarios only: contracts, named-client reports, and general reports. Not a general-purpose HTML generator.
  Do NOT use for: marketing pages, campaign microsites, social graphics, short landing pages, product UI, slide decks, email HTML, interactive dashboards, or dynamic web apps — Lorkindoc assumes static, paginated, text-heavy output and will decline visual-impact-first asks.
disable-model-invocation: false
argument-hint: "[document type + subject, e.g. 'MSA for Acme', 'industry report on vertical AI']"
---

# Lorkindoc — Lorhard's Formal Document Design System

A single-file distillation of the typographic and structural rules behind every long-form document Lorhard publishes — contracts, consulting reports, and sector research — encoded as a reusable HTML/CSS skeleton.

This skill produces **structure and style, not content**. It will not inject business terms, pricing, legal clauses, client data, or analysis. The author supplies those; Lorkindoc guarantees a Lorhard document looks, paginates, and prints like a Lorhard document regardless of who drafted it.

Lorkindoc is **opinionated and narrow**. It encodes one shared design language — serif body, gold rule at #be9c72, 580px measure, uppercase small-caps h2, italic h3, Letter paper with 1in margins — and adapts it to three scenarios (contracts, named-client reports, general reports). It does not offer themes, variants, or visual flexibility beyond those three cases.

## When this skill activates

This skill triggers when a task calls for a **formal, printable long-form document** published under the Lorhard brand. Users often describe the need without naming Lorkindoc directly:

- Drafts a contract — MSA, SOW, NDA, service agreement, procurement agreement
- Produces a consulting report, research report, competitive analysis, or PDP study for a named client
- Writes a sector note, industry research report, security / equity research, or white paper under Lorhard's own name
- Explicitly requests "Lorhard style," "Lorkindoc style," or "our official document format"
- Asks for HTML that must print or export to PDF cleanly (Letter, 1in margins, serif body)

**Works across scenarios:** client-facing legal documents, internal research memos, externally published thought leadership, and any long-form output that must carry Lorhard's visual identity.

**Exclusions:** marketing pages, campaign microsites, social graphics, short landing pages, product UI, or anything that prioritizes visual impact over editorial density — these belong to a separate frontend design system, not Lorkindoc.

Also not for: slide decks, email HTML, interactive dashboards, dynamic web apps — Lorkindoc assumes static, paginated, text-heavy output.

---

## How to use this skill

1. **Identify the scenario.** Contract (A), named-client report (B), or general report (C). If the request is ambiguous, ask once before generating.
2. **Copy the Complete Style Baseline** as the starting `<style>` block. Do not recolor, resize, or rewiden.
3. **Tailor the cover and footer** to match the scenario. The three Scenario sections below enumerate what must appear, what is optional, and what is forbidden.
4. **Paste the standard logo snippet verbatim** for scenarios B and C. Never substitute an `<img>`, remote URL, or redrawn SVG.
5. **Wrap every unfilled field** in `<span class="placeholder">{{…}}</span>` so the author can find and replace them at review time.
6. **Do not supply business content.** Clauses, pricing, analysis, client data, and sensitive information are the author's responsibility. This skill delivers scaffolding only.

---

## Core Design Language

These choices are non-negotiable. Deviating from any of them breaks Lorhard's visual identity across the document family.

### Typography

English text is set in Times New Roman; CJK text falls back through Noto Serif SC → SimSun → Songti SC. All four share a serif classification, which is what keeps mixed-language passages visually coherent. Complete `font-family` stack is in the Complete Style Baseline below.

### Color

| Token | Hex | Role |
|---|---|---|
| Primary text | `#111` | Headings, emphasized body, table headers |
| Secondary text | `#444` | Subtitles, table cells, block quotes |
| Tertiary text | `#888` | Cover labels, footer, TOC sub-items |
| Rules / borders | `#bbb` / `#ccc` / `#ddd` | h2 top border, table dividers, TOC dotted leaders, `<hr>` |
| Brand gold | `#be9c72` | The 60px rule under the cover title. **The only chromatic element.** |
| Highlight background | `#fffbe6` (with `#e6d9a0` border) | Placeholders, key figures, pull quotes |

**Principle:** the document is grayscale with one restrained accent. Any color beyond `#be9c72` and the highlight pair is a bug.

### Type scale and rhythm

Base: `html { font-size: 12pt }`, compressing to `11.5pt` when printed. Line-height is `1.55`.

**Heading rhythm (non-negotiable):**
- `cover-title` 28pt 700, `cover-subtitle` 11pt italic
- `h1` 18pt centered; `h2` 12pt uppercase + `letter-spacing: .03em` + top border `.5px #bbb`; `h3` 11pt italic, no border
- Body paragraphs are justified (`text-align: justify`)

### Measure

- **Cover:** full viewport (`min-height: 100vh`), `padding: 100px 72px`, centered.
- **Body:** `max-width: 580px`, horizontally centered. This is Lorkindoc's signature measure. **Never widen it.**

### Print contract

All Lorkindoc documents default to US Letter with 1in margins (`@page { size: letter; margin: 1in }`). Under print, the font shrinks to 11.5pt, h2/h3 avoid widowing, paragraphs enforce `orphans: 3; widows: 3`, and tables never break across pages. Every document must export to PDF or print cleanly — if a document looks right on screen but breaks when printed, it is wrong.

---

## Document Shell

Every Lorkindoc document is a linear sequence of up to five sections. Which sections appear depends on the scenario (see below).

```
1. <Cover>          — Full-page title block. Always present.
2. <TOC>            — Table of contents. Required for contracts; strongly recommended
                      for reports; may be omitted only for short reports (< 4 h2 sections).
3. <DocBody>        — The body: h1/h2/h3, paragraphs, tables, block quotes. Uses .doc-body.
4. <SignaturePage>  — Countersignature block. Contracts only.
5. <Footer>         — Lorhard-branded footer. Reports only (never for contracts).
```

A contract ends at the signature page. A report ends at the branded footer. These terminations are mutually exclusive — do not mix.

---

## Table of Contents

Lorkindoc TOCs adopt a book-style layout: an uppercase small-caps title, dotted leaders connecting entry to edge, manual numbering, and indented sub-entries. The visual language aligns with the document's serif body and Letter-page proportions.

**Requirement by scenario:**

| Scenario | TOC |
|---|---|
| A — Contract | Required — every contract must have a TOC between cover and body. |
| B — Named-client report | Strongly recommended; required unless the report has fewer than 4 `h2` sections. |
| C — General report | Strongly recommended; required unless the report has fewer than 4 `h2` sections. |

**Structural rules:**

- Container is `<div class="toc">` with page-break after (the TOC always occupies its own page).
- Title is `<p class="toc-title">TABLE OF CONTENTS</p>` — uppercase with wide letter-spacing. The title follows the document's primary language; use the canonical translation in whichever language the document is written in. Brand-identity tags on the cover (`Confidential`, `Execution Version`, `Internal Reference`) follow the same rule.
- Entries live in a `<ul>`, not `<ol>`. Numbering is **written into the text** (`1. Framework, SOWs, and Order of Precedence`) rather than generated by the list element. This keeps numbering controllable across jumps, appendices, and renumbered sections.
- Every entry links to a section anchor (`<a href="#sec-1">…</a>`). Anchors follow the `sec-<N>` convention for contracts; reports may use slug anchors (`#methodology`, `#case-studies`).
- Sub-entries use `<li class="toc-sub">`. Indented 18px, smaller type, no dotted leader — they should read as a quiet continuation of their parent.

**Standard markup:**

```html
<div class="toc">
  <p class="toc-title">TABLE OF CONTENTS</p>
  <ul>
    <li><a href="#sec-1">1. Framework, SOWs, and Order of Precedence</a></li>
    <li><a href="#sec-2">2. Services</a></li>
    <li><a href="#sec-3">3. Scope of Services and Phase Objectives</a></li>
    <li class="toc-sub"><a href="#sub-3-1">3.1 Phase I — Launch and Conversion Foundation</a></li>
    <li class="toc-sub"><a href="#sub-3-2">3.2 Phase II — Content Operating System (Reference Only)</a></li>
    <li><a href="#sec-4">4. Acceptance Procedure</a></li>
  </ul>
</div>
```

CSS (`.toc`, `.toc-title`, `.toc li`, `.toc .toc-sub`) lives in the Complete Style Baseline below; do not duplicate it here.

---

## The Three Scenarios

**Shared invariants across all scenarios:** typography, color, type scale, measure, heading rhythm, gold rule, print contract.
**Permitted differences:** cover wording, signature page, footer presence, UTM parameters.

> **Note on language.** All English strings in the examples below (`Confidential`, `Execution Version`, `Internal Reference`, `Industry Report`, `Published by`, `Prepared by Lorhard for …`, binding-language declarations, etc.) are illustrative. Per the **Language policy** in Generation Workflow, translate them to the document's primary language. The only strings that stay canonical regardless of language are proper nouns (`LORHARD INC`) and widely understood abbreviations (MSA, SOW, NDA, …).

### Scenario A — Contract

For MSAs, SOWs, NDAs, service agreements, procurement agreements, and any mutual legal instrument.

**Cover must include:**
- Top-right confidentiality tag: `<div class="cover-conf">Confidential</div>`
- Label above the title: `Execution Version` (or `Execution Version — Phase I` for phased documents)
- Main title — e.g. `Master Services Agreement`, `Statement of Work`
- **Subtitle (optional, italic):** Subordinate or phased documents may include a subtitle naming the parent agreement, e.g. `Under the Master Services Agreement dated April 1, 2026`
- **Parties block** (required):

  ```html
  <div class="cover-parties">
    <div class="cover-party">
      <div class="cover-party-role">Customer</div>
      <div class="cover-party-name">{{Counterparty legal name}}</div>
    </div>
    <div class="cover-and">and</div>
    <div class="cover-party">
      <div class="cover-party-role">Provider</div>
      <div class="cover-party-name">LORHARD INC</div>
    </div>
  </div>
  ```

- Effective date

**Table of contents:** required. Contract entries link to `#sec-<N>` anchors. See **Table of Contents** for markup and requirement rules.

**Body:** lead with a single-line `<blockquote>` declaring which language version is legally binding — phrase it naturally in the document's primary language (e.g. for an English contract: `This English-language version is the binding contract document.`). Then an uppercase `<h1>` title, followed by numbered h2 sections (`1. …`, `2. …`). Clauses are numbered with `<span class="clause-num">1.1</span>` in bold. Sub-lists use Roman numerals `(i) / (ii) / (iii)`.

**Signature page (required):** on its own page, opening with `IN WITNESS WHEREOF …`, followed by two signature blocks — Customer and Provider — each with By / Name / Title / Date fields.

**Forbidden in contracts:** the Lorhard logo on the cover, GitHub icon, `© Lorhard`, Privacy link, UTM parameters, or any marketing-style footer. Contracts terminate at the signature page.

### Scenario B — Named-client report

For consulting reports, product research, competitive analyses, PDP studies, and any deliverable written for a specific, identified client.

**Cover must include:**
- Confidentiality tag `<div class="cover-conf">Confidential</div>` (or `Internal Reference` depending on distribution)
- Label: `Internal Reference`, `Client Deliverable`, or similar
- Main title — the research topic
- Italic subtitle describing scope
- **Co-authorship block** (Client × Lorhard):

  ```html
  <div class="cover-parties">
    <div class="cover-party">
      <div class="cover-party-name">{{Client name}}</div>
    </div>
    <div class="cover-and">&times;</div>
    <div class="cover-party">
      <div class="cover-party-name">Lorhard</div>
    </div>
  </div>
  ```

  Do **not** use the `Customer` / `Provider` role labels here — those are reserved for contracts.

- Date
- Meta block — entry count, document type, version

**Logo:** required. Paste the Standard Inline Snippet from **Logo** verbatim, directly above `cover-label`.

**Table of contents:** strongly recommended for reports with four or more h2 sections; see **Table of Contents**.

**Footer (required, matches the lorhard.com site footer):**

```html
<div class="doc-footer">
  <div class="footer-note">Prepared by Lorhard for {{Client}} · Internal reference only</div>
  <div class="site-footer">
    <a href="https://github.com/Lorhard" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
    </a>
    <span class="copy">&copy; 2026 Lorhard</span>
    <a href="https://lorhard.com/privacy">Privacy</a>
  </div>
</div>
```

### Scenario C — General report

For sector notes, industry research, equity / security research, white papers — anything published under Lorhard's own name, not on behalf of an external client.

**Cover must include:**
- Confidentiality / distribution tag appropriate to audience — `Public`, `Internal`, or `Confidential`
- Label: `Industry Report`, `Sector Note`, `White Paper`, etc.
- Main title
- Italic subtitle
- **Byline block — Lorhard only**, no `×` pairing:

  ```html
  <div class="cover-parties">
    <div class="cover-party">
      <div class="cover-party-role">Published by</div>
      <div class="cover-party-name">Lorhard</div>
    </div>
  </div>
  ```

- Date
- Meta block — analyst, coverage scope, version

**Logo / Table of contents:** same rules as Scenario B.

**Footer (required, identical structure to Scenario B):** GitHub icon + `© 2026 Lorhard` + Privacy link. Replace the `footer-note` with `Published by Lorhard · For informational purposes only` or an equivalent disclaimer appropriate to the report type.

---

## Logo

| Scenario | Logo | Placement |
|---|---|---|
| A — Contract | ❌ Omitted | — |
| B — Named-client report | ✅ Required | Above `cover-label`, centered |
| C — General report | ✅ Required | Above `cover-label`, centered |

The logo must be **inlined as SVG** inside every Lorkindoc document. The Lorkindoc skill ships to an independent public repo (lorkinsey), so it cannot depend on any main-repo file path; and formal documents must remain viewable offline, printable, and convertible to PDF without fetching remote assets. The Standard Inline Snippet below is the single source of truth; when the logo changes visually, update it here first and re-sync all downstream documents. All hard rules are consolidated in **Guardrails**.

**Standard Inline Snippet (single source of truth — copy verbatim):**

```html
<a href="https://lorhard.com/" target="_blank" rel="noopener noreferrer" class="cover-logo-link" aria-label="Lorhard">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024" class="cover-logo" role="img" aria-label="Lorhard">
    <rect width="1024" height="1024" rx="122.88" ry="122.88" fill="#FF6602"/>
    <path d="M 399.9 277.9 L 401 277.875 L 402.2 277.861 L 403.4 277.861 L 404.5 277.873 L 405.7 277.9 L 406.8 277.938 L 407.9 277.988 L 409 278.053 L 410.1 278.132 L 411.1 278.218 L 412.1 278.319 L 413.1 278.435 L 414.1 278.568 L 414.975 278.7 L 415.8 278.838 L 416.7 279.006 L 417.6 279.193 L 418.4 279.377 L 419.2 279.578 L 420 279.798 L 420.8 280.039 L 421.5 280.269 L 422.2 280.517 L 422.9 280.784 L 423.6 281.073 L 424.3 281.385 L 424.9 281.672 L 425.539 282 L 426.2 282.364 L 426.769 282.7 L 427.3 283.034 L 427.9 283.436 L 428.5 283.868 L 429.06 284.3 L 429.6 284.746 L 430.1 285.186 L 430.6 285.655 L 431.045 286.1 L 431.515 286.6 L 431.956 287.1 L 432.37 287.6 L 432.8 288.153 L 433.2 288.704 L 433.605 289.3 L 433.986 289.9 L 434.342 290.5 L 434.7 291.149 L 435.035 291.8 L 435.323 292.4 L 435.635 293.1 L 435.925 293.8 L 436.2 294.518 L 436.442 295.2 L 436.704 296 L 436.943 296.8 L 437.163 297.6 L 437.363 298.4 L 437.568 299.3 L 437.733 300.1 L 437.902 301 L 438.054 301.9 L 438.19 302.8 L 438.324 303.8 L 438.443 304.8 L 438.538 305.7 L 438.631 306.7 L 438.713 307.7 L 438.791 308.8 L 438.914 311 L 439.014 313.5 L 439.086 316.2 L 439.137 319.3 L 439.17 323 L 439.189 327.6 L 439.2 344.2 L 439.201 624.2 L 439.218 635.9 L 439.239 639.6 L 439.273 642.7 L 439.326 645.6 L 439.397 648.1 L 439.487 650.3 L 439.605 652.4 L 439.746 654.3 L 439.916 656.1 L 440.018 657 L 440.118 657.8 L 440.229 658.6 L 440.351 659.4 L 440.486 660.2 L 440.614 660.9 L 440.774 661.7 L 440.927 662.4 L 441.093 663.1 L 441.272 663.8 L 441.465 664.5 L 441.674 665.2 L 441.9 665.899 L 442.108 666.5 L 442.33 667.1 L 442.568 667.7 L 442.821 668.3 L 443.091 668.9 L 443.38 669.5 L 443.636 670 L 444.075 670.8 L 444.494 671.5 L 444.947 672.2 L 445.439 672.9 L 445.973 673.6 L 446.469 674.2 L 447.003 674.8 L 447.581 675.4 L 448.2 675.994 L 448.77 676.5 L 449.4 677.019 L 450.031 677.5 L 450.7 677.972 L 451.4 678.429 L 452.1 678.85 L 452.9 679.293 L 453.7 679.698 L 454.5 680.069 L 455.3 680.409 L 456.1 680.721 L 456.9 681.006 L 457.805 681.3 L 458.7 681.563 L 459.7 681.828 L 460.7 682.065 L 461.7 682.276 L 462.7 682.464 L 463.8 682.647 L 464.9 682.808 L 466.1 682.959 L 467.3 683.09 L 468.6 683.21 L 470.2 683.332 L 471.9 683.435 L 473.8 683.524 L 475.8 683.594 L 478 683.649 L 480.4 683.69 L 483.2 683.721 L 486.5 683.741 L 491.7 683.755 L 499.9 683.76 L 603.3 683.765 L 608.6 683.775 L 612.5 683.793 L 615.8 683.824 L 618.6 683.868 L 620.6 683.916 L 622.5 683.978 L 624.3 684.056 L 625.9 684.144 L 627.4 684.247 L 628.8 684.365 L 630.2 684.506 L 631.5 684.661 L 632.8 684.844 L 634 685.04 L 635.2 685.266 L 636.3 685.502 L 637.4 685.77 L 638.4 686.044 L 639.4 686.35 L 640.4 686.692 L 641.4 687.073 L 642.3 687.454 L 643.2 687.874 L 644 688.284 L 644.8 688.732 L 645.6 689.222 L 646 689.485 L 646.4 689.76 L 647.1 690.274 L 647.8 690.833 L 648.115 691.1 L 648.5 691.442 L 648.883 691.8 L 649.19 692.1 L 649.768 692.7 L 650.1 693.067 L 650.388 693.4 L 650.956 694.1 L 651.5 694.832 L 652.023 695.6 L 652.519 696.4 L 652.973 697.2 L 653.4 698.027 L 653.81 698.9 L 654.2 699.82 L 654.573 700.8 L 654.9 701.758 L 655.2 702.743 L 655.485 703.8 L 655.722 704.8 L 655.949 705.9 L 656.144 707 L 656.31 708.1 L 656.459 709.3 L 656.577 710.5 L 656.673 711.8 L 656.736 713.1 L 656.769 714.4 L 656.769 715.8 L 656.738 717.1 L 656.676 718.4 L 656.581 719.7 L 656.453 721 L 656.303 722.2 L 656.119 723.4 L 655.9 724.6 L 655.665 725.7 L 655.394 726.8 L 655.084 727.9 L 654.765 728.9 L 654.407 729.9 L 654.212 730.4 L 654.006 730.9 L 653.603 731.8 L 653.4 732.223 L 653.158 732.7 L 652.7 733.54 L 652.43 734 L 652.183 734.4 L 651.924 734.8 L 651.653 735.2 L 651.369 735.6 L 651.1 735.963 L 650.8 736.349 L 650.514 736.7 L 650.2 737.069 L 649.9 737.406 L 649.6 737.73 L 649.24 738.1 L 648.6 738.716 L 648.286 739 L 647.9 739.334 L 647.5 739.663 L 647.1 739.976 L 646.7 740.275 L 646.3 740.56 L 645.9 740.832 L 645.5 741.092 L 645.1 741.34 L 644.659 741.6 L 643.8 742.072 L 643.3 742.327 L 642.7 742.615 L 642.1 742.884 L 641.589 743.1 L 641 743.334 L 640.4 743.558 L 639.8 743.768 L 639.1 743.995 L 638.5 744.177 L 637.8 744.374 L 637.2 744.531 L 636.5 744.702 L 635.8 744.859 L 635.1 745.004 L 634.4 745.138 L 633.6 745.279 L 632.8 745.406 L 632 745.522 L 630.4 745.722 L 628.7 745.894 L 626.9 746.039 L 624.9 746.163 L 622.8 746.26 L 620.4 746.339 L 617.8 746.397 L 614.7 746.439 L 611.1 746.465 L 606.6 746.48 L 600.2 746.487 L 423.6 746.488 L 415.4 746.476 L 410 746.446 L 407.7 746.421 L 405.7 746.388 L 403.8 746.346 L 402.1 746.294 L 400.3 746.223 L 398.6 746.137 L 397.1 746.04 L 395.6 745.922 L 394.2 745.788 L 392.8 745.628 L 391.5 745.452 L 390.3 745.263 L 389.1 745.045 L 388 744.817 L 386.9 744.558 L 385.8 744.265 L 384.8 743.965 L 383.8 743.631 L 382.8 743.259 L 381.9 742.887 L 381 742.476 L 380.1 742.023 L 379.689 741.8 L 379.2 741.522 L 378.4 741.032 L 378 740.769 L 377.6 740.495 L 377.2 740.207 L 376.8 739.905 L 376.1 739.34 L 375.706 739 L 375.4 738.724 L 374.751 738.1 L 374.4 737.74 L 374.084 737.4 L 373.8 737.081 L 373.475 736.7 L 372.9 735.979 L 372.617 735.6 L 372.332 735.2 L 372.06 734.8 L 371.801 734.4 L 371.553 734 L 371.3 733.573 L 371.034 733.1 L 370.82 732.7 L 370.516 732.1 L 370.231 731.5 L 369.965 730.9 L 369.715 730.3 L 369.481 729.7 L 369.227 729 L 368.992 728.3 L 368.774 727.6 L 368.572 726.9 L 368.385 726.2 L 368.213 725.5 L 368.032 724.7 L 367.866 723.9 L 367.716 723.1 L 367.579 722.3 L 367.454 721.5 L 367.341 720.7 L 367.226 719.8 L 367.124 718.9 L 367.033 718 L 366.952 717.1 L 366.872 716.1 L 366.737 714 L 366.633 711.8 L 366.55 709.3 L 366.489 706.5 L 366.447 703.2 L 366.424 700.1 L 366.41 696.3 L 366.4 683.8 L 366.404 332.2 L 366.412 327.2 L 366.427 323.4 L 366.453 320.2 L 366.489 317.5 L 366.54 315.1 L 366.606 312.9 L 366.69 310.9 L 366.796 309 L 366.872 307.9 L 366.96 306.8 L 367.052 305.8 L 367.157 304.8 L 367.276 303.8 L 367.396 302.9 L 367.531 302 L 367.68 301.1 L 367.847 300.2 L 368.01 299.4 L 368.189 298.6 L 368.386 297.8 L 368.6 297 L 368.804 296.3 L 369.057 295.5 L 369.3 294.794 L 369.557 294.1 L 369.838 293.4 L 370.14 292.7 L 370.419 292.1 L 370.768 291.4 L 371.089 290.8 L 371.433 290.2 L 371.801 289.6 L 372.195 289 L 372.545 288.5 L 372.993 287.9 L 373.4 287.391 L 373.817 286.9 L 374.3 286.367 L 374.8 285.852 L 375.268 285.4 L 375.8 284.918 L 376.293 284.5 L 376.8 284.096 L 377.329 283.7 L 377.9 283.299 L 378.5 282.906 L 379.1 282.539 L 379.692 282.2 L 380.3 281.875 L 381 281.526 L 381.6 281.248 L 382.3 280.946 L 383 280.667 L 383.7 280.408 L 384.4 280.168 L 385.1 279.947 L 385.8 279.741 L 386.6 279.526 L 387.4 279.329 L 388.2 279.15 L 389 278.987 L 389.9 278.821 L 390.8 278.672 L 391.7 278.54 L 392.6 278.423 L 393.6 278.308 L 394.6 278.209 L 395.6 278.124 L 396.6 278.053 L 397.7 277.988 L 398.8 277.938 Z" fill="#FAFAF6"/>
  </svg>
</a>
```

CSS rules live in the **Complete Style Baseline** below (`.cover-logo-link` and `.cover-logo`). Do not duplicate them elsewhere — a single CSS source prevents dimension drift between documents.

---

## UTM Tracking (recommended, optional)

Every link to `https://lorhard.com/` inside a Lorkindoc document — the logo's outer `<a>`, the Privacy link in the footer, any inline reference — **should** carry UTM parameters so the site's analytics can distinguish traffic originating from our formal documents. UTM parameters are URL tags only; they introduce no new data collection and do not affect the privacy policy.

**Applies to Scenarios B and C only.** Contracts (Scenario A) have no logo or footer links to tag, so UTM is irrelevant.

**Naming convention:**

| Parameter | Value | Meaning |
|---|---|---|
| `utm_source` | `lorkindoc` | Fixed. Marks traffic as originating from a formal Lorhard document. |
| `utm_medium` | `client-report` or `industry-report` | Scenario type. |
| `utm_campaign` | Document slug (kebab-case) | e.g. `yeswelder-pdp`, `q2-ai-sector`. |

**Examples:**

```html
<!-- Scenario B — named-client report -->
<a href="https://lorhard.com/?utm_source=lorkindoc&utm_medium=client-report&utm_campaign=yeswelder-pdp" target="_blank" rel="noopener noreferrer" class="cover-logo-link" aria-label="Lorhard">…</a>

<!-- Scenario C — general report -->
<a href="https://lorhard.com/?utm_source=lorkindoc&utm_medium=industry-report&utm_campaign=q2-ai-sector" target="_blank" rel="noopener noreferrer" class="cover-logo-link" aria-label="Lorhard">…</a>
```

**Do not do:**

- ❌ Tracking pixels (`<img src="…/pixel.gif">`) — they fail under print and PDF export, leaving a broken image icon.
- ❌ Inline `<script>` or remote JavaScript — lost on PDF export, frequently blocked by client firewalls, and would trigger a privacy policy update.
- ❌ Any tracking parameters or scripts inside a contract document.

---

## Placeholders

Every unfilled dynamic field uses `<span class="placeholder">{{…}}</span>`. Wrapping this way makes unresolved fields visually unmistakable at review time. Apply it to `{{company name}}`, `{{amount}}`, `{{date}}`, and any other `{{…}}` token.

The rendered style is a muted yellow background with a bronze border (`#fffbe6` / `#e6d9a0` / `#7a6a1e`). CSS is in the Complete Style Baseline.

---

## Complete Style Baseline

Every Lorkindoc document starts from this `<style>` block. Append signature-related rules for contracts; append footer rules for reports.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;600;700&display=swap');
* { margin: 0; padding: 0; box-sizing: border-box; }
html { font-size: 12pt; }
body { font-family: 'Times New Roman','Noto Serif SC','SimSun','Songti SC',serif;
       color: #111; line-height: 1.55; background: #fff; }

/* Cover */
.cover { min-height: 100vh; display: flex; flex-direction: column;
         justify-content: center; align-items: center; text-align: center;
         padding: 100px 72px; page-break-after: always; position: relative; }
.cover-conf { position: absolute; top: 48px; right: 48px;
              font-size: 9pt; letter-spacing: .2em; text-transform: uppercase; color: #888; }
.cover-label { font-size: 9pt; letter-spacing: .18em; text-transform: uppercase;
               color: #888; margin-bottom: 20px; }
.cover-title { font-size: 28pt; font-weight: 700; color: #111; line-height: 1.2; margin-bottom: 10px; }
.cover-title::after { content: ''; display: block; width: 60px; height: 1.5px;
                      background: #be9c72; margin: 20px auto 0; }
.cover-subtitle { font-size: 11pt; color: #444; margin-bottom: 48px;
                  max-width: 480px; font-style: italic; }
.cover-parties { display: flex; align-items: center; gap: 36px; margin: 36px 0; }
.cover-party { text-align: center; }
.cover-party-role { font-size: 8pt; letter-spacing: .15em; text-transform: uppercase;
                    color: #888; margin-bottom: 4px; }
.cover-party-name { font-size: 13pt; font-weight: 700; color: #111; }
.cover-and { font-size: 12pt; color: #888; font-style: italic; }
.cover-date { font-size: 11pt; color: #444; margin-top: 12px; }
.cover-meta { font-size: 9pt; color: #888; line-height: 1.8; margin-top: 36px; }
.cover-logo-link { display: inline-block; margin-bottom: 20px; text-decoration: none; }
.cover-logo { height: 27px; display: block; }

/* TOC */
.toc { max-width: 580px; margin: 0 auto; padding: 72px 0; page-break-after: always; }
.toc-title { font-size: 11pt; font-weight: 700; letter-spacing: .15em;
             text-transform: uppercase; color: #111;
             margin-bottom: 20px; padding-bottom: 6px; border-bottom: 1px solid #333; }
.toc ul { list-style: none; }
.toc li { font-size: 11pt; line-height: 2; border-bottom: 1px dotted #ccc; }
.toc li a { color: #111; text-decoration: none; }
.toc .toc-sub { padding-left: 18px; font-size: 10.5pt; color: #444; border-bottom: none; }

/* Doc body */
.doc-body { max-width: 580px; margin: 0 auto; padding: 0 0 72px; }
blockquote { font-size: 10pt; color: #444; border-left: 2px solid #ccc;
             padding: 6px 14px; margin: 0 0 20px; font-style: italic; }
h1 { font-size: 18pt; font-weight: 700; color: #111; margin: 0 0 20px; text-align: center; }
h2 { font-size: 12pt; font-weight: 700; color: #111; margin: 28px 0 10px;
     padding-top: 16px; border-top: .5px solid #bbb;
     text-transform: uppercase; letter-spacing: .03em; }
h3 { font-size: 11pt; font-weight: 700; color: #111; margin: 20px 0 8px; font-style: italic; }
p { margin: 0 0 8px; text-align: justify; hyphens: auto; orphans: 3; widows: 3; }

/* Clauses & lists (mainly contracts) */
.clause { margin: 0 0 8px; text-align: justify; }
.clause-num { font-weight: 700; color: #111; margin-right: 2px; }
.list-item { margin: 0 0 3px; padding-left: 24px; text-indent: -24px; }
.list-num { font-weight: 700; display: inline-block; width: 20px;
            text-align: right; margin-right: 4px; }

/* Utility */
.bold-subheader { font-size: 11pt; font-weight: 700; color: #111;
                  margin: 16px 0 6px; font-style: italic; }
.placeholder { background: #fffbe6; padding: 0 3px; border: 1px solid #e6d9a0;
               border-radius: 1px; font-size: 10pt; color: #7a6a1e; }
strong { font-weight: 700; }
hr { border: none; border-top: .5px solid #bbb; margin: 24px 0; }

/* Tables */
table { width: 100%; border-collapse: collapse; margin: 12px 0; font-size: 10.5pt; }
th { font-size: 10pt; font-weight: 700; text-align: left; padding: 6px 8px;
     border-bottom: 1.5px solid #333; color: #111; }
td { padding: 5px 8px; border-bottom: .5px solid #ddd; vertical-align: top; color: #444; }
.right { text-align: right; }

/* Signature (contracts only) */
.signature-page { page-break-before: always; padding-top: 48px; }
.sig-preamble { font-size: 11pt; color: #444; margin-bottom: 48px;
                font-style: italic; text-align: center; }
.sig-blocks { display: flex; flex-direction: column; gap: 56px; }
.sig-role { font-size: 9pt; font-weight: 700; letter-spacing: .12em;
            text-transform: uppercase; color: #888; margin-bottom: 2px; }
.sig-entity { font-size: 12pt; font-weight: 700; color: #111; margin-bottom: 24px; }
.sig-field { display: flex; align-items: baseline; gap: 8px; margin-bottom: 18px; }
.sig-label { font-size: 11pt; color: #111; flex-shrink: 0; width: 48px; }
.sig-line { flex: 1; border-bottom: .5px solid #333; min-height: 20px;
            display: flex; align-items: flex-end; padding: 0 4px 1px; }

/* Footer (reports only — DO NOT include in contracts) */
.doc-footer { margin-top: 40px; padding-top: 16px; border-top: .5px solid #bbb;
              text-align: center; font-size: 9pt; color: #888; page-break-inside: avoid; }
.doc-footer .footer-note { margin-bottom: 16px; }
.site-footer { display: flex; align-items: center; justify-content: center;
               gap: 10px; margin-top: 12px; font-size: 8pt; color: #888;
               font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', system-ui, sans-serif; }
.site-footer a { color: #888; text-decoration: none; opacity: .7; }
.site-footer a:hover { opacity: 1; }
.site-footer svg { display: inline-block; vertical-align: middle; opacity: .6; }
.site-footer .copy { opacity: .7; }

/* Screen — add horizontal padding on screen so the body and footer don't hug the viewport edge on small screens */
@media screen {
  .doc-body { padding: 30px 24px 60px; }
  .doc-footer { max-width: 580px; margin: 40px auto 0; padding: 16px 24px 40px; }
}

/* Print */
@media print {
  html { font-size: 11.5pt; }
  .cover { min-height: auto; padding: 140px 72px; }
  .toc, .doc-body { max-width: none; }
  h2, h3 { page-break-after: avoid; }
  p { orphans: 3; widows: 3; }
  table { page-break-inside: avoid; }
  .signature-page { page-break-before: always; }
  a { color: #111; text-decoration: none; }
  @page { size: letter; margin: 1in; }
}
```

---

## Generation Workflow

1. **Identify the scenario.** A (contract), B (named-client report), or C (general report). If the user has not said, ask once before generating.
2. **Start from the baseline.** Copy the entire `<style>` block from Complete Style Baseline as-is. Do not recolor, resize, rewiden, or substitute fonts.
3. **Trim for the scenario:**
   - Contract → keep signature rules (`.signature-page`, `.sig-*`). **Remove** `.cover-logo-link`, `.cover-logo`, `.doc-footer`, `.site-footer`, and all related HTML.
   - Named-client report / general report → remove `.signature-page` and `.sig-*`. **Keep** `.cover-logo-link`, `.cover-logo`, `.doc-footer`, and `.site-footer`. Logo and footer are required, not optional.
4. **Tailor the cover.** Follow the exact cover fragments defined in Scenarios A / B / C. For B and C, paste the Standard Inline Snippet from the Logo section directly above the `cover-label`.
5. **Insert the TOC.** For contracts: always. For reports: include whenever the document has four or more `h2` sections. Use the markup from the **Table of Contents** section; number entries manually (`1. … / 1.1 … / 2. …`) and anchor each entry to its `h2`.
6. **Wrap placeholders.** Every `{{…}}` field goes inside `<span class="placeholder">…</span>`.
7. **Do not inject business content.** Ship the scaffold. Clauses, pricing, analysis, and client-specific data remain the author's responsibility.
8. **Language policy — match the user's language.**
   - Generate the document in the language the user writes in, or the language of the source material they supply. Do **not** default to English.
   - Translate every illustrative string in this skill — cover labels, confidentiality tags, TOC title, binding-language declarations, footer disclaimers — into that same language.
   - Keep canonical English only for (a) proper nouns (entity names, trademarks, place names) and (b) widely understood technical abbreviations (MSA, SOW, NDA, MOU, SaaS, USD, KPI, ROI, GAAP, IP).
   - Never mix languages in body prose. Choose one primary language per document and stay consistent.

---

## Guardrails

Hard red lines only. Full rules live in their dedicated sections.

- **Contracts end at the signature page.** No logo, no branded footer, no UTM, no tracking pixels or scripts. Ever.
- **Reports (B / C) must carry both** the cover logo (linked to lorhard.com) and the site-style footer. See **Logo** and Scenario B / C for exact markup.
- **`#be9c72` is the only chromatic element.** Never substitute.
- **`.doc-body` never exceeds 580px.** Never widen.
- **Body type is always serif.** `.site-footer` is the sole deliberate exception.
- **Pixels, remote JavaScript, and runtime requests are prohibited** regardless of scenario. UTM parameters on static links are the only tracking allowed, and only in reports.
