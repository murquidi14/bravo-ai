# Database Schema — Shared Dashboard

*Created: February 7, 2026*

---

## Overview

```
COMPANIES ─────┬───── USERS
               │
               ▼
         SUBSCRIPTIONS (seat-based)
               │
               ▼
            JOBS ─────── JOB_COMPANIES (who's on what job)
               │                │
               │                ▼
               │         JOB_USERS (role per user per job)
               │
               ▼
         JOB DATA (messages, docs, pieces, etc.)
```

---

## Core Tables

### 1. Companies

```sql
CREATE TABLE companies (
  id              UUID PRIMARY KEY,
  name            VARCHAR(255) NOT NULL,
  type            ENUM('fabricator', 'erector', 'gc', 'owner', 'other'),
  email           VARCHAR(255),
  phone           VARCHAR(50),
  address         TEXT,
  logo_url        VARCHAR(500),
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

-- Example:
-- { id: 'abc-123', name: 'Del Bravo Steel', type: 'fabricator' }
```

### 2. Users

```sql
CREATE TABLE users (
  id              UUID PRIMARY KEY,
  company_id      UUID REFERENCES companies(id),
  email           VARCHAR(255) UNIQUE NOT NULL,
  phone           VARCHAR(50),
  name            VARCHAR(255) NOT NULL,
  role_in_company ENUM('owner', 'admin', 'manager', 'user'),
  avatar_url      VARCHAR(500),
  auth_provider   VARCHAR(50),          -- 'email', 'google', 'microsoft'
  auth_id         VARCHAR(255),         -- External auth ID
  last_login      TIMESTAMP,
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

-- Example:
-- { id: 'user-1', company_id: 'abc-123', name: 'Mario', role_in_company: 'owner' }
```

### 3. Subscriptions (Seat-Based)

```sql
CREATE TABLE subscriptions (
  id              UUID PRIMARY KEY,
  company_id      UUID REFERENCES companies(id),
  plan            ENUM('shop_starter', 'shop_pro', 'shop_enterprise',
                       'field_starter', 'field_pro', 'field_enterprise',
                       'gc_free', 'gc_starter', 'gc_pro'),
  status          ENUM('active', 'past_due', 'cancelled', 'trial'),
  included_seats  INT NOT NULL,
  extra_seats     INT DEFAULT 0,
  price_base      DECIMAL(10,2),        -- Monthly base price
  price_per_seat  DECIMAL(10,2),        -- Per extra seat
  billing_cycle   ENUM('monthly', 'annual'),
  current_period_start TIMESTAMP,
  current_period_end   TIMESTAMP,
  stripe_customer_id   VARCHAR(255),
  stripe_subscription_id VARCHAR(255),
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

-- Seat count enforcement:
-- Total seats allowed = included_seats + extra_seats
-- Compare against COUNT of active users in company
```

### 4. Jobs (Projects)

```sql
CREATE TABLE jobs (
  id              UUID PRIMARY KEY,
  name            VARCHAR(255) NOT NULL,
  number          VARCHAR(100),         -- Job number (e.g., 'DT-2026-042')
  address         TEXT,
  city            VARCHAR(100),
  state           VARCHAR(50),
  status          ENUM('active', 'completed', 'on_hold', 'archived'),
  start_date      DATE,
  target_end_date DATE,
  actual_end_date DATE,
  created_by      UUID REFERENCES users(id),
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

-- Example:
-- { id: 'job-1', name: 'Downtown Tower', number: 'DT-2026-042' }
```

### 5. Job Companies (Which companies are on which jobs)

```sql
CREATE TABLE job_companies (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  company_id      UUID REFERENCES companies(id),
  role            ENUM('fabricator', 'erector', 'gc', 'owner', 'engineer', 'other'),
  invited_by      UUID REFERENCES users(id),
  accepted_at     TIMESTAMP,
  created_at      TIMESTAMP DEFAULT NOW(),
  
  UNIQUE(job_id, company_id)  -- One company per role per job
);

-- Example:
-- { job_id: 'job-1', company_id: 'abc-123', role: 'fabricator' }
-- { job_id: 'job-1', company_id: 'xyz-456', role: 'erector' }
-- { job_id: 'job-1', company_id: 'gc-789', role: 'gc' }
```

### 6. Job Users (User permissions per job)

```sql
CREATE TABLE job_users (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  user_id         UUID REFERENCES users(id) ON DELETE CASCADE,
  company_id      UUID REFERENCES companies(id),
  role            ENUM('admin', 'manager', 'user', 'viewer'),
  access_shop     BOOLEAN DEFAULT FALSE,
  access_field    BOOLEAN DEFAULT FALSE,
  access_gc       BOOLEAN DEFAULT FALSE,
  access_shared   BOOLEAN DEFAULT TRUE,
  can_invite      BOOLEAN DEFAULT FALSE,
  invited_by      UUID REFERENCES users(id),
  created_at      TIMESTAMP DEFAULT NOW(),
  
  UNIQUE(job_id, user_id)
);

-- Example: Fab shop admin on a job
-- { job_id: 'job-1', user_id: 'user-1', role: 'admin', 
--   access_shop: true, access_field: false, access_gc: false, access_shared: true }
```

---

## Job Data Tables

### 7. Messages (Message Board)

```sql
CREATE TABLE messages (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  user_id         UUID REFERENCES users(id),
  company_id      UUID REFERENCES companies(id),
  content         TEXT NOT NULL,
  priority        ENUM('critical', 'watch', 'info') DEFAULT 'info',
  is_pinned       BOOLEAN DEFAULT FALSE,
  piece_id        UUID REFERENCES pieces(id),   -- Optional: tagged to piece
  parent_id       UUID REFERENCES messages(id), -- For threading
  voice_url       VARCHAR(500),                 -- If voice message
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

-- Indexes for fast queries
CREATE INDEX idx_messages_job ON messages(job_id, created_at DESC);
CREATE INDEX idx_messages_piece ON messages(piece_id);
```

### 8. Documents (Drawings, BOLs, etc.)

```sql
CREATE TABLE documents (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  uploaded_by     UUID REFERENCES users(id),
  company_id      UUID REFERENCES companies(id),
  type            ENUM('drawing', 'bol', 'mtr', 'rfi', 'submittal', 'photo', 'report', 'other'),
  name            VARCHAR(255) NOT NULL,
  file_url        VARCHAR(500) NOT NULL,
  file_size       INT,
  mime_type       VARCHAR(100),
  revision        VARCHAR(50),
  is_current      BOOLEAN DEFAULT TRUE,        -- Latest revision?
  supersedes      UUID REFERENCES documents(id), -- Previous version
  piece_id        UUID REFERENCES pieces(id),   -- Optional: linked to piece
  created_at      TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_documents_job ON documents(job_id, type);
CREATE INDEX idx_documents_current ON documents(job_id, is_current);
```

### 9. Pieces (Steel pieces with status)

```sql
CREATE TABLE pieces (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  mark            VARCHAR(100) NOT NULL,       -- Piece mark (e.g., 'B-42')
  description     TEXT,
  weight          DECIMAL(10,2),               -- lbs
  quantity        INT DEFAULT 1,
  
  -- Status tracking
  status          ENUM('not_started', 'fabricating', 'fabricated', 
                       'shipped', 'on_site', 'staged', 'installed', 
                       'bolted', 'complete'),
  
  -- Location in model
  level           VARCHAR(50),
  grid_line       VARCHAR(50),
  sequence        INT,
  
  -- Traceability
  heat_numbers    TEXT[],                      -- Array of heat numbers
  
  -- Timestamps per stage
  fab_started_at  TIMESTAMP,
  fab_complete_at TIMESTAMP,
  qc_passed_at    TIMESTAMP,
  shipped_at      TIMESTAMP,
  received_at     TIMESTAMP,
  installed_at    TIMESTAMP,
  
  -- Who updated
  last_updated_by UUID REFERENCES users(id),
  
  -- QR code
  qr_code         VARCHAR(255),
  
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_pieces_job ON pieces(job_id);
CREATE INDEX idx_pieces_status ON pieces(job_id, status);
CREATE INDEX idx_pieces_mark ON pieces(job_id, mark);
```

### 10. RFIs

```sql
CREATE TABLE rfis (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  number          VARCHAR(50),                 -- RFI-001
  subject         VARCHAR(500) NOT NULL,
  description     TEXT,
  status          ENUM('draft', 'submitted', 'pending', 'answered', 'closed'),
  priority        ENUM('low', 'medium', 'high', 'critical'),
  
  -- Who
  created_by      UUID REFERENCES users(id),
  assigned_to     UUID REFERENCES users(id),
  company_id      UUID REFERENCES companies(id),
  
  -- Linked items
  piece_id        UUID REFERENCES pieces(id),
  location        VARCHAR(255),                -- Grid/level reference
  
  -- Response
  response        TEXT,
  responded_by    UUID REFERENCES users(id),
  responded_at    TIMESTAMP,
  
  -- Dates
  due_date        DATE,
  created_at      TIMESTAMP DEFAULT NOW(),
  updated_at      TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_rfis_job ON rfis(job_id, status);
```

### 11. Daily Reports

```sql
CREATE TABLE daily_reports (
  id              UUID PRIMARY KEY,
  job_id          UUID REFERENCES jobs(id) ON DELETE CASCADE,
  report_date     DATE NOT NULL,
  company_id      UUID REFERENCES companies(id),
  submitted_by    UUID REFERENCES users(id),
  
  -- Field data
  crew_count      INT,
  hours_worked    DECIMAL(5,2),
  weather         VARCHAR(100),
  temperature     VARCHAR(50),
  work_performed  TEXT,
  issues          TEXT,
  
  -- Pieces affected
  pieces_installed TEXT[],                     -- Array of piece marks
  
  created_at      TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_reports_job ON daily_reports(job_id, report_date DESC);
```

---

## Seat-Based Pricing Rules

### Pricing Table

| Plan | Base | Included Seats | Extra Seat | Seat Types |
|------|------|----------------|------------|------------|
| shop_starter | $500/mo | 3 | $50/mo | Full |
| shop_pro | $1,500/mo | 10 | $40/mo | Full |
| shop_enterprise | $3,500/mo | 25 | $30/mo | Full |
| field_starter | $300/mo | 5 | $30/mo | Full + Field |
| field_pro | $800/mo | 15 | $25/mo | Full + Field |
| field_enterprise | $1,500/mo | 40 | $20/mo | Full + Field |
| gc_free | $0 | 3 | FREE | Viewer only |
| gc_starter | $500/mo | 5 | $50/mo | Full |
| gc_pro | $1,000/mo | 15 | $40/mo | Full |

### Seat Enforcement Logic

```sql
-- Function to check if company can add more users
CREATE FUNCTION can_add_user(company_uuid UUID) RETURNS BOOLEAN AS $$
DECLARE
  sub RECORD;
  current_users INT;
  max_users INT;
BEGIN
  -- Get subscription
  SELECT * INTO sub FROM subscriptions 
  WHERE company_id = company_uuid AND status = 'active';
  
  -- Count current users
  SELECT COUNT(*) INTO current_users FROM users 
  WHERE company_id = company_uuid;
  
  -- Calculate max
  max_users := sub.included_seats + sub.extra_seats;
  
  RETURN current_users < max_users;
END;
$$ LANGUAGE plpgsql;
```

---

## Permission Check Logic

```sql
-- Can user access job?
CREATE FUNCTION can_access_job(user_uuid UUID, job_uuid UUID) RETURNS BOOLEAN AS $$
BEGIN
  RETURN EXISTS (
    SELECT 1 FROM job_users 
    WHERE user_id = user_uuid AND job_id = job_uuid
  );
END;
$$ LANGUAGE plpgsql;

-- Can user edit in job?
CREATE FUNCTION can_edit_job(user_uuid UUID, job_uuid UUID) RETURNS BOOLEAN AS $$
DECLARE
  ju RECORD;
BEGIN
  SELECT * INTO ju FROM job_users 
  WHERE user_id = user_uuid AND job_id = job_uuid;
  
  RETURN ju.role IN ('admin', 'manager', 'user');
END;
$$ LANGUAGE plpgsql;

-- Can user access specific UI?
CREATE FUNCTION can_access_ui(user_uuid UUID, job_uuid UUID, ui VARCHAR) RETURNS BOOLEAN AS $$
DECLARE
  ju RECORD;
BEGIN
  SELECT * INTO ju FROM job_users 
  WHERE user_id = user_uuid AND job_id = job_uuid;
  
  CASE ui
    WHEN 'shop' THEN RETURN ju.access_shop;
    WHEN 'field' THEN RETURN ju.access_field;
    WHEN 'gc' THEN RETURN ju.access_gc;
    WHEN 'shared' THEN RETURN ju.access_shared;
    ELSE RETURN FALSE;
  END CASE;
END;
$$ LANGUAGE plpgsql;
```

---

## Sample Data Flow

### Creating a Job

```sql
-- 1. Fab shop admin creates job
INSERT INTO jobs (id, name, number, created_by) 
VALUES ('job-1', 'Downtown Tower', 'DT-2026-042', 'mario-id');

-- 2. Add fab shop company to job
INSERT INTO job_companies (job_id, company_id, role)
VALUES ('job-1', 'delbravo-steel', 'fabricator');

-- 3. Add fab shop users to job
INSERT INTO job_users (job_id, user_id, company_id, role, access_shop, access_shared, can_invite)
VALUES ('job-1', 'mario-id', 'delbravo-steel', 'admin', TRUE, TRUE, TRUE);

-- 4. Mario invites erector company
INSERT INTO job_companies (job_id, company_id, role, invited_by)
VALUES ('job-1', 'xyz-erectors', 'erector', 'mario-id');

-- 5. Erector admin joins and adds their crew
INSERT INTO job_users (job_id, user_id, company_id, role, access_field, access_shared)
VALUES 
  ('job-1', 'tom-id', 'xyz-erectors', 'admin', TRUE, TRUE),
  ('job-1', 'juan-id', 'xyz-erectors', 'user', TRUE, TRUE);

-- 6. Invite GC with free view-only access
INSERT INTO job_companies (job_id, company_id, role, invited_by)
VALUES ('job-1', 'turner-gc', 'gc', 'mario-id');

INSERT INTO job_users (job_id, user_id, company_id, role, access_gc, access_shared)
VALUES ('job-1', 'lisa-pm', 'turner-gc', 'viewer', TRUE, TRUE);
```

---

## Next Steps

1. **Choose database:** PostgreSQL recommended (Supabase for easy setup)
2. **Build API layer:** Next.js API routes or separate Node/Express
3. **Build auth:** Supabase Auth or NextAuth.js
4. **Build UI:** Start with Message Board component

---

*This schema supports the full permission model with seat-based pricing.*
