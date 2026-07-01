# FitZone Gym Website

A full-stack gym membership platform built with Flask — featuring a dynamic 3D landing page, complete user authentication system, membership plan gating, and a live admin dashboard powered by Anvil Works. Deployed on PythonAnywhere and live for **1+ month** with zero downtime.

🔗 **Live Site: [krishnakarthik09.pythonanywhere.com](https://krishnakarthik09.pythonanywhere.com)**

---

## What It Does

- Visitors can browse the gym, view programs, and see membership plans on a 3D animated landing page
- **Login / Sign Up** buttons let users create an account or log in
- Once logged in, the nav updates to show the user's name and a Logout button, and the **"Get Membership"** button unlocks
- Clicking "Get Membership" redirects to a connected **Anvil Works app**, where users fill in their details to join the gym
- At the bottom of the enrollment form, an **Admin Login** button lets an admin securely log in with a password
- After admin login, a live **Subscriptions Dashboard** displays:
  - Total Members
  - Active / Expired subscriptions
  - Total Revenue
  - A member-wise table with Plan, Status, Renewal Date, Last Payment, and Amount

---

## Features

- Full user authentication — signup, login, logout (Flask)
- Passwords hashed using `werkzeug.security` — never stored as plain text
- Session management via Flask-Login — server remembers logged-in users across requests
- SQLite database storing user accounts (via Flask-SQLAlchemy)
- Duplicate username detection with user-friendly error messages
- Route protection — membership button hidden/locked until authenticated
- Cross-app integration — Flask login gates access to a separate **Anvil Works** membership + admin system
- Password-protected admin dashboard with live stats pulled from a two-table (Members + Subscriptions) database
- 3D rotating dumbbell landing page built with Three.js (drag to rotate)
- Fully responsive dark neon design matching the FitZone brand

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend (Auth site) | Python 3, Flask |
| Database (Auth site) | SQLite via Flask-SQLAlchemy |
| Auth | Flask-Login, Werkzeug password hashing |
| Frontend | HTML, CSS, Jinja2 templates |
| 3D Graphics | Three.js (r128) |
| Membership + Admin App | Anvil Works (Python-based low-code app) |
| Hosting | PythonAnywhere (live for 1+ month) |

---

## Project Structure

```
fitzone-gym-auth/
  app.py                  # Flask app — routes, auth logic, database models
  templates/
    index.html            # Landing page (3D dumbbell, programs, plans, CTA)
    login.html            # Login form — dark themed, matches brand
    signup.html           # Signup form — dark themed, matches brand
  instance/
    gym.db                # SQLite database (gitignored — not in repo)
  .gitignore
```

---

## App Flow

```
Visitor lands on /
    ↓
Clicks "Login" or "Sign Up"
    ↓
Redirected to /signup → username + password → hashed + saved to gym.db
    ↓
Redirected to /login → credentials checked against hash
    ↓
login_user() creates session cookie
    ↓
Back to / — nav shows username + Logout, "Get Membership" unlocked
    ↓
Clicks "Get Membership" → redirected to Anvil Works enrollment form
    ↓
User fills in personal + plan details → saved to Anvil's Members/Subscriptions tables
    ↓
Admin clicks "Admin Login" on the form → enters admin password
    ↓
Admin Dashboard loads → shows Total Members, Active/Expired count, Revenue, and full member table
    ↓
/logout (on Flask site) → session cleared → back to /
```

---

## Running Locally (Flask App)

```bash
# Clone the repo
git clone https://github.com/krishnakarthik09/fitzone-gym-auth-.git
cd fitzone-gym-auth-

# Install dependencies
pip install flask flask-sqlalchemy flask-login

# Run the app
python app.py
```

Visit `http://127.0.0.1:5000`
The database (`gym.db`) is created automatically on first run inside an `instance/` folder.

> Note: The Anvil Works membership + admin app runs as a separate hosted service and is accessed via the live link above.

---

## Security Notes

- Passwords are never stored in plain text — only a `werkzeug` hash is saved
- The `SECRET_KEY` in `app.py` should be replaced with a long random string before production use
- `gym.db` is excluded from the repo via `.gitignore` to avoid exposing user data
- Flask-Login session cookies are cryptographically signed using the secret key
- The Anvil admin dashboard is protected behind a separate admin password before revealing member data

---

## Live Demo

1. Visit **[krishnakarthik09.pythonanywhere.com](https://krishnakarthik09.pythonanywhere.com)**
2. Create an account and log in — the **Get Membership** button unlocks
3. Click it to fill out the enrollment form on the **[Anvil Works app](https://natural-wavy-tank.anvil.app)**
4. Scroll down and click **Admin Login** to view the live members dashboard (Total Members, Active/Expired, Revenue, and full subscription table)

**Deployment status:** Live on PythonAnywhere and running continuously for over a month.

---

## Built By

**Krishna Karthik** 
[GitHub](https://github.com/krishnakarthik09) · [LinkedIn](https://linkedin.com/in/krishna-karthik-922b89301)
