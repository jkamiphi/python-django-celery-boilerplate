# Python Django Celery Boilerplate

A minimal Django 6 boilerplate with Python 3.12, modern quality tooling, and initial structure for Celery-based background tasks.

## Stack

- Python 3.12+
- Django 6
- PostgreSQL or SQLite (via `dj-database-url`)
- Celery + Redis dependencies included
- Tooling: `uv`, `pytest`, `ruff`, `pyright`

## Prerequisites

- Python 3.12
- [uv](https://docs.astral.sh/uv/)

## Getting Started

1. Install dependencies:

   ```bash
   uv sync
   ```

2. Run database migrations:

   ```bash
   uv run python manage.py migrate
   ```

3. Start the development server:

   ```bash
   uv run python manage.py runserver
   ```

4. Open Django admin at:

   ```text
   http://127.0.0.1:8000/admin/
   ```

## Environment Variables

Configuration is loaded from environment variables (and `.env` if present). Common variables:

- `SECRET_KEY`
- `DEBUG`
- `ALLOWED_HOSTS`
- `DATABASE_URL`

If `DATABASE_URL` is not set, SQLite is used by default.

## Quality Checks

- Lint:

  ```bash
  uv run ruff check .
  ```

- Format:

  ```bash
  uv run ruff format .
  ```

- Type check:

  ```bash
  uv run pyright
  ```

- Tests:

  ```bash
  uv run pytest
  ```

## Project Structure

- `apps/` — Django apps
- `config/` — Django settings and URL configuration
- `tasks/` — task package placeholder for background jobs
- `tests/` — test package
- `ai-specs/` — AI skills/specs for project workflows

## Notes

- Celery and Redis dependencies are included in `pyproject.toml`.
- Add your Celery app configuration when implementing background workers.
