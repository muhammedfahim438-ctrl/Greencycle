# GreenCycle Nexus — Run Instructions

## Folder Structure
```
greencycle-nexus/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── models.py
│   │   └── routes.py
│   ├── requirements.txt
│   └── run.py
└── app.html
```

---

## 1. Start the Backend

```bash
cd greencycle-nexus/backend

# Create virtual env (recommended)
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run Flask
python run.py
```

Server starts at: **http://127.0.0.1:5000**

The SQLite database (`greencycle.db`) is auto-created on first run.
Three demo accounts are auto-seeded.

---

## 2. Open the Frontend

Just open `app.html` in your browser — **no server needed**.

```bash
open greencycle-nexus/app.html       # macOS
xdg-open greencycle-nexus/app.html   # Linux
# Or double-click the file in Windows Explorer
```

---

## Demo Accounts

| Role    | Phone      | PIN  |
|---------|------------|------|
| Admin   | 9000000001 | 1111 |
| Citizen | 9000000002 | 2222 |
| Worker  | 9000000003 | 3333 |

---

## Pricing Logic

| Type    | Rate     |
|---------|----------|
| Food    | ₹2 / kg  |
| Plastic | ₹3 / kg  |
| Other   | ₹1 / kg  |

**Flow:** Citizen logs waste → Admin approves → Payment auto-generated (due in 7 days)

---

## API Endpoints

| Method | Endpoint              | Auth     | Description              |
|--------|-----------------------|----------|--------------------------|
| POST   | /register             | —        | Create account           |
| POST   | /login                | —        | Login, get token         |
| POST   | /waste                | Bearer   | Log waste entry          |
| GET    | /history/:user_id     | Bearer   | User's waste history     |
| GET    | /pending              | Admin    | Unapproved entries       |
| POST   | /approve/:id          | Admin    | Approve + create payment |
| GET    | /payments/:user_id    | Bearer   | Payments + total due     |
| GET    | /schedule/:user_id    | Bearer   | Pickup schedule          |
| GET    | /pickups/:worker_id   | Bearer   | Worker's pickups         |
| POST   | /collect/:id          | Bearer   | Mark pickup collected    |

---

## Future Extensions
- GPS tracking for workers
- WhatsApp alerts via Twilio
- Ward / zone mapping
- OTP-based login
- Payment gateway integration
