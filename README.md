# Secrets App – Authentication with Local & Google OAuth

A secure Node.js authentication system that allows users to sign up/login using a local email-password method or Google OAuth 2.0. Authenticated users can submit and view a personal "secret" stored in a PostgreSQL database.

## Features
- User registration & login with hashed passwords (bcrypt)
- Google OAuth 2.0 login (Sign in with Google)
- Session-based authentication using Passport.js
- Protected routes — only logged-in users can access `/secrets` and `/submit`
- Submit and view personal secrets stored in PostgreSQL

## Tech Stack
- **Backend:** Node.js, Express.js
- **Authentication:** Passport.js (Local Strategy + Google OAuth2 Strategy)
- **Database:** PostgreSQL
- **Frontend:** EJS templating, CSS
- **Security:** bcrypt (password hashing), express-session

## Project Structure
├── views/
│   ├── home.ejs
│   ├── login.ejs
│   ├── register.ejs
│   ├── submit.ejs
│   └── secrets.ejs
├── public/
├── index.js
├── .env
└── package.json


## Prerequisites
- Node.js installed
- PostgreSQL database running
- Google Cloud Console project with OAuth 2.0 credentials

## Installation

1. Clone the repository
```bash
git clone https://github.com/your-username/repo-name.git
cd repo-name
```

2. Install dependencies
```bash
npm install
```

3. Create a `.env` file in the root directory
PG_USER=your_postgres_user
PG_HOST=localhost
PG_DATABASE=your_database_name
PG_PASSWORD=your_postgres_password
PG_PORT=5432
SESSION_SECRET=your_session_secret
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

5. Set up the database table
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(100) NOT NULL,
  secret TEXT
);
```

5. Run the app
```bash
node index.js
```
App will run at `http://localhost:3000`

## Google OAuth Setup
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create OAuth 2.0 credentials
3. Add `http://localhost:3000/auth/google/secrets` as an Authorized redirect URI
4. Copy Client ID & Client Secret into your `.env` file

## Routes
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | Home page |
| GET | `/login` | Login page |
| GET | `/register` | Register page |
| POST | `/register` | Create new user |
| POST | `/login` | Local login |
| GET | `/auth/google` | Google login redirect |
| GET | `/auth/google/secrets` | Google OAuth callback |
| GET | `/secrets` | View secret (protected) |
| GET | `/submit` | Submit secret form (protected) |
| POST | `/submit` | Save secret to DB |
| GET | `/logout` | Logout user |

## Author
Rahul Pawar — [GitHub](https://github.com/rahulpawar-o7)
