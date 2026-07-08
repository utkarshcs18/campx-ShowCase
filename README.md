# CampX

A private campus board where verified students can **ask for help** or **share what they have** — notes, gear, hostel extras, and everyday campus needs.

Only students on the college roster can join. There is no public feed and no posting to strangers.

---

## Why it exists

On campus, people often need something for a few hours: a calculator, a lab coat, notes, a charger. Asking in random groups is noisy and unsafe.

CampX keeps that exchange inside the college list. You sign in as a registered student, post what you need or what you can spare, and connect with a classmate.

---

## Features

- **Roster-only access** — Sign up with a PRN or college email that already exists on the student list.
- **OTP verification** — A one-time code is sent to the college email before an account is created.
- **Ask and Share posts** — Ask for something, or offer something others can borrow. Posts can be tagged as Study, Hostel, Tech, or Style.
- **Campus feed** — See open posts from classmates. Filter by Asks or Shares.
- **Requests** — Send a request on a post. The owner can accept or reject it.
- **WhatsApp handoff** — After a request is accepted, both students can continue on WhatsApp.
- **Activity and history** — Track incoming and outgoing requests, and review your own posts.
- **Account tools** — Password reset, profile view, help, and account deletion (with OTP and a 24-hour wait before signing up again).

---

## How it works

1. Open CampX and enter your **PRN** or **college email**.
2. If you are on the roster, verify with an **OTP**, then set a password.
3. On Home, browse the feed or create an **Ask** / **Share** post.
4. Another student sends a **request**.
5. You **accept** or **reject**. If accepted, you continue the handoff on WhatsApp.

---

## Tech stack

| Layer | Tools |
| --- | --- |
| Server | Node.js, Express |
| Database | MongoDB (Mongoose) |
| Auth | Sessions, bcrypt, email OTP (Nodemailer) |
| Frontend | HTML, CSS, vanilla JavaScript |

---

## Getting started

### What you need

- Node.js 18 or later
- MongoDB running locally, or a MongoDB Atlas URI
- SMTP credentials (for example a Gmail app password) to send OTP emails

### Setup

```bash
git clone <your-repo-url>
cd campx
npm install
```

Create a `.env` file in the project root:

```env
PORT=3000
SESSION_SECRET=replace-with-a-long-random-string
MONGODB_URI=mongodb://127.0.0.1:27017/campx
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-app-password
DEV_MODE=false
```

Generate a session secret:

```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### Student roster

CampX only allows students listed in `data/studentData.json`. That file is not committed (it can contain personal data). Create it locally:

```json
[
  {
    "prn": "1234567890",
    "name": "Student Name",
    "gender": "female",
    "email": "student@college.edu",
    "ph_number": "9876543210",
    "department": "CSE"
  }
]
```

### Run

```bash
npm start
```

Open [http://localhost:3000](http://localhost:3000).

Set `DEV_MODE=true` only on your machine if you need easier OTP testing. Keep it off for any shared or live environment.

---

## Project layout

```
campx/
├── index.js              # App entry
├── config/               # Database, session, mailer
├── controller/           # Auth, pages, and API logic
├── middleware/           # Login checks
├── model/                # MongoDB models and roster helpers
├── route/                # Page, auth, and API routes
├── data/                 # studentData.json (local only)
└── views/                # Landing, home, CSS, and JS
```

---

## Notes

- This is a student sharing space, not an official college portal.
- Profile details (name, PRN, department, phone) come from the roster file, not from in-app editing.
- Do not commit `.env` or `data/studentData.json`.

---

## License

ISC
