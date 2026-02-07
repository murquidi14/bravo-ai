# Bravo AI - Product Vision & Roadmap

*Created: February 6, 2026*
*Updated: February 7, 2026 — Three-tier product architecture*

---

## The Big Picture

**Two-lane business model:**

```
┌─────────────────────────────────────────────────────────────────┐
│                         BRAVO AI                                 │
├────────────────────────────┬────────────────────────────────────┤
│     🔩 VERTICAL PRODUCT    │     🌐 HORIZONTAL SERVICES         │
│  Steel Fab + Erection      │     Any Industry                   │
├────────────────────────────┼────────────────────────────────────┤
│  • Purpose-built software  │  • Custom AI implementations       │
│  • Industry-specific       │  • Consulting & integration        │
│  • Scalable SaaS           │  • Tailored solutions              │
│  • Recurring revenue       │  • Project-based revenue           │
│  • Self-serve possible     │  • High-touch, premium pricing     │
└────────────────────────────┴────────────────────────────────────┘
```

---

## 🔒 THREE-TIER PRODUCT ARCHITECTURE (LOCKED)

*Decision made: February 7, 2026*

**The Core Insight:** Most steel companies are EITHER fabricators OR erectors — rarely both. But GCs and building owners need visibility into BOTH to track their project.

### Product Structure — Four-Layer Model

```
┌─────────────────────────────────────────────────────────────────────┐
│                        [PRODUCT NAME]                                │
│           "Forged in Steel. Powered by AI. Built for All."          │
└─────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────┐
│                      📋 SHARED DASHBOARD                             │
│                  (What ALL parties care about)                       │
├─────────────────────────────────────────────────────────────────────┤
│  📐 Shop Drawings    │  Current rev, pending revisions, markups     │
│  ❓ RFIs             │  Open, pending response, who's ball          │
│  📅 Master Schedule  │  Timeline, milestones, slippage alerts       │
│  🚚 Load Schedule    │  What's shipping when, delivery calendar     │
│  📄 BOLs             │  All shipments, signed receipts, MTRs        │
│  📝 Daily Reports    │  Shop + field combined activity log          │
├─────────────────────────────────────────────────────────────────────┤
│  👁️ VISIBLE TO: Fab Shop + Erector + GC (all parties on the job)   │
└─────────────────────────────────────────────────────────────────────┘
                                    │
            ┌───────────────────────┼───────────────────────┐
            ▼                       ▼                       ▼
   ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
   │   🔩 SHOP UI    │    │   🏗️ FIELD UI   │    │    📊 GC UI     │
   │  (Fab-specific) │    │(Erector-specific)│    │(Owner-specific) │
   ├─────────────────┤    ├─────────────────┤    ├─────────────────┤
   │ Material/heats  │    │ Crew dispatch   │    │ Overall %       │
   │ Cut list queue  │    │ Install tracker │    │ Budget vs actual│
   │ Fit-up status   │    │ Site inventory  │    │ Risk flags      │
   │ Weld maps/logs  │    │ Safety/JHAs     │    │ Sub performance │
   │ QC checkpoints  │    │ Punch list      │    │ Change orders   │
   │ Production %    │    │ Photo docs      │    │ Payment status  │
   ├─────────────────┤    ├─────────────────┤    ├─────────────────┤
   │  Desktop-first  │    │  Mobile-first   │    │  Dashboard/Web  │
   │  Shop floor     │    │  Job site       │    │  Office / PM    │
   └─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┴───────────────────────┘
                                 │
                                 ▼
                    ┌───────────────────────┐
                    │   SAME JOB RECORD     │
                    │   One source of truth │
                    └───────────────────────┘
```

### Layer Breakdown

| Layer | Purpose | Who Sees | Who Edits |
|-------|---------|----------|-----------|
| **Shared** | Collaboration space — docs, RFIs, schedule, BOLs | All parties | All parties (their areas) |
| **Shop UI** | Fab production tools — materials, cutting, QC | Fab shop only | Fab shop only |
| **Field UI** | Erection tools — install, crew, safety | Erector only | Erector only |
| **GC UI** | Oversight & analytics — progress, budget, risk | GC/Owner only | GC/Owner only |

### User Experience

1. **Everyone lands on Shared Dashboard** — the common ground
2. **Click into role-specific UI** — your workbench with your tools
3. **Updates flow automatically** — fab shop marks "shipped" → erector sees "incoming" → GC sees progress update

### What Lives Where

**📋 SHARED DASHBOARD (All Parties)**

**📢 Message Board — Project Communication Hub**
```
One voice note → Transcribed → Everyone sees it instantly
┌─────────────────────────────────────────────────────────────────┐
│ 🔴 "Erector needs Area C steel by March 15" — J. Martinez, GC  │
│ 🟡 "Hold on grid line 7 - pending RFI-042" — Shop              │
│ 🟢 "Area A install complete, moving to B" — Field              │
│ 📎 "Revised sequence attached" — GC, 2 hrs ago                 │
└─────────────────────────────────────────────────────────────────┘
```
- Voice notes transcribed automatically
- Pin critical items to top
- Priority tags: 🔴 Critical, 🟡 Watch, 🟢 Info
- Anyone posts, everyone sees — full paper trail
- Replaces scattered texts/emails/calls

**📦 Received Summary — What's On Site**
```
┌──────────┬──────────┬──────────┬──────────┬──────────┐
│  STEEL   │  BOLTS   │   DECK   │  JOISTS  │   MISC   │
├──────────┼──────────┼──────────┼──────────┼──────────┤
│ 142 tons │   85%    │ 12,000SF │  48 pcs  │  22 pcs  │
│ of 210   │ on site  │ of 18k   │  of 72   │  of 35   │
│  (68%)   │(15% pend)│  (67%)   │  (67%)   │  (63%)   │
└──────────┴──────────┴──────────┴──────────┴──────────┘
```
- At-a-glance: what's on site vs what's needed
- Categories: Steel, bolts, deck, joists, misc, embeds, handrails
- Click any box to drill into details

**🏗️ 3D Model Viewer — Live Status on the Building**
```
┌─────────────────────────────────────────────────────────────┐
│  Click any piece in model:                                   │
│  → See mark #, heat #s, BOL, install date                   │
│  → Jump to drawing sheet                                     │
│  → Full lifecycle history                                    │
├─────────────────────────────────────────────────────────────┤
│  Color by status:                                            │
│  ⚪ Not started  🔵 Fabricated  🟢 Shipped                   │
│  🟡 On site      🟣 Installed   ✅ Complete                  │
└─────────────────────────────────────────────────────────────┘
```
- Model + drawings always in sync — auto-updates
- Bi-directional linking: Drawing ↔ Model ↔ Piece
- Tap piece on drawing → see where it goes in model
- Tap piece in model → jump to drawing sheet
- Erector ALWAYS has latest drawings — no outdated prints
- Revision posted → everyone sees it instantly

**The "no more outdated drawings" guarantee:**
> If it's in the Shared Dashboard, it's current. Period.
> No more "I was working off Rev 2" when Rev 5 is out.

**Core Shared Features:**
- Shop drawings (revisions, current set, RFI markups) — ALWAYS CURRENT
- RFIs (open, pending, resolved, who's holding the ball)
- Master schedule (milestones, critical path, delays)
- Load schedule (shipping calendar, what's on each truck)
- BOLs (all shipments, signed receipts, linked MTRs)
- Daily reports (combined shop + field activity)
- Documents library (contracts, specs, certs)

**🔩 SHOP UI (Fab Shop Only)**
- Material inventory (stock, heat numbers, MTRs)
- Production queue (what's next, priority order)
- Cut lists (by assembly, by load, by sequence)
- Fit-up tracking (who's fitting what)
- Weld maps & logs (welder assignments, WPS)
- QC checkpoints (hold points, inspection status)
- Fabrication % complete (by job, by load)

**🏗️ FIELD UI (Erector Only)**
- Incoming deliveries (what's arriving today/tomorrow)
- Site inventory (what's on ground, staged where)
- Install tracker (piece-by-piece status)
- Crew dispatch (who's doing what today)
- Safety docs (JHAs, toolbox talks, incident logs)
- Punch list (snags, corrections needed)
- Erection % complete (by area, by sequence)

**📱 Field Input Methods — Talk or Scan**
```
OPTION 1: Voice (Primary)                 OPTION 2: QR Scan (Detail View)
─────────────────────────────             ─────────────────────────────
🎤 "We set B-42 and B-43"                 📱 Scan QR on piece
       │                                         │
       ▼                                         ▼
🤖 Agent understands                      📄 See drawing
       │                                  🏗️ See in model  
       ▼                                  📍 See where it goes
✅ Status updated                               │
📋 Dashboard reflects                           ▼
                                          ✅ Tap to update status
                                          📸 Add photo
```

**Why voice-first works for ironworkers:**
- Hands dirty/gloved → Just talk
- 40 feet up on steel → Just talk  
- QR covered in paint → Just talk
- Faster than any app → Just talk

**"We set 12 pieces in Area C this morning"** → Agent updates all 12 → Done

The AI IS the interface. Not buttons. Not menus. Just talk.

**📊 GC UI (GC/Owner Only)**
- Project overview (overall %, earned value)
- Fab vs Erection gap (is steel piling up on site?)
- Schedule variance (ahead/behind, critical items)
- Sub performance (on-time %, quality scores)
- Risk flags (delays, bottlenecks, weather holds)
- Budget tracking (committed, spent, forecast)
- Payment status (invoices, retainage, releases)

### The GC Dashboard Vision

When a GC's project has both a fab shop AND erector on the platform:

```
PROJECT: Downtown Tower
├── Fabrication (ABC Steel Co.)  ─────────────────────
│   ├── 847 pieces total
│   ├── 612 fabricated ✅
│   ├── 180 in QC 🔄
│   ├── 55 not started ⏳
│   └── Next shipment: Tuesday (120 pcs)
│
├── Erection (XYZ Ironworks)  ────────────────────────
│   ├── 492 pieces received on site
│   ├── 410 installed ✅
│   ├── 82 awaiting install
│   └── Crew: 6 ironworkers today
│
└── Timeline  ────────────────────────────────────────
    ├── Fab: 72% complete (2 days ahead)
    └── Install: 48% complete (on schedule)
```

**No phone calls. No emails. Real-time visibility.**

### Why This Is THE Play

**1. Network Effects**
- Every fab shop signed → makes Field more valuable to erectors
- Every erector signed → makes Shop more valuable to fab shops
- GC dashboard only works with both → drives adoption of both

**2. Switching Costs**
- Once a GC sees this visibility, they'll REQUIRE subs to use it
- "Use [ProductName] or you're not on my bid list"

**3. Land & Expand Flywheel**
```
Sign fab shop 
    → They tell erector about it
        → Erector signs up
            → GC sees the magic
                → GC tells other subs on other projects
                    → Flywheel 🔄
```

**4. Nobody Else Has This**
- Tekla, Strumis, FabSuite → Stop at the shop door
- We go: Shop → Truck → Site → Installed → GC sees it all

### Pricing Structure (Phased Rollout)

**PHASE 1 PRICING: Trades Paid, GCs Free**

| Product | Tier | Monthly | Setup | Notes |
|---------|------|---------|-------|-------|
| 🔩 **Shop** | Starter | $500 | $2,500 | Small fab shops |
| 🔩 **Shop** | Professional | $1,500 | $7,500 | Mid-size fab shops |
| 🔩 **Shop** | Enterprise | $3,500 | $15,000 | Large fab shops |
| 🏗️ **Field** | Starter | $300 | $1,500 | Small erection crews |
| 🏗️ **Field** | Professional | $800 | $4,000 | Mid-size erectors |
| 🏗️ **Field** | Enterprise | $1,500 | $8,000 | Large erection companies |
| 📊 **GC View** | Free | **$0** | **$0** | View-only dashboard |

**Why GC is free (Phase 1):**
- Zero friction → easy to get them on platform
- They see the value → tell other subs to join
- Demand engine → drives trade signups
- Future upsell → paid GC features in Phase 2

**PHASE 2 PRICING: GC Paid Features (Q3 2026)**

| Product | Tier | Monthly | Setup | Features |
|---------|------|---------|-------|----------|
| 📊 **GC** | Starter | $500 | $2,500 | Super mobile tools, field RFIs |
| 📊 **GC** | Professional | $1,000 | $5,000 | + Multi-project, daily reports |
| 📊 **GC** | Enterprise | $2,500 | $10,000 | + Full platform, all trades |

**Bundle Discount:** Shop + Field together = 20% off both

### Seat-Based Revenue Model 💺

**Every user = a seat = recurring revenue**

| Plan | Base | Included | Extra Seat |
|------|------|----------|------------|
| 🔩 Shop Starter | $500/mo | 3 seats | +$50/seat |
| 🔩 Shop Pro | $1,500/mo | 10 seats | +$40/seat |
| 🔩 Shop Enterprise | $3,500/mo | 25 seats | +$30/seat |
| 🏗️ Field Starter | $300/mo | 5 seats | +$30/seat |
| 🏗️ Field Pro | $800/mo | 15 seats | +$25/seat |
| 🏗️ Field Enterprise | $1,500/mo | 40 seats | +$20/seat |
| 📊 GC Free | $0 | 3 seats | FREE |
| 📊 GC Starter | $500/mo | 5 seats | +$50/seat |
| 📊 GC Pro | $1,000/mo | 15 seats | +$40/seat |

**Revenue scales with customer growth:**
```
Day 1:   Shop Starter, 3 users     = $500/mo
Month 3: Add 5 more users          = $750/mo
Month 6: Add 7 more users          = $1,100/mo
Year 1:  Upgrade to Pro            = $1,500/mo
         │
         ▼
Revenue grows WITHOUT selling new deals
```

**Seat Types (optional future feature):**
| Type | Price | Access |
|------|-------|--------|
| Full User | $50/mo | Full edit |
| Viewer | $15/mo | View only |
| Field-Only | $25/mo | Mobile app only |

### The Magic Moment

When steel ships from Shop to a project where an erector uses Field:

1. **Shop:** Generates BOL with heat numbers, MTRs attached
2. **System:** Notifies Field app: "Load #4521 arriving tomorrow"
3. **Field:** Crew receives, confirms pieces, photos
4. **Connect:** GC dashboard updates automatically: "492 pieces on site"
5. **System:** Tracks installation as crew marks complete

**Zero manual data entry across company boundaries.**

### Market Reality

| Company Type | What They Need | Our Product |
|--------------|----------------|-------------|
| Fab shop only | Shop modules | **Shop** |
| Erector only | Field modules | **Field** |
| GC / CM | Visibility across subs | **Connect** |
| Vertically integrated (rare, like Del Bravo) | Everything | **Shop + Field** |

**Most companies = one product. The GLUE is Connect.**

---

## Lane 1: Steel Fabricator Product 🔩

### Product Name Ideas

| Name | Vibe | Domain Available? |
|------|------|-------------------|
| **FabCommand** | Direct, clear, industry-specific | fabcommand.com |
| **ShopBrain** | Memorable, implies intelligence | shopbrain.io |
| **SteelOps AI** | Professional, clear function | steelops.ai |
| **FabFlow** | Smooth, workflow-focused | fabflow.io |
| **IronMind** | Strong, memorable | ironmind.ai |
| **ForgeAI** | Industry-adjacent, powerful | forgeai.co |

**Recommendation:** Check domain availability, but **FabCommand** or **ShopBrain** hit the right notes.

---

### Product Packages (Steel Fabricators)

#### 🥉 STARTER — $500/month
*"Get your shop talking"*

**Ideal for:** Small shops, 5-20 employees, testing the waters

**Includes:**
- 1 AI Assistant (Shop Operations)
- Telegram/SMS access for team
- Daily production summaries
- Basic alerts & notifications
- Email integration
- 2 hours onboarding
- Email support

**They handle:** All subscriptions, basic setup

---

#### 🥈 PROFESSIONAL — $1,500/month
*"Your shop, on autopilot"*

**Ideal for:** Growing shops, 20-50 employees, multiple projects

**Includes everything in Starter, plus:**
- 3 AI Assistants (Ops, Purchasing, Field)
- PowerFab/FabSuite integration
- Shipping & delivery tracking
- RFQ & bid tracking dashboard
- Inventory alerts
- Calendar integration
- Weekly strategy reports
- 4 hours onboarding
- Priority support (Telegram direct)

---

#### 🥇 ENTERPRISE — $3,500/month
*"Full command center"*

**Ideal for:** Established shops, 50+ employees, complex operations

**Includes everything in Professional, plus:**
- Unlimited AI Assistants
- Custom integrations (Procore, Tekla, etc.)
- Multi-location support
- Advanced analytics & dashboards
- Document processing (BOLs, certs, MTRs)
- Dedicated account manager
- Monthly strategy calls
- Custom workflow development
- On-site training available
- 24/7 priority support

---

### Add-Ons (À la carte)

| Add-On | Price | Description |
|--------|-------|-------------|
| Additional AI Assistant | $200/mo | Specialized for specific function |
| Custom Integration | $2,500 one-time | Connect to any system with API |
| On-site Training | $2,500/day + travel | Hands-on team training |
| Custom Reporting | $500/mo | Tailored dashboards & reports |
| Dedicated Slack/Discord | $300/mo | Private team channel with AI |

---

### Implementation Fee (One-Time)

| Package | Setup Fee | Includes |
|---------|-----------|----------|
| Starter | $2,500 | Configuration, 2hr training, documentation |
| Professional | $7,500 | Full integration, 4hr training, workflows |
| Enterprise | $15,000 | Custom build, on-site training, full setup |

---

### Modular Licensing (À La Carte)

**For shops that want to start small or only need specific features.**

#### Individual Modules

| Module | What It Does | Monthly |
|--------|--------------|---------|
| 📊 **Estimating** | Quick takeoffs, cost breakdowns, bid prep | $300 |
| 📋 **Bid Dashboard** | Track RFQs, GCs, win rates, follow-ups | $200 |
| 📦 **Purchasing** | PO tracking, vendor management, receiving | $300 |
| 🔩 **Material Tracking** | Heat #s, full lifecycle, BOL generation | $400 |
| 🏭 **Shop Ops** | Production status, alerts, reporting | $400 |
| 🚚 **Shipping** | Load tracking, BOLs, delivery coordination | $200 |
| 📱 **Field Crew** | Erection tracking, site communication | $300 |

*Each module includes Telegram/SMS access + basic support.*

#### Module Setup Fees

| Modules | Setup Fee |
|---------|-----------|
| 1-2 modules | $1,500 |
| 3-4 modules | $3,500 |
| 5+ modules | $5,000 |

#### Bundle Discounts (Commit to Package = Save)

| Option | À La Carte | Bundle Price | Savings |
|--------|------------|--------------|---------|
| Pick any 2 | ~$400-600 | **$500** (Starter) | ~15% |
| Pick any 4 | ~$900-1,200 | **$1,500** (Professional) | ~25% |
| All modules | ~$2,100 | **$3,500** (Enterprise) | ~40% |

#### The Upsell Path

```
Month 1:  Buy Estimating ($300/mo)
          "Just want to try it out"
               ↓
Month 3:  Add Bid Dashboard ($200/mo)
          "This is working, can you track my bids too?"
               ↓
Month 6:  Add Purchasing + Material Tracking ($700/mo)
          "Let's do the whole purchasing flow"
               ↓
Month 12: Convert to Professional ($1,500/mo)
          "Just give me everything, this is saving us time"
```

#### Positioning vs. PowerFab/Strumis (DIRECT COMPETITION)

**We don't complement them. We replace them.**

```
POWERFAB / STRUMIS               BRAVO AI
(Legacy software)                (AI-native replacement)
─────────────────────────────    ─────────────────────────────
Built 10-20 years ago            Built for 2026
Database-first                   AI-first
Click through menus              Talk to it naturally
Complex desktop UI               Telegram/SMS/Web
$30-80k first year               $6-42k/year
Weeks of training                Learn in hours
Slow annual updates              Continuous improvement
On-premise or clunky cloud       Modern cloud-native
Same old workflows               Intelligent automation
```

**The pitch:**
> "Everything PowerFab does, but you talk to it instead of clicking through screens. And it costs 1/3 the price."

**Why we win:**
1. **AI-native** — Not AI bolted onto old software
2. **10x easier** — Text, don't click
3. **1/3 the cost** — No bloated enterprise pricing
4. **Built by fabricators** — We know the pain firsthand
5. **Modern stack** — Fast, reliable, always improving

---

## Lane 2: Custom AI Solutions 🌐

**The Bravo AI Consulting Arm**

For businesses outside steel fabrication who want custom AI automation.

| Package | Price | Scope |
|---------|-------|-------|
| Discovery | $2,500 | 2-day assessment, roadmap, proposal |
| Starter | $12,500 | 40 hrs, 3 weeks, basic implementation |
| Professional | $22,000 | 70 hrs, 6 weeks, full implementation |
| Enterprise | $40,000+ | 130+ hrs, complex multi-system builds |

*This is the current Bravo AI model — keeps working for non-fab clients.*

---

## Roadmap

### Phase 1: Foundation (Now - Q1 2026)
- [x] Build Command Center for Del Bravo Steel (Shop modules)
- [x] Document universal vs. custom components
- [x] Material tracking system with heat number lifecycle
- [x] Four-layer product architecture defined (Shared + Shop + Field + GC)
- [x] Voice-first input + QR scan workflows defined
- [x] Field RFI creation workflow defined
- [ ] Build Field modules for Del Bravo Erectors
- [ ] Create deployment templates
- [ ] Finalize product name + branding

### Phase 2: Launch Trades + Free GC (Q2 2026) 🚀
**Target: Fab shops + Erectors (paid) | GCs (free)**

| Product | Price | Goal |
|---------|-------|------|
| 🔩 Shop UI | $500-3,500/mo | 10 fab shops |
| 🏗️ Field UI | $300-1,500/mo | 5 erectors |
| 📋 Shared Dashboard | Included | Comes with paid tiers |
| 📊 GC View | **FREE** | Hook them, convert later |

- [ ] Launch Shop UI to market
- [ ] Launch Field UI to market  
- [ ] Free GC dashboard (view-only, see steel progress)
- [ ] Build marketing site for product
- [ ] First 10 fab shops + 5 erectors
- [ ] First cross-company project (Shop + Field + GC watching)
- [ ] Case study: "How [GC] got free real-time visibility"

**Free GC Strategy:**
```
GC gets free visibility
       ↓
GC sees the magic
       ↓
GC tells other subs: "Get on this"
       ↓
More trades sign up (paying)
       ↓
Flywheel kicks in 🔄
```

### Phase 3: Scale + GC Upsell (Q3-Q4 2026)
**Target: Convert free GCs to paid, network effects growing**

- [ ] Launch GC paid features:
  - Superintendent mobile tools
  - RFI from field
  - Automated daily reports
  - Multi-project dashboard
- [ ] GC paid tier: $500-1,500/mo
- [ ] Hire support/implementation help
- [ ] Content marketing (YouTube, LinkedIn, case studies)
- [ ] Attend AISC/NASCC conference
- [ ] Target: 20 Shop + 15 Field + 10 GC (5 paid) = $40k MRR

### Phase 4: Network Effects (2027)
**Target: GC demand pulls trades, flywheel accelerating**

- [ ] GCs requiring subs to use platform
- [ ] Build partner network (PowerFab consultants switching)
- [ ] Mobile apps for Field
- [ ] Expand to adjacent trades (deck, joists, misc metals)
- [ ] Advanced analytics / AI insights
- [ ] Target: 50 Shop + 40 Field + 30 GC = $100k MRR

### Phase 5: Platform (2028+)
**Target: Multi-trade coordination platform**

- [ ] Add more trades (concrete, MEP partnerships)
- [ ] Become the "operating system for construction projects"
- [ ] National expansion beyond Texas
- [ ] Potential acquisition target or raise funding
- [ ] Target: $500k+ MRR

---

## Revenue Projections

### Year 1 Targets (Conservative)

| Revenue Stream | Count | Avg Price | Annual |
|----------------|-------|-----------|--------|
| Shop subscriptions | 10 | $1,200/mo | $144,000 |
| Field subscriptions | 5 | $600/mo | $36,000 |
| Connect subscriptions | 3 | $400/mo | $14,400 |
| Setup fees | 18 | $4,000 avg | $72,000 |
| Consulting projects | 4 | $20,000 avg | $80,000 |
| **Total Year 1** | | | **$346,400** |

*Monthly run rate by Dec Y1: ~$20k MRR*

### Year 2 Targets (Network Effects Kicking In)

| Revenue Stream | Count | Avg Price | Annual |
|----------------|-------|-----------|--------|
| Shop subscriptions | 35 | $1,400/mo | $588,000 |
| Field subscriptions | 20 | $700/mo | $168,000 |
| Connect subscriptions | 15 | $500/mo | $90,000 |
| Setup fees | 50 | $4,500 avg | $225,000 |
| Consulting projects | 6 | $25,000 avg | $150,000 |
| **Total Year 2** | | | **$1,221,000** |

*Monthly run rate by Dec Y2: ~$85k MRR*

### The Flywheel Math

```
Year 1: Land 10 fab shops
Year 2: Those fab shops' projects → 20 erectors discover us
Year 2: GCs see the magic → 15 Connect subscriptions
Year 3: GCs require subs to use it → exponential growth
```

**Connect is loss-leader if needed** — the real money is Shop + Field subscriptions driven by GC demand.

---

## Competitive Advantage

**Why Bravo AI beats PowerFab, Strumis, and FabSuite:**

1. **AI-native architecture** — Built from scratch with AI, not bolted on
2. **10x easier to use** — Text commands, not complex menu navigation
3. **1/3 the price** — No enterprise bloat, no perpetual license games
4. **Built by fabricators** — Mario knows the pain points firsthand
5. **Faster deployment** — Days, not months to go live
6. **Modern tech stack** — Cloud-native, mobile-first, always improving
7. **Accessible anywhere** — Telegram/SMS from the shop floor, not desktop-only
8. **Relationship-based** — We're in the industry, we show up at NASCC

**The long-term goal:**
> Complete replacement for legacy fab shop software. AI-native from day one.

**Our Unfair Advantage: AI-Powered Development**

```
POWERFAB/STRUMIS                 BRAVO AI
─────────────────────────────    ─────────────────────────────
Feature request → 6-12 months    Feature request → DAYS
Annual update cycle              Weekly improvements
"Submit a ticket"                "Text us what you need"
Same software for everyone       Customized per shop
Expensive professional services  AI builds it for you
```

**The Secret Weapon:**
We use AI to BUILD the product, not just run it. When a customer needs something custom:
- Traditional vendor: "We'll add it to the roadmap" (never happens)
- Bravo AI: "Done by Friday"

**Simpler. Cheaper. Better. Faster.**

This is how a small team beats enterprise giants.

---

## Immediate Next Steps

1. **Pick a product name** — Domain check, trademark search
2. **Refine packages** — Validate pricing with 2-3 shop owners
3. **Create product landing page** — Separate from bravoai.co or subdomain
4. **Build demo instance** — Sandbox for prospects to try
5. **Draft Software License Agreement** — Protect IP for SaaS delivery

---

*This document is a living roadmap. Update as we learn from customers.*
