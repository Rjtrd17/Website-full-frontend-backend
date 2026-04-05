# PostgreSQL Setup Guide
**For Harsidhdhi Mataji Temple Website Backend Migration**

This guide provides step-by-step instructions for moving from a static frontend-only site to a dynamic PostgreSQL-backed architecture, separating public and admin concerns.

## 1. Prerequisites
- **PostgreSQL Database Server:** Download from [postgresql.org](https://www.postgresql.org/download/) or use a managed service like AWS RDS, Supabase, or Render.
- **Node.js (Backend server):** Download from [nodejs.org](https://nodejs.org/). This will act as the API layer.

## 2. Database Schema Creation

Create a new database named `harsidhdhi_temple_db`.

Run the following SQL script to initialize the core tables:

```sql
-- Gallery Images Table
CREATE TABLE gallery_images (
    id SERIAL PRIMARY KEY,
    image_url TEXT NOT NULL,
    title_gu VARCHAR(255),
    title_en VARCHAR(255),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Livestream Config Table
CREATE TABLE livestream_config (
    id SERIAL PRIMARY KEY,
    youtube_url TEXT NOT NULL,
    is_live BOOLEAN DEFAULT FALSE,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Donations Ledger Table
CREATE TABLE donations (
    id SERIAL PRIMARY KEY,
    donor_name VARCHAR(150),
    contact_number VARCHAR(15),
    amount DECIMAL(10, 2) NOT NULL,
    transaction_id VARCHAR(100) UNIQUE,
    payment_status VARCHAR(50) DEFAULT 'PENDING',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 3. Backend Integration (Node.js/Express)
You will need a backend server to safely connect to PostgreSQL.
Do **NOT** connect frontend HTML/JS directly to PostgreSQL, as it will expose your database credentials.

1. **Initialize Project:** `npm init -y`
2. **Install Dependencies:** `npm install express pg cors dotenv`
3. **Connect PG Plugin:**
```javascript
const { Pool } = require('pg');
const pool = new Pool({
  user: 'admin',
  host: 'localhost',
  database: 'harsidhdhi_temple_db',
  password: 'your_password',
  port: 5432,
});
```

## 4. Connecting `admin.html`
Modify the `saveSettings` functions in `admin.html` to send `POST` requests via `fetch()` to your newly created Node.js endpoints (e.g., `POST /api/admin/livestream` with the URL payload) which will run an `INSERT/UPDATE` on PostgreSQL.
