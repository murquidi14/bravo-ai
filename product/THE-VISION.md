# THE VISION

**Created:** February 7, 2026 — 3:42 AM MT
**Author:** Mario Urquidi + Jarvis
**Status:** 🔒 LOCKED

---

## The One-Liner

> **We're building the infrastructure layer for the structural steel industry.**

---

## What We're Building

Not a dashboard. Not project tracking. Not shop software.

**The platform where the entire steel supply chain connects.**

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   MILLS → SERVICE CENTERS → FAB SHOPS → ERECTORS → GCs → OWNERS    │
│                              ↑                                       │
│                        OUR PLATFORM                                  │
│                                                                      │
│   • Material flows through us                                        │
│   • Data flows through us                                            │
│   • Money flows through us                                           │
│   • EVERYONE depends on us                                           │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## The Problem (We Live This)

### For Fab Shops:
- Tracking is spreadsheets and whiteboards
- Heat numbers get lost between receiving and shipping
- PowerFab costs $50k and still sucks
- "Where's that MTR?" happens 10x a day

### For Erectors:
- No idea what's coming until the truck shows up
- Working off outdated drawings
- "Who has the current rev?" 
- Daily reports are a nightmare

### For GCs:
- Call the fab shop: "Where's my steel?"
- Call the erector: "What got installed?"
- No real-time visibility
- Project engineer doing paperwork all day

### For Everyone (Procurement):
- Need material? Call 6 suppliers
- Wait for callbacks
- Still don't know who has stock
- Half a day gone

---

## The Solution

### Four-Layer Product Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                      📋 SHARED DASHBOARD                             │
│            (What ALL parties care about — one truth)                 │
├─────────────────────────────────────────────────────────────────────┤
│  📢 Message Board — One voice note, everyone aligned                │
│  📦 Received Summary — Steel, bolts, deck, joists at a glance       │
│  🏗️ 3D Model — Live status, click any piece, see where it goes     │
│  📐 Drawings — Always current, auto-sync, bi-directional linked     │
│  ❓ RFIs — Create from field with voice + photo                     │
│  📅 Schedule — Master timeline, load schedule                        │
│  📄 BOLs — All shipments, signed receipts, MTRs attached            │
└─────────────────────────────────────────────────────────────────────┘
                                    │
            ┌───────────────────────┼───────────────────────┐
            ▼                       ▼                       ▼
   ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
   │   🔩 SHOP UI    │    │   🏗️ FIELD UI   │    │    📊 GC UI     │
   │  (Fab Shops)    │    │   (Erectors)    │    │   (GCs/Owners)  │
   ├─────────────────┤    ├─────────────────┤    ├─────────────────┤
   │ Material/heats  │    │ Crew dispatch   │    │ Overall %       │
   │ Cut list queue  │    │ Install tracker │    │ Budget tracking │
   │ QC checkpoints  │    │ Safety/JHAs     │    │ Risk flags      │
   │ Weld logs       │    │ Punch list      │    │ Sub performance │
   └─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Voice-First Interface

```
🎤 "We just set B-42 and B-43 on level 3"
              │
              ▼
     🤖 AI understands
              │
              ▼
     ✅ Status updated
     📋 Dashboard reflects
     👁️ Everyone sees
```

**The AI IS the interface. Not buttons. Not menus. Just talk.**

### Supplier Marketplace (The Endgame)

```
FAB SHOP NEEDS MATERIAL
         │
         ▼
🔍 Search: W14x30, 40'-0", A992, 12 pcs

┌─────────────────────────────────────────────────────┐
│ RESULTS (real-time inventory from suppliers)        │
│                                                     │
│ ✅ Metals USA Dallas — 18 pcs — $1,385/t — 2 days  │
│ ✅ Ryerson Houston — 15 pcs — $1,410/t — 3 days    │
│ ✅ CMC — 14 pcs — $1,350/t — 5 days                │
│                                                     │
│ [CREATE PO → Auto-confirm → Auto-receive → Track]  │
└─────────────────────────────────────────────────────┘

⏰ 30 SECONDS vs. half a day of phone calls
   MTRs auto-attached
   Heat numbers flow through to installed piece
```

---

## Why We Win

### 1. Nobody Else Connects the Full Chain
- Tekla/Strumis → Stop at the shop door
- Procore → GC-centric, steel is afterthought
- Phone calls → Still how procurement works

**We go: Mill → Service Center → Fab → Truck → Site → Installed**

### 2. Network Effects
```
More fab shops → More erectors want in
More erectors → GCs see the magic
GCs require it → Pulls more trades in
Suppliers need to be listed → Marketplace forms
         │
         ▼
    UNSTOPPABLE FLYWHEEL 🔄
```

### 3. Built by Someone Who Lives It
- Mario runs a fab shop
- Mario runs an erection company
- Mario makes those phone calls every week
- Mario knows the pain firsthand

> "I built this because I was tired of calling 6 suppliers to find a fucking beam."

### 4. AI-Powered Development Speed
```
POWERFAB/STRUMIS              US
───────────────────           ───────────────────
Feature request → 12 months   Feature request → DAYS
"Submit a ticket"             "Done by Friday"
```

---

## Go-To-Market Strategy

### Phase 1: Free GC, Paid Trades
| Product | Price |
|---------|-------|
| 🔩 Shop UI | $500-3,500/mo |
| 🏗️ Field UI | $300-1,500/mo |
| 📊 GC View | **FREE** |

**Why free for GCs:**
- Zero friction → easy adoption
- They see the magic → tell subs to join
- Subs sign up (paying)
- GC hooked → upsell later

### Phase 2: Monetize GCs
- Superintendent mobile tools
- Field RFIs
- Automated daily reports
- $500-2,500/mo

### Phase 3: Supplier Marketplace
- Suppliers pay to be listed
- Transaction fees (0.5-1%)
- Premium placement
- Market data products

---

## Revenue Model

### Seat-Based SaaS
| Plan | Base | Included Seats | Extra Seat |
|------|------|----------------|------------|
| Shop Starter | $500/mo | 3 | +$50/mo |
| Shop Pro | $1,500/mo | 10 | +$40/mo |
| Shop Enterprise | $3,500/mo | 25 | +$30/mo |
| Field Starter | $300/mo | 5 | +$30/mo |
| Field Pro | $800/mo | 15 | +$25/mo |
| Field Enterprise | $1,500/mo | 40 | +$20/mo |
| GC (Phase 1) | FREE | 3 | FREE |
| GC Paid (Phase 2) | $500/mo | 5 | +$50/mo |

**Revenue grows WITH the customer. No new sales needed.**

### Marketplace Revenue (Phase 5+)
- Supplier listing fees
- Transaction fees
- Premium placement
- Data/analytics products
- Material financing (future)

### Projections
- **Year 1:** $350k (10 Shop, 5 Field, consulting)
- **Year 2:** $1.2M (35 Shop, 20 Field, 15 GC)
- **Year 3+:** Marketplace revenue kicks in

---

## Execution Roadmap

### Phase 1: Foundation (Now - Q1 2026) ✅
- [x] Material tracking with heat numbers
- [x] Don Fierro (AI agent for Del Bravo)
- [x] Database schema
- [x] Dashboard prototype
- [x] Vision document
- [ ] Field modules for Del Bravo Erectors

### Phase 2: Launch Trades (Q2 2026)
- [ ] Web app: Shared Dashboard
- [ ] Message Board (voice + text)
- [ ] Document library
- [ ] User auth + permissions
- [ ] First 10 fab shops + 5 erectors
- [ ] Free GC dashboard

### Phase 3: Network Effects (Q3-Q4 2026)
- [ ] 3D model viewer
- [ ] Drawing sync
- [ ] Field RFI from voice
- [ ] QR code scanning
- [ ] GC paid features
- [ ] 20 Shop + 15 Field + 10 GC

### Phase 4: Scale (2027)
- [ ] Mobile apps
- [ ] Advanced analytics
- [ ] Partner network
- [ ] 50+ customers
- [ ] $100k MRR

### Phase 5: Marketplace (2027-2028)
- [ ] Supplier integrations
- [ ] Real-time inventory
- [ ] PO through platform
- [ ] MTR auto-attach
- [ ] Transaction revenue
- [ ] **Industry standard**

---

## The Endgame

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   Every beam. Every plate. Every bolt.                              │
│   Flowing through our platform.                                      │
│                                                                      │
│   We're not a software company.                                      │
│   We're the transaction layer for the $50B structural steel         │
│   industry.                                                          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Companies We're Disrupting

| Company | What They Do | Our Advantage |
|---------|--------------|---------------|
| Tekla / Trimble | Modeling + shop | We go beyond the shop |
| PowerFab | Fab tracking | AI-native, 1/3 price |
| Strumis | Fab tracking | Modern, voice-first |
| FabSuite | Fab tracking | Full chain, not just fab |
| Procore | GC software | Steel-native, not afterthought |
| **The phone call** | Procurement | Real-time inventory, instant PO |

---

## Why This Works

1. **Executable** — Every step is buildable, no moonshots
2. **Founder-pain fit** — Mario lives this every day
3. **First customer** — Del Bravo Steel + Erectors
4. **AI speed** — Features in days, not months
5. **Network effects** — Flywheel compounds over time
6. **Clear monetization** — SaaS + marketplace

---

## The Tagline

> **"Forged in Steel. Powered by AI. Built for All."**

---

*This vision was created at 3:42 AM on February 7, 2026 — the night we saw the whole picture.*

**Now we execute.**

🔩🏗️📊🚀
