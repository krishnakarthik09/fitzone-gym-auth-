# FitZone Gym Website

A full-stack gym membership website built with Flask — featuring a dynamic 3D landing page, complete user authentication system, and membership plan gating. Live and deployed on PythonAnywhere.

🔗 **Live Site: [krishnakarthik09.pythonanywhere.com](https://krishnakarthik09.pythonanywhere.com)**

---

## What It Does

- Visitors can browse the gym, view programs, and see membership plans
- **Login / Sign Up** buttons in the nav let users create an account or log in
- Plan buttons (Starter, Pro, Elite) and the "Get Membership" CTA are **gated** — clicking them redirects unauthenticated users to sign up first
- Once logged in, the nav updates to show the user's name and a Logout button, and all membership buttons unlock and point to the FitZone membership app
- Logout clears the session and returns the user to the home page

---

## Features

- Full user authentication — signup, login, logout
- Passwords hashed using `werkzeug.security` — never stored as plain text
- Session management via Flask-Login — server remembers logged-in users across requests
- SQLite database storing user accounts (via Flask-SQLAlchemy)
- Duplicate username detection on signup with user-friendly error messages
- Route protection — membership links hidden until authenticated
- 3D rotating dumbbell built with Three.js (drag to rotate)
- Fully responsive dark neon design — matches FitZone brand identity

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Python 3, Flask |
| Database | SQLite via Flask-SQLAlchemy |
| Auth | Flask-Login, Werkzeug password hashing |
| Frontend | HTML, CSS, Jinja2 templates |
| 3D Graphics | Three.js (r128) |
| Hosting | PythonAnywhere |

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

## Auth Flow

```
Visitor lands on /
    ↓
Clicks "Join Now" or any plan button
    ↓
Redirected to /signup → username + password → hashed + saved to gym.db
    ↓
Redirected to /login → credentials checked against hash
    ↓
login_user() creates session cookie
    ↓
Back to / — nav shows username + Logout, membership buttons unlocked
    ↓
/logout → session cleared → back to /
```

---

## Running Locally

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

---

## Security Notes

- Passwords are never stored in plain text — only a `werkzeug` bcrypt-style hash is saved
- The `SECRET_KEY` in `app.py` should be replaced with a long random string before production use
- `gym.db` is excluded from the repo via `.gitignore` to avoid exposing user data
- Flask-Login session cookies are cryptographically signed using the secret key

---

## Live Demo

Visit **[krishnakarthik09.pythonanywhere.com](https://krishnakarthik09.pythonanywhere.com)**, create an account, and see the membership buttons unlock after login.

---

## Built By

**Krishna Karthik** — ECE Graduate, Hyderabad  
[GitHub](https://github.com/krishnakarthik09) · [LinkedIn](https://linkedin.com/in/krishna-karthik-922b89301)
