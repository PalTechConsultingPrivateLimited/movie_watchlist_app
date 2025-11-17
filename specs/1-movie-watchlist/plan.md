# Implementation Plan: Movie Watchlist

**Branch**: `1-movie-watchlist` | **Date**: 2025-11-17 | **Spec**: ../1-movie-watchlist/spec.md

## Summary
Build a simple, beginner-friendly Movie Watchlist application that lets a single
user add movies to a personal list, mark them watched/unwatched, rate them,
search and filter the list, and view/edit/delete movie details. Keep the UI
clean and the app fast and easy to navigate.

## High-level Architecture

- Single-page Frontend (Angular 18) communicating with a Backend API
  (ASP.NET Core 8). The backend persists data to SQL Server via EF Core.
- The app is single-user (local or single account), lightweight, and intended
  for learning and quick iteration.

Architecture (textual):

```
[Browser / Angular SPA] <---- HTTP JSON ----> [ASP.NET Core Web API]
                                    |
                                    +--> EF Core DbContext --> SQL Server (database/)
```

## Folder Structure (root-level)

- `frontend/`  — Angular project (components, modules, services, assets)
- `backend/`   — ASP.NET Core Web API (Controllers, Services, Repositories, Data)
- `database/`  — SQL scripts: schema + seed data

Example minimal tree:

```
frontend/
  src/
    app/
      components/
      modules/
      services/
backend/
  src/
    Controllers/
    Services/
    Repositories/
    Data/
    Models/
database/
  schema.sql
  seed.sql
```

## Backend Structure (ASP.NET Core 8)

Keep the backend simple and layered so beginners can follow.

- Controllers: HTTP endpoints mapped to feature actions (MovieController)
  - Responsible for request/response mapping and returning appropriate status codes.
- Services: Business logic (MovieService)
  - Handles operations like add, update, mark watched, rating rules, search.
- Repositories: Data access via EF Core (MovieRepository)
  - Simple CRUD methods, abstract DbContext so services don't talk to EF directly.
- Data / Models:
  - `Movie` entity class and DTOs for requests/responses (e.g., MovieDto, CreateMovieDto).
- DbContext & Migrations:
  - `ApplicationDbContext` with `Movies` DbSet.

Notes for beginners:
- Keep methods small and focused.
- Validate inputs in controllers or service layer and return helpful errors.

## Frontend Structure (Angular 18)

Organize the Angular app into logical modules and components.

- Modules
  - `AppModule` (root)
  - `MoviesModule` (watchlist feature)
  - `SharedModule` (reusable components like buttons, rating display)
- Components
  - `WatchlistComponent` — shows list of movies, search and filter controls
  - `MovieDetailsComponent` — shows full details with edit/delete options
  - `AddEditMovieComponent` — form for create/edit
  - `RatingComponent` — star rating UI (reusable)
  - `EmptyStateComponent` — shown when list is empty
- Services
  - `MovieApiService` — interacts with backend endpoints
  - `UiService` (optional) — for notifications/snackbars and shared UI state
- Routing
  - `''` → Watchlist, `/movie/:id` → Movie details, `/add` `/edit/:id` for forms

Frontend notes for beginners:
- Keep components focused and pass data via inputs/outputs or service observables.
- Keep styling minimal and consistent.

## Data Model

- Movie
  - `Id` (GUID or int)
  - `Title` (string, required)
  - `Year` (int, required)
  - `Genre` (string, optional)
  - `Description` (string, optional)
  - `Watched` (bool, default false)
  - `Rating` (int? 1–5, nullable)
  - `CreatedAt` (datetime)
  - `UpdatedAt` (datetime)

SQL table (conceptual): `Movies(Id, Title, Year, Genre, Description, Watched, Rating, CreatedAt, UpdatedAt)`

## API Endpoints (HTTP JSON)

- `GET /api/movies`
  - Query params: `q` (search string), `watched` (true|false|omit), `page`, `pageSize`
  - Returns list of movies matching search/filter
- `GET /api/movies/{id}`
  - Returns movie details
- `POST /api/movies`
  - Body: create movie payload (title, year, genre, description)
  - Creates movie and returns created resource
- `PUT /api/movies/{id}`
  - Body: update payload (title, year, genre, description, rating, watched)
  - Updates movie
- `PATCH /api/movies/{id}/watched`
  - Body: `{ "watched": true|false }` to toggle watched status (optional; PUT can cover)
- `PATCH /api/movies/{id}/rating`
  - Body: `{ "rating": 1..5 }` to set rating (optional; PUT can cover)
- `DELETE /api/movies/{id}`
  - Deletes movie

Notes:
- Keep endpoints predictable and RESTful. For a simple app PUT can be used instead of PATCH.
- Return standard HTTP status codes (200, 201, 400, 404, etc.).

## Database (database/)

- `schema.sql` — CREATE TABLE `Movies` with columns mapping to the data model.
- `seed.sql` — optional small set of sample movies for local testing (3–5 rows).

Keep scripts small and documented so beginners can run them locally.

## Development Milestones (Beginner-friendly)

1. Project Setup (1–2 days)
   - Initialize `frontend/` with an Angular workspace skeleton.
   - Initialize `backend/` with ASP.NET Core Web API project and EF Core setup.
   - Add `database/schema.sql` and `seed.sql`.
2. Backend: Basic CRUD (2–3 days)
   - Implement `Movie` entity, `ApplicationDbContext`, repository, and controller endpoints for CRUD.
   - Add simple validation and seed data.
3. Frontend: Watchlist UI (2–3 days)
   - Implement `WatchlistComponent` to list movies and call API.
   - Add `AddEditMovieComponent` form and wiring to create movies.
4. Frontend: Details, Edit, Delete (1–2 days)
   - Implement `MovieDetailsComponent`, edit flow, and delete confirmation.
5. Search, Filter, Mark Watched & Rating (1–2 days)
   - Add search box, filter controls, and rating/watched actions in UI.
6. Polish & Usability (1–2 days)
   - Improve layout, add empty states, UX tweaks, and basic client-side validation.
7. QA & Local Testing (1 day)
   - Run through acceptance scenarios and fix issues.

Estimate total: 8–13 days for a single beginner developer to produce a solid MVP.

## Acceptance Checklist (for this plan)

- [ ] Backend returns movies and handles CRUD operations
- [ ] Frontend shows list, add/edit/delete flows working end-to-end
- [ ] Search and filter behave as expected
- [ ] Watched toggle and rating persist and display correctly
- [ ] Database scripts create schema and seed sample data

## Tips for Beginners

- Start small: implement a single flow end-to-end first (add → list → details).
- Keep commits small and focused with clear messages.
- Use the API from the browser (Postman or the browser devtools network tab) to
  debug before wiring the UI.
- Keep styles simple and consistent; prefer readability over fancy designs.

---

If you want, I can now:
- create the plan file in the repo (done),
- initialize minimal Angular / ASP.NET projects (I can scaffold files), or
- create initial `schema.sql` and `seed.sql` under `database/`.

Which of those should I do next?