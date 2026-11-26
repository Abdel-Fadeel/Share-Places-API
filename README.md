# Share Places API

REST API for **[Share Places](https://github.com/Abdel-Fadeel/Share-Places)**. Users sign up, then create, update and delete places with an image and an address that is turned into map coordinates automatically. Built with **Node.js, Express and TypeScript**, using **MongoDB (Mongoose)** with transactions, JWT auth and Cloudinary image uploads.

**Front end:** [Abdel-Fadeel/Share-Places](https://github.com/Abdel-Fadeel/Share-Places) · **Live app:** _coming soon_

## Features

- **Authentication.** Sign up with a profile image and log in. Passwords are hashed with bcrypt, and the JWT expires after 1 hour.
- **Places CRUD,** with only the owner allowed to update or delete.
- **Geocoding.** The address is converted to coordinates (geocode.xyz) when a place is created.
- **Image uploads** with Multer, stored on Cloudinary.
- **Mongoose transactions** keep users and places in sync when creating and deleting places.
- **Validation** with `express-validator`, plus a custom `HttpError` class and a global error handler.
- **Security.** Helmet and `express-mongo-sanitize`.

## API endpoints

Base URL: `/api/v1`

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/users` | List all users (without passwords) | – |
| POST | `/users/signup` | Sign up (multipart, with `image`) | – |
| POST | `/users/login` | Log in, returns `userId`, `email` and `token` | – |
| GET | `/places/:placeId` | Get a place | – |
| GET | `/places/user/:userId` | Get all places of a user | – |
| POST | `/places` | Create a place (multipart, with `image`) | Bearer token |
| PATCH | `/places/:placeId` | Update title and description | Bearer token (owner) |
| DELETE | `/places/:placeId` | Delete a place | Bearer token (owner) |

## Tech stack

| | |
|---|---|
| Runtime | Node.js, Express 4 |
| Language | TypeScript |
| Database | MongoDB Atlas + Mongoose (sessions and transactions) |
| Auth | JWT, bcryptjs |
| Uploads | Multer, Cloudinary |
| Validation | express-validator |
| Security | Helmet, express-mongo-sanitize, CORS |

## Getting started

```bash
git clone https://github.com/Abdel-Fadeel/Share-Places-API.git
cd Share-Places-API
npm install
cp .env.example .env   # then fill in your values
npm run dev
```

The server runs on `http://localhost:5000`. See [`.env.example`](.env.example) for the variables you need.

| Command | What it does |
|---|---|
| `npm run dev` | Compile in watch mode and restart on changes |
| `npm run build` | Compile TypeScript to `build/` |
| `npm start` | Run the compiled server |

## Project structure

```
app.ts            # Express app, middleware, routes, DB connection
routes/           # places, users
controllers/      # placesController, usersController
models/           # placeModel, userModel, HttpError
middleware/       # checkAuth (JWT), fileUpload (Multer)
utils/            # location (geocoding)
```

## Author

**Abdel-Fadeel Hamdy**, Front-End Engineer · [GitHub](https://github.com/Abdel-Fadeel)
