# 🎬 TMDB API Testing – Postman & Newman

API testing project for [The Movie Database (TMDB) API](https://developer.themoviedb.org/docs). The goal was to verify that the API behaves correctly and reliably across the main user scenarios, by validating not only status codes but also response structure, required fields, and data accuracy.

## 📊 Results at a glance

| Metric | Value |
|---|---|
| Requests | 12 |
| Assertions | 53 |
| Automated test scripts | 24 |
| Real issue found | 1 (`Now Playing` date range) |

## 🧪 Scenarios covered

- Authentication setup and verification (Bearer token)
- Search movies by keyword
- Search TV shows by name
- Movie details & credits
- Person (actor/director) details
- Discover movies by genre & get the genre list
- Popular movies & Now Playing movies
- TV show details
- Add a movie to the watchlist (**POST**)

## ✅ What each test validates

- **Status codes** (e.g. 200 for success, 401 for invalid auth)
- **Response structure** (expected keys and data types)
- **Required fields** (present and not empty)
- **Data accuracy** (values match the request, e.g. date ranges, genre IDs, pagination)

## 🐞 Finding: `Now Playing` date range inconsistency

The `Now Playing` endpoint returned data outside the expected date range.

- **Expected:** `<expected date range>`
- **Actual:** `<what was returned>`
- **Test that caught it:** `<name of the test script>`

> Status code was 200, so the issue would have been missed without validating the data itself.

## 🛠️ Tools

- **Postman** – building requests, authentication, environment variables, test scripts
- **Newman** – running the collection from the command line and generating HTML reports
- **TMDB public API** – system under test

## 📁 Project structure

```
├── collection/
│   └── TMDB.postman_collection.json
├── environment/
│   └── TMDB.postman_environment.json   # no real token inside
├── reports/
│   └── report.html                     # Newman HTML report
└── README.md
```

## ▶️ How to run

1. Install [Node.js](https://nodejs.org/), then install Newman and the HTML reporter:

   ```bash
   npm install -g newman newman-reporter-htmlextra
   ```

2. Get a TMDB API token from your TMDB account settings.
3. Open the environment file and set your token (do **not** commit your real token):

   ```
   token = <your TMDB Bearer token>
   ```

4. Run the collection:

   ```bash
   newman run collection/TMDB.postman_collection.json \
     -e environment/TMDB.postman_environment.json \
     -r cli,htmlextra \
     --reporter-htmlextra-export reports/report.html
   ```

5. Open `reports/report.html` in your browser.

## 📚 What I learned

- Designing and organizing a structured Postman collection from scratch
- Setting up Bearer-token authentication and managing environment variables
- Working with both GET and POST requests
- Writing assertions that validate data, not just status codes
- Handling dynamic data such as date ranges and pagination
- Running a full collection with Newman and reading automated reports
- Thinking about API testing end to end: from searching for data to performing real actions on it
