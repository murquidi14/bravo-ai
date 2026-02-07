# Command Center Template Audit

**Created:** 2026-02-05
**Purpose:** Categorize all files for export/template creation

---

## Summary

| Category | Files | Action |
|----------|-------|--------|
| ✅ **Universal** | 15 | Reuse as-is |
| 🔧 **Parameterize** | 18 | Replace variables |
| 🏢 **Client-Specific** | 12 | Rebuild per client |
| 📁 **Structure Only** | 10 | Empty templates |

---

## ✅ UNIVERSAL (Reuse As-Is)

These are industry-standard and don't need changes:

### Industry Data
| File | Description |
|------|-------------|
| `aisc-database.md` | AISC 16th Ed shapes - universal |
| `bolt-grades-database.md` | ASTM bolt standards - universal |
| `aisc-w-shapes.js` | W-shape properties - universal |
| `aisc-weights.js` | Weight lookup - universal |

### Workflow Logic (Generic)
| File | Description |
|------|-------------|
| `po-workflow.md` | PO lifecycle logic (remove Telegram IDs) |
| `material-traceability-rules.md` | Heat# tracking logic |
| `material-receiving-workflow.md` | Receiving process |
| `inventory-lifecycle.md` | ON ORDER → IN STOCK → ALLOCATED |
| `shipping-eligibility-strict.md` | Route completion rules |
| `load-eligibility-rules.md` | What can ship when |
| `fabrication-routes.md` | W&P, WNP, NWP, C/O routes |
| `cut-list-rules.md` | Combining → cut list rules |
| `material-combining-workflow.md` | Inventory → piece marks |
| `data-integrity-rules.md` | No fake data rule |
| `pfxt-import-workflow.md` | PFXT processing logic |

---

## 🔧 PARAMETERIZE (Replace Variables)

These need `{{VARIABLE}}` placeholders:

### Company Identity
| File | Variables to Replace |
|------|---------------------|
| `SOUL.md` | `{{COMPANY_NAME}}`, `{{COMPANY_TAGLINE}}`, `{{AGENT_NAME}}` |
| `IDENTITY.md` | `{{AGENT_NAME}}`, `{{COMPANY_NAME}}` |
| `USER.md` | `{{OWNER_NAME}}`, `{{OWNER_EMAIL}}` |
| `TOOLS.md` | `{{EMAIL}}`, `{{TELEGRAM_GROUPS}}`, `{{PINS}}` |

### Rates & Pricing
| File | Variables to Replace |
|------|---------------------|
| `system-parameters.md` | `{{LABOR_RATES}}`, `{{OVERHEAD_PCT}}`, `{{PROFIT_PCT}}`, `{{PINS}}`, `{{DECK_PRICING}}` |
| `estimating-parameters.md` | `{{LABOR_RATES}}`, `{{TIME_FACTORS}}`, `{{COST_FACTORS}}` |
| `estimating-parameters-locked.md` | Same as above |
| `estimating-markups.md` | `{{OVERHEAD}}`, `{{SGA}}`, `{{PROFIT}}` |
| `estimating-labor-codes.md` | Keep codes, parameterize rates |
| `estimating-system.md` | `{{COST_CODES}}`, `{{CATEGORIES}}` |

### Workflow Config
| File | Variables to Replace |
|------|---------------------|
| `bid-tracking-workflow.md` | `{{OWNER_EMAIL}}`, `{{TELEGRAM_ID}}` |
| `document-control-workflow.md` | `{{AGENT_EMAIL}}`, `{{PROJECT_FOLDER}}` |
| `pm-workflow.md` | `{{FOLDER_STRUCTURE}}` |
| `po-creator-config.md` | `{{DEFAULT_GRADES}}`, `{{SUPPLIERS}}` |
| `billing-access.md` | `{{BILLING_PIN}}` |
| `dashboard-tab-format.md` | `{{BILLING_PIN}}` |
| `job-rules.md` | Keep as-is (generic) |
| `po-page-template.md` | `{{COMPANY_LOGO}}` |

---

## 🏢 CLIENT-SPECIFIC (Rebuild Per Client)

These are Del Bravo-only and need fresh content:

| File | Why Client-Specific |
|------|---------------------|
| `del-bravo-rules-index.md` | Master index - rebuild for each client |
| `contracts.md` | Client's actual contracts |
| `vendors/` | Client's supplier list |
| `MEMORY.md` | Client history (starts empty) |
| `memory/YYYY-MM-DD.md` | Daily logs (starts empty) |
| All job-specific data | Fresh per client |

### Data Folders (Start Empty)
| Folder | Purpose |
|--------|---------|
| `data/jobs/` | Client's job data |
| `data/po-data/` | Client's POs |
| `data/bids/` | Client's bids |
| `data/receipts/` | Client's receipts |
| `integrations/email/` | Client's OAuth config |

---

## 📁 TEMPLATES (HTML/Forms)

These need logo/branding replacement:

| Template | Variables |
|----------|-----------|
| `daily-report-template.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `qc-report-template.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `production-dashboard.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `transmittal-cover-sheet.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `material-receiving-checklist.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `production-control-sheet.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |
| `shipping-calendar.html` | `{{LOGO}}`, `{{COMPANY_NAME}}` |

### Dashboard HTMLs
| File | Variables |
|------|-----------|
| `Bid-Dashboard.html` | `{{LOGO}}`, `{{COMPANY_NAME}}`, `{{PINS}}` |
| `AP-Dashboard.html` | `{{LOGO}}`, `{{COMPANY_NAME}}`, `{{PINS}}` |
| `Receipt-Tracker.html` | `{{LOGO}}`, `{{COMPANY_NAME}}`, `{{PINS}}` |
| `PO-Creator.html` | `{{LOGO}}`, `{{COMPANY_NAME}}`, `{{DEFAULT_RATES}}` |
| `Estimate-Builder.html` | `{{LOGO}}`, `{{COMPANY_NAME}}`, `{{DEFAULT_RATES}}` |

### Scripts (Universal - No Changes)
| Script | Purpose |
|--------|---------|
| `generate_heat_report.py` | Heat number reports |
| `generate_modern_docs.py` | Document generation |
| `generate_po.py` | PO PDF generation |
| `generate_transmittal.py` | Transmittal PDFs |

---

## 🎯 DEPLOYMENT CHECKLIST

### Pre-Deployment (Bravo AI does this)
- [ ] Clone template workspace
- [ ] Run config script with client details
- [ ] Generate branded templates
- [ ] Set up Telegram bot
- [ ] Configure email OAuth
- [ ] Set PINs and security

### Client Provides
- [ ] Company name & logo
- [ ] Owner name & contact info
- [ ] Labor rates (or use defaults)
- [ ] Markup percentages
- [ ] Telegram user IDs
- [ ] Email domain (if using)
- [ ] Preferred PINs

### First Week Customization
- [ ] Import their vendor list
- [ ] Set up job templates
- [ ] Configure any special workflows
- [ ] Train team on system

---

## 📦 TEMPLATE STRUCTURE

```
command-center-template/
├── config/
│   ├── client-config.json      # All client variables
│   └── setup.sh                # Deployment script
├── workspace/
│   ├── AGENTS.md               # Template
│   ├── SOUL.md                 # Template with {{vars}}
│   ├── USER.md                 # Template with {{vars}}
│   ├── TOOLS.md                # Template with {{vars}}
│   ├── HEARTBEAT.md            # Empty
│   ├── MEMORY.md               # Empty (fresh start)
│   └── memory/                 # Empty
├── rules/                      # All workflow rules
│   ├── universal/              # Copy as-is
│   └── parameterized/          # Replace {{vars}}
├── data/
│   ├── steel/                  # AISC database (universal)
│   └── templates/              # Empty job structure
├── dashboards/                 # All HTML dashboards
├── scripts/                    # Python/JS scripts
└── integrations/
    └── email/                  # OAuth template
```

---

## NEXT STEPS

1. **Create `client-config.json` schema** - All variables in one place
2. **Build `setup.sh` deployment script** - Automated variable replacement
3. **Extract universal rules** - Copy to template/rules/universal/
4. **Templatize parameterized files** - Add {{VARIABLE}} placeholders
5. **Create fresh workspace structure** - Empty data folders
6. **Test deployment** - Clone, configure, verify

---

*This audit identifies 45+ files that make up the Command Center.*
*Approximately 60% can be reused with minimal changes.*
