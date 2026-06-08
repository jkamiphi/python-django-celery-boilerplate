# DRF Setup Onboarding

## Task

Configure Django REST Framework for the Django 6.0 boilerplate without adding example API apps,
serializers, viewsets, or endpoints beyond auth and documentation.

## User Decisions

- Authentication: JWT using `djangorestframework-simplejwt` with access and refresh tokens.
- Documentation: `drf-spectacular` for OpenAPI 3 schema, Swagger UI, and Redoc.
- Scope: installation and configuration only.

## Current Project State

- Stack: Django 6.0, PostgreSQL-compatible settings via `dj-database-url`, HTMX.
- Package manager: `uv`.
- `apps/` is empty except for `__init__.py`.
- `config/urls.py` currently exposes only `admin/`.
- `config/settings.py` uses `os.getenv()` and `dotenv.load_dotenv()`.
- Existing third-party apps are `django_extensions` and `django_htmx`.
- Existing dependency declarations live in `pyproject.toml`; lock file is `uv.lock`.

## Planned Changes

- Add dependencies:
  - `djangorestframework`
  - `djangorestframework-simplejwt`
  - `drf-spectacular`
- Add installed apps:
  - `rest_framework`
  - `rest_framework_simplejwt`
  - `rest_framework_simplejwt.token_blacklist`
  - `drf_spectacular`
- Add DRF defaults:
  - JWT authentication first
  - session authentication as a secondary development/browser support mechanism
  - authenticated-by-default permissions
  - drf-spectacular schema class
  - page-number pagination with page size 20
- Add Simple JWT settings:
  - `JWT_ACCESS_MINUTES`, default `60`
  - `JWT_REFRESH_DAYS`, default `7`
  - refresh rotation enabled
  - blacklist after rotation enabled
- Add drf-spectacular settings:
  - title `API`
  - description `API documentation`
  - version `1.0.0`
  - do not include schema in served docs UI
- Add URLs:
  - `api/token/`
  - `api/token/refresh/`
  - `api/schema/`
  - `api/docs/`
  - `api/redoc/`

## Verification

- Run migrations for `token_blacklist`.
- Run `uv run python manage.py check`.
- Run `uv run python manage.py spectacular --file /tmp/schema.yml`.
- Run quality checks:
  - `uv run ruff check .`
  - `uv run ruff format --check .`
  - `uv run pyright`
