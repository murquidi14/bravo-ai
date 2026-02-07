# IP Protection Guide — Bravo AI / FabCommand

*Step-by-step playbook to protect your software assets*

---

## Overview: Layers of Protection

```
┌─────────────────────────────────────────────────────────────────┐
│                    IP PROTECTION STACK                          │
├─────────────────────────────────────────────────────────────────┤
│  🔒 TRADE SECRETS        — Keep it confidential (FREE)          │
│  📝 COPYRIGHT            — Protect the code ($35-65)            │
│  ™️ TRADEMARK             — Protect the name ($250-350)          │
│  📜 CONTRACTS            — Control how it's used (FREE)         │
│  🛡️ TECHNICAL CONTROLS   — Prevent unauthorized access (FREE)   │
│  📋 PATENT (Optional)    — Protect the method ($10-15k)         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Step 1: Trade Secrets (Do This NOW — FREE)

Trade secrets protect your confidential business information as long as you keep it secret.

### What counts as trade secrets:
- AI prompts and system instructions
- Workflow logic and automation rules
- Integration methods and configurations
- Pricing algorithms
- Client data and insights
- Training materials and documentation

### Actions to take:

**A. Create a Trade Secrets Policy**
```markdown
BRAVO AI CONFIDENTIAL
This document contains proprietary trade secrets of Bravo AI LLC.
Unauthorized disclosure, copying, or distribution is prohibited.
```

**B. Mark all confidential documents**
- Add "CONFIDENTIAL" or "PROPRIETARY" headers
- Include confidentiality notices in code comments
- Mark folders/repos as private

**C. Limit access**
- Only share what's necessary
- Use NDAs before ANY demonstrations
- Keep master templates separate from client versions

**D. Document your secrets**
Create a "Trade Secrets Register" listing what's protected:
- Core prompt library
- Workflow templates
- Integration configurations
- Pricing models
- Client onboarding process

✅ **Action Item:** Create a TRADE-SECRETS-REGISTER.md file listing all confidential assets

---

## Step 2: Copyright Registration ($35-65)

Copyright protects the actual code, documentation, and creative works.

### What's automatically protected (but register anyway):
- Source code
- Documentation
- Training materials
- Website content
- Marketing materials
- Prompt libraries (as literary works)

### How to register:

1. **Go to:** https://www.copyright.gov/registration/
2. **Choose:** "Literary Work" (for software/code)
3. **Pay:** $35 (single author, online) or $65 (standard)
4. **Submit:** Deposit copy of code (can be partial/redacted)
5. **Timeline:** 2-8 months for certificate

### What to register:
- Main software codebase (as one work)
- Documentation package (as one work)
- Prompt library (as literary work)

✅ **Action Item:** Register copyright for core software — budget $100-200 total

---

## Step 3: Trademark ($250-350)

Trademark protects your brand name and logo.

### What to trademark:
- Product name (FabCommand, ShopBrain, etc.)
- Company name (Bravo AI)
- Logo
- Tagline ("AI for Modern Fabrication")

### Before filing — Search first:
1. **USPTO Search:** https://tmsearch.uspto.gov
2. **Google search** the name + competitors
3. **Domain availability** check
4. **Social media** handles available?

### How to register:

1. **Go to:** https://www.uspto.gov/trademarks
2. **Choose:** TEAS Plus ($250) or TEAS Standard ($350)
3. **File for:** Class 042 (Software as a service)
4. **Describe:** "Software as a service for manufacturing operations management"
5. **Timeline:** 8-12 months for approval

### Alternative — Start with "TM"
You can use ™ symbol immediately (no registration needed).
® symbol only after federal registration.

✅ **Action Item:** Search and reserve product name, file trademark application

---

## Step 4: Contracts (FREE but Critical)

Contracts control how clients can use your software.

### A. Software License Agreement
**Key terms to include:**
- Grant of license (not ownership transfer)
- Restrictions (no copying, reverse engineering, resale)
- Term and termination
- IP ownership (you own everything)
- Confidentiality obligations
- Limitation of liability

### B. Terms of Service
For SaaS products — users agree by using the software:
- Acceptable use policy
- Account responsibilities
- Service level commitments
- Data handling
- Termination rights

### C. NDA (Non-Disclosure Agreement)
Use BEFORE any demos or discussions:
- Already have template in `/templates/nda.md`
- Get signed before showing Command Center

### D. Update your MSA
Add stronger IP clauses:
- All work product belongs to Bravo AI
- Client gets license, not ownership
- Improvements stay with Bravo AI

✅ **Action Item:** Draft Software License Agreement and Terms of Service

---

## Step 5: Technical Controls (FREE)

Prevent unauthorized access and copying.

### A. Keep core IP on your infrastructure
```
CLIENT ACCESS:
  └── Telegram bot → API calls → YOUR SERVER → Database

THEY NEVER SEE:
  └── Source code
  └── Prompt library
  └── Workflow configs
  └── Integration logic
```

### B. Private repositories
- GitHub repo set to PRIVATE ✓
- Limit collaborator access
- Use branch protection rules
- Audit access regularly

### C. Environment separation
```
/bravo-core/          ← NEVER shared (trade secrets)
  /prompts/
  /workflows/
  /integrations/

/client-configs/      ← Client-specific only
  /clientA/
  /clientB/
```

### D. Licensing keys (future)
For software distribution:
- Unique license key per client
- Phone-home validation
- Feature flags by tier

✅ **Action Item:** Audit repo access, separate core from client configs

---

## Step 6: Patent (Optional — $10-15k)

Patents protect novel methods and processes. Most expensive, but strongest.

### When to consider:
- You invented a truly novel method
- Competitors could copy your approach
- You want to block others from the market
- You might seek investment (VCs like patents)

### What might be patentable:
- Novel AI workflow for fabrication scheduling
- Unique integration method between systems
- Specific algorithm for inventory optimization

### Process:
1. **Provisional patent:** $1,500-3,000 (buys 12 months)
2. **Utility patent:** $10,000-15,000 (full protection, 20 years)
3. **Timeline:** 2-3 years for approval

### Recommendation:
Wait until you have revenue and proven product. Patents are expensive and time-consuming. Focus on trade secrets and contracts first.

✅ **Action Item:** Bookmark for later — revisit at $500k ARR

---

## Priority Action Checklist

### This Week (FREE)
- [ ] Create TRADE-SECRETS-REGISTER.md
- [ ] Add confidentiality headers to all docs
- [ ] Make GitHub repo private (if not already)
- [ ] Separate core IP from client configs
- [ ] Search product name availability (trademark, domain)

### This Month ($100-300)
- [ ] Register copyright for software ($35-65)
- [ ] File trademark application ($250-350)
- [ ] Draft Software License Agreement
- [ ] Draft Terms of Service
- [ ] Update MSA with stronger IP language

### This Quarter
- [ ] Implement license key system
- [ ] Create client deployment process (protects core)
- [ ] Document all proprietary methods
- [ ] Set up audit trail for access

### When Revenue Hits $500k+
- [ ] Consult IP attorney for full strategy
- [ ] Consider provisional patent
- [ ] Trademark additional product names
- [ ] International trademark filing (if expanding)

---

## Quick Reference: What Protects What

| Asset | Protection | Cost | Timeline |
|-------|------------|------|----------|
| Code & docs | Copyright | $35-65 | 2-8 months |
| Product name | Trademark | $250-350 | 8-12 months |
| Secret methods | Trade secrets | FREE | Immediate |
| Client usage | Contracts | FREE | Immediate |
| Access control | Technical | FREE | Immediate |
| Novel inventions | Patent | $10-15k | 2-3 years |

---

## Resources

- **Copyright registration:** https://www.copyright.gov
- **Trademark search:** https://tmsearch.uspto.gov
- **Trademark filing:** https://www.uspto.gov/trademarks
- **NDA template:** `/templates/nda.md`
- **MSA template:** `/templates/master-service-agreement.md`

---

*Protect it now. It's easier to prevent theft than recover from it.*
