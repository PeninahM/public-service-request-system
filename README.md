# Public Service Request System

A mini eCitizen-style web app where citizens report public service issues
(broken streetlights, water problems, garbage collection) and county staff
track and resolve them.

**Live demo:** https://public-service-request-system-eight.vercel.app
**Repository:** https://github.com/PeninahM/public-service-request-system

## Features

- Citizen registration and login
- Submit a request (category, location, description)
- Citizens see only their own requests and their status
- Admin dashboard listing all requests
- Status tracking: Pending → In Progress → Resolved
- Basic analytics: total, open and resolved case counts
- Role-based access: admins and citizens are separated

## Tech stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend:** Supabase (Postgres database, authentication)
- **Security:** Row Level Security (RLS) policies on all tables
- **Hosting:** Vercel (auto-deploys from GitHub)

## Project structure

| File | Purpose |
|---|---|
| `index.html` | Register and login page |
| `dashboard.html` | Citizen page: submit and view own requests |
| `admin.html` | Admin page: all requests, status changes, analytics |
| `config.js` | Supabase connection (publishable key only) |

## Database

- `requests`: id, created_at, user_id, category, location, description, image_url, status
- `profiles`: id (linked to auth user), role (`citizen` or `admin`)

RLS rules: citizens can insert and read only their own requests; admins
(checked with an `is_admin()` function) can read and update all requests.

## Running locally

1. Clone the repo.
2. Open `config.js` and set your Supabase project URL and publishable key.
3. Open `index.html` in a browser (or use any static server).

## Creating an admin

Register normally, then in the Supabase SQL editor run:

    update profiles set role = 'admin' where id = (select id from auth.users where email = 'you@example.com');# public-service-request-system
Citizens submitting service requests
