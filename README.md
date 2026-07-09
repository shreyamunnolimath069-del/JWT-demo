# JWT Auth Demo

A minimal full-stack example of authentication with JSON Web Tokens (JWT) — a React frontend paired with an Express/Node backend. Built to demonstrate the core flow: register → log in → access a protected route with a token.

## Features

- User registration with hashed passwords (bcrypt)
- Login that issues a signed JWT
- Protected `/profile` route that requires a valid token
- Simple React UI to register, log in, fetch the protected profile, and log out

## Tech Stack

**Frontend:** React, plain CSS
**Backend:** Node.js, Express, `jsonwebtoken`, `bcryptjs`, `cors`

## Project Structure

```
.
├── client/          # React app
│   ├── src/
│   │   ├── App.jsx
│   │   └── App.css
├── server/          # Express API
│   └── index.js
```

*(Adjust paths above to match your actual folder layout.)*

## Getting Started

### Prerequisites

- Node.js (v16+ recommended)
- npm

### 1. Clone the repo

```bash
git clone https://github.com/your-username/jwt-auth-demo.git
cd jwt-auth-demo
```

### 2. Set up the backend

```bash
cd server
npm install
node index.js
```

The API will run on `http://localhost:5000`.

### 3. Set up the frontend

In a separate terminal:

```bash
cd client
npm install
npm start
```

The React app will run on `http://localhost:3000` (or whichever port your setup uses).

## How It Works

1. **Register** — `POST /register` takes a username and password, hashes the password with bcrypt, and stores the user in memory.
2. **Log in** — `POST /login` verifies the credentials and returns a signed JWT (valid for 1 hour).
3. **Access protected route** — The client stores the token and sends it in the `Authorization: Bearer <token>` header when calling `GET /profile`.
4. **Verify** — A middleware function checks the token's validity before allowing the request through.

## API Endpoints

| Method | Route       | Auth Required | Description                          |
|--------|-------------|----------------|---------------------------------------|
| POST   | `/register` | No             | Create a new account                  |
| POST   | `/login`    | No             | Log in and receive a JWT              |
| GET    | `/profile`  | Yes (Bearer token) | Returns a welcome message for the logged-in user |

## Notes

- This is a **learning/demo project**. The "database" is an in-memory object that resets whenever the server restarts — don't use this in production as-is.
- The JWT secret is hardcoded for simplicity. In a real app, move it to an environment variable (e.g. via a `.env` file) and never commit it to source control.
- No refresh-token flow is implemented; tokens simply expire after 1 hour and the user must log in again.

## License

MIT — feel free to use this as a starting point for your own projects.
