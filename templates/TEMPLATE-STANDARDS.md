# Bravo AI - Template Standards

**Established:** 2026-02-06
**Based on:** V3 Bold Proposal Template
**Status:** 🔒 LOCKED - Use for all future templates

---

## Brand Colors

| Name | Hex | Usage |
|------|-----|-------|
| Navy (Primary) | `#172554` | Headers, primary text, gradients |
| Dark Navy | `#0f172a` | Cover backgrounds, deep sections |
| Red (Accent) | `#7f1d1d` | Accents, section numbers, highlights |
| Bright Red | `#f87171` | Glows, icons, AI text |
| Light Gray | `#f8fafc` | Backgrounds, footer |
| Text Gray | `#64748b` | Secondary text, labels |
| Border Gray | `#e2e8f0` | Borders, dividers |
| Success Green | `#22c55e` | Checkmarks, positive indicators |

---

## Typography

| Element | Font | Weight | Size |
|---------|------|--------|------|
| Headings | Space Grotesk | 700 | 28-56px |
| Body | Space Grotesk | 400 | 15-16px |
| Labels | Space Grotesk | 500 | 11-12px (uppercase, letter-spacing: 1-2px) |
| Section Numbers | Space Grotesk | 700 | 48px |

**Font Import:**
```html
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
```

---

## Logo Usage

### With I-Beam Icon (Preferred)
- Cover pages: White/red gradient beam on dark background
- Footers: Navy/red beam on light background
- Always include the I-beam icon for brand recognition

### SVG Code (Cover - Light on Dark):
```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 50" width="40" height="42">
  <rect x="0" y="0" width="48" height="10" rx="2" fill="#ffffff"/>
  <rect x="0" y="40" width="48" height="10" rx="2" fill="#f87171"/>
  <defs>
    <linearGradient id="beamGrad" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" style="stop-color:#ffffff"/>
      <stop offset="100%" style="stop-color:#f87171"/>
    </linearGradient>
  </defs>
  <rect x="19" y="10" width="10" height="30" fill="url(#beamGrad)"/>
  <circle cx="24" cy="25" r="5" fill="#0f172a"/>
</svg>
```

### SVG Code (Footer - Dark on Light):
```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 50" width="32" height="34">
  <rect x="0" y="0" width="48" height="10" rx="2" fill="#172554"/>
  <rect x="0" y="40" width="48" height="10" rx="2" fill="#7f1d1d"/>
  <defs>
    <linearGradient id="beamGrad" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" style="stop-color:#172554"/>
      <stop offset="100%" style="stop-color:#7f1d1d"/>
    </linearGradient>
  </defs>
  <rect x="19" y="10" width="10" height="30" fill="url(#beamGrad)"/>
  <circle cx="24" cy="25" r="5" fill="#64748b"/>
</svg>
```

---

## Page Structure

### Cover Page
- Full-page gradient background: `linear-gradient(135deg, #172554 0%, #0f172a 50%, #7f1d1d 100%)`
- Logo top-left, meta (proposal #, date) top-right
- Large title centered with highlight color on key word
- Client name at bottom with border-top separator
- Footer: website + tagline

### Content Pages
- White background
- 50px padding
- Max-width: 900px centered

### Section Headers
- Section number (48px, red)
- Section title (28px, navy)
- Gradient line extending right

---

## Components

### Stat Cards (Dark)
```css
.stat-card {
  background: linear-gradient(135deg, #172554, #1e3a5f);
  color: white;
  padding: 30px;
  border-radius: 16px;
}
```

### Pricing Cards
```css
.pricing-card {
  border: 2px solid #e2e8f0;
  border-radius: 16px;
  padding: 32px;
  text-align: center;
}
.pricing-card.featured {
  border-color: #7f1d1d;
  transform: scale(1.05);
  box-shadow: 0 20px 40px rgba(127, 29, 29, 0.15);
}
```

### Tables
```css
th {
  background: #172554;
  color: white;
  padding: 16px;
  text-transform: uppercase;
  letter-spacing: 1px;
}
th:first-child { border-radius: 8px 0 0 8px; }
th:last-child { border-radius: 0 8px 8px 0; }
```

### Guarantee Box
```css
.guarantee-box {
  background: #7f1d1d;
  color: white;
  padding: 40px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  gap: 30px;
}
```

### Checklist
- Green circle with checkmark: `#22c55e` background
- Gray arrow for client items: `#f1f5f9` background

---

## Page Breaks (CRITICAL)

```css
/* Cover always on its own page */
.cover {
  page-break-after: always;
}

/* Section headers stay with content */
.section-header {
  page-break-after: avoid;
  break-after: avoid;
}

/* Cards and tables don't split */
.pricing-row, .card-row, .checklist, table {
  page-break-inside: avoid;
  break-inside: avoid;
}

/* Guarantee box stays together */
.guarantee-box {
  page-break-inside: avoid;
  break-inside: avoid;
}

/* Signatures on their own page */
.signature-section {
  page-break-before: always;
  break-before: always;
}

/* Individual cards don't split */
.pricing-card, .stat-card {
  page-break-inside: avoid;
  break-inside: avoid;
}
```

---

## Footer (All Documents)

```html
<div class="footer">
  [I-BEAM ICON SVG]
  <span class="bravo">BRAVO</span><span class="ai">AI</span>
  <p>13351 Montana Ave • El Paso, Texas 79938</p>
  <p>mario@bravoai.co • bravoai.co</p>
  <p><em>Built by fabricators. For fabricators.</em></p>
</div>
```

---

## File Naming

| Document | Filename |
|----------|----------|
| Proposal | `BravoAI-Proposal-[CLIENT]-[DATE].pdf` |
| SOW | `BravoAI-SOW-[CLIENT]-[NUMBER].pdf` |
| MSA | `BravoAI-MSA-[CLIENT].pdf` |
| Invoice | `BravoAI-Invoice-[NUMBER].pdf` |

---

## Reference Template

**🔒 LOCKED: Official Proposal Template**
Master HTML: `/projects/db-consulting/templates/proposal-template.html`
**Locked:** February 6, 2026

### Cover Page Design (Style "L + I Hybrid")
- **Header bar:** Navy gradient (#172554 → #1e3a5f), logo + tagline centered left, "Proposal" badge right
- **Body:** Centered — red accent bar, title, subtitle, client name, date
- **Footer bar:** Navy gradient, logo left, contact info right
- **Format:** Letter (8.5" x 11") Portrait

### Contact Info (Footer)
- Phone: (915) 525-0499
- Email: mario@bravoai.co
- Web: bravoai.co

---

*These standards apply to all Bravo AI client-facing documents.*
