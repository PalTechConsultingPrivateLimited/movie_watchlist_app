---
description: "Task list for Movie Watchlist feature"
---

# Tasks: Movie Watchlist

**Input**: Design documents from `specs/1-movie-watchlist/`
**Prerequisites**: `spec.md`, `plan.md`

## Phase 1: Setup (Project initialization)

- [ ] T001 [P] Initialize Angular workspace in `frontend/` (create project skeleton in `frontend/`)
- [ ] T002 [P] Initialize ASP.NET Core Web API project in `backend/` (create project skeleton in `backend/`)
- [ ] T003 [P] Create database folder and files: `database/schema.sql` and `database/seed.sql`
- [ ] T004 Create `specs/1-movie-watchlist/README.md` with quickstart and run instructions
- [ ] T005 [P] Add minimal `.gitignore` entries for `frontend/`, `backend/`, and `database/` (paths: repository root)

---

## Phase 2: Foundational (Blocking prerequisites)

- [ ] T006 Implement `Movie` entity class in `backend/src/Models/Movie.cs`
- [ ] T007 Implement `ApplicationDbContext` with `DbSet<Movie>` in `backend/src/Data/ApplicationDbContext.cs`
- [ ] T008 Configure EF Core migrations scaffold in `backend/` and add initial migration files (path: `backend/`)
- [ ] T009 Create `backend/src/Repositories/IMovieRepository.cs` and `backend/src/Repositories/MovieRepository.cs` (basic CRUD methods)
- [ ] T010 Create DTOs: `backend/src/Models/Dto/CreateMovieDto.cs` and `backend/src/Models/Dto/MovieDto.cs`
- [ ] T011 Add basic validation attributes to DTOs in `backend/src/Models/Dto/` (title required, year required)
- [ ] T012 Create `frontend/src/app/services/movie-api.service.ts` with placeholder methods for CRUD (paths under `frontend/`)
- [ ] T013 Add standard sample seed data rows to `database/seed.sql` (3 sample movies)

---

## Frontend Tasks (map to user stories)

### User Story 1 - Add Movie (US1) (Priority: P1)
- [ ] T014 [US1] Create `frontend/src/app/components/add-edit-movie/add-edit-movie.component.ts` (component file + template + stylesheet)
- [ ] T015 [US1] Implement add-movie form template in `frontend/src/app/components/add-edit-movie/add-edit-movie.component.html` (fields: title, year, genre, description)
- [ ] T016 [US1] Wire form submit to `movie-api.service.ts` create method in `frontend/src/app/services/movie-api.service.ts`
- [ ] T017 [US1] Add route `/add` to `frontend/src/app/app-routing.module.ts`
- [ ] T018 [US1] Add client-side validation messages in the component template (file path above)
- [ ] T019 [US1] Integration test: `frontend/tests/integration/add-movie.spec.ts` (end-to-end flow: open form, submit, see movie in list)

### User Story 2 - View & Edit Movie Details (US2) (Priority: P1)
- [ ] T020 [US2] Create `frontend/src/app/components/movie-details/movie-details.component.ts` + template
- [ ] T021 [US2] Add route `/movie/:id` to `frontend/src/app/app-routing.module.ts`
- [ ] T022 [US2] Implement edit flow in `add-edit-movie.component.ts` to load data for editing when `id` present
- [ ] T023 [US2] Add delete confirmation UI in `frontend/src/app/components/movie-details/movie-details.component.html`
- [ ] T024 [US2] Integration test: `frontend/tests/integration/view-edit-delete.spec.ts` (verify view, edit, delete flows)

### User Story 3 - Mark Watched & Rate (US3) (Priority: P1)
- [ ] T025 [US3] Create `frontend/src/app/components/rating/rating.component.ts` (reusable stars UI)
- [ ] T026 [US3] Add watched toggle control to `frontend/src/app/components/watchlist/watchlist.component.html`
- [ ] T027 [US3] Wire rating and watched actions to `movie-api.service.ts` update methods
- [ ] T028 [US3] Integration test: `frontend/tests/integration/watch-and-rate.spec.ts` (toggle watched, set rating, verify persistence)

### User Story 4 - Search & Filter (US4) (Priority: P2)
- [ ] T029 [US4] Implement `frontend/src/app/components/watchlist/watchlist.component.ts` with search box and filter controls
- [ ] T030 [US4] Add debounce on search input and call `movie-api.service.ts` with query param
- [ ] T031 [US4] Integration test: `frontend/tests/integration/search-filter.spec.ts` (search and filter behaviors)

---

## Backend Tasks (map to user stories)

### User Story 1 - Add Movie (US1) (Priority: P1)
- [ ] T032 [US1] Implement `backend/src/Controllers/MovieController.cs` POST `/api/movies` action
- [ ] T033 [US1] Implement `backend/src/Services/MovieService.cs` CreateMovie method
- [ ] T034 [US1] Implement `backend/src/Repositories/MovieRepository.cs` Add method for creating movies
- [ ] T035 [US1] Unit test: `backend/tests/unit/MovieService.CreateMovieTests.cs`
- [ ] T036 [US1] Integration test: `backend/tests/integration/MovieApi.AddMovie.cs` (POST /api/movies end-to-end)

### User Story 2 - View & Edit Movie Details (US2) (Priority: P1)
- [ ] T037 [US2] Implement `backend/src/Controllers/MovieController.cs` GET `/api/movies/{id}` and PUT `/api/movies/{id}` and DELETE `/api/movies/{id}` actions
- [ ] T038 [US2] Implement `backend/src/Services/MovieService.cs` methods for GetById, Update, Delete
- [ ] T039 [US2] Unit tests: `backend/tests/unit/MovieService.GetUpdateDeleteTests.cs`
- [ ] T040 [US2] Integration tests: `backend/tests/integration/MovieApi.ViewEditDelete.cs`

### User Story 3 - Mark Watched & Rate (US3) (Priority: P1)
- [ ] T041 [US3] Implement patch/update endpoints handling `watched` and `rating` in `MovieController.cs`
- [ ] T042 [US3] Implement service methods in `MovieService.cs` to apply watched/rating updates and validation (1–5 range)
- [ ] T043 [US3] Unit tests: `backend/tests/unit/MovieService.WatchAndRateTests.cs`
- [ ] T044 [US3] Integration tests: `backend/tests/integration/MovieApi.WatchAndRate.cs`

### User Story 4 - Search & Filter (US4) (Priority: P2)
- [ ] T045 [US4] Implement `GET /api/movies` with query params `q` and `watched` in `MovieController.cs`
- [ ] T046 [US4] Implement repository/search method in `MovieRepository.cs` with simple LIKE matching
- [ ] T047 [US4] Integration tests: `backend/tests/integration/MovieApi.SearchFilter.cs`

---

## Database Tasks

- [ ] T048 Create `database/schema.sql` with `CREATE TABLE Movies (...)` reflecting the data model
- [ ] T049 Create `database/seed.sql` with 3 sample movie INSERTs for local testing
- [ ] T050 Add migration SQL or EF migration notes in `backend/` (file: `backend/MIGRATION_README.md`)
- [ ] T051 Confirm connection string and local DB instructions in `specs/1-movie-watchlist/README.md`

---

## Final Phase: Polish & Cross-Cutting Concerns

- [ ] T052 [P] Add client-side form validation for all forms (file paths under `frontend/src/app/components`)
- [ ] T053 [P] Add server-side validation and friendly error responses in `backend/src/Controllers/MovieController.cs`
- [ ] T054 [P] Add basic logging to `backend/src/Services/MovieService.cs` for create/update/delete actions (file path)
- [ ] T055 [P] Add simple e2e smoke tests that run key flows end-to-end in `frontend/tests/e2e/smoke.spec.ts`
- [ ] T056 [ ] Update `specs/1-movie-watchlist/plan.md` with any deviations and mark completed tasks

---

## Dependencies & Execution Order

- Setup (Phase 1) tasks T001-T005: can run in parallel (P) where marked
- Foundational (Phase 2) tasks T006-T013: MUST be completed before most user stories
- User stories (T014-T031 frontend, T032-T047 backend): depend on foundational completion but independent across stories where possible
- Database tasks T048-T051: should be completed before integration tests

## Parallel Opportunities

- Frontend and Backend initialization (T001, T002) and DB seed creation (T003) can run in parallel
- Unit tests across different service classes are parallelizable
- Frontend component implementations for different stories can be parallel if they don't touch shared files

## Implementation Strategy

### MVP First
1. Complete Phase 1 and Phase 2 foundational tasks.
2. Implement User Story 1 end-to-end (T014-T017 frontend + T032-T034 backend + T048-T049 database).
3. Validate via integration tests (T036 + T019).
4. Iterate to add User Story 2 and 3, then search/filter (US4).

---

## Acceptance Checklist

- [ ] Backend CRUD endpoints implemented and tested (T032-T047)
- [ ] Frontend add/list/details/edit flows implemented and tested (T014-T031)
- [ ] Database schema and seed scripts created (T048-T049)
- [ ] Integration tests exercise core user journeys (T036, T040, T044)

*** End of tasks.md ***
