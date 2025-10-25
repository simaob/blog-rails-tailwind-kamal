# Repository Guidelines

## Project Structure & Module Organization
Source lives under `app/` following Rails conventions: controllers, models, Turbo-enabled views, and Stimulus controllers in `app/javascript`. Tailwind styles compile from `app/assets/stylesheets/application.tailwind.css`. Tests sit in `test/`, split into unit, integration, and system suites. Configuration (database, Kamal, queues) resides in `config/`, with deployment settings in `config/deploy.yml`. Database migrations are defined in `db/migrate/`. Static assets and compiled files flow through `public/` and `storage/`; avoid committing generated content from these paths.

## Build, Test, and Development Commands
Run `bin/setup` once to install gems, set up the database, and pull front-end dependencies. For local development, `bin/dev` (Procfile-backed) starts the Rails server and Tailwind watcher concurrently. Execute `bin/rails test` for the full Minitest suite, `bin/rails test system` for browser-driven checks, and `bin/rails test TEST=test/controllers/posts_controller_test.rb` to target a single file. Use `bundle exec rubocop` before opening a PR to catch style issues. Security scanners `bin/brakeman` and `bin/bundler-audit` are available when touching dependencies or authentication logic.

## Coding Style & Naming Conventions
Follow Ruby’s standard two-space indentation and snake_case for files, classes, and methods; use CamelCase only for class names. Prefer intent-revealing partials and helpers over in-view logic. JavaScript modules should mirror Stimulus controller naming (`example_controller.js`). Tailwind utility extractions belong in `app/assets/stylesheets/components/` when patterns repeat. Let RuboCop’s omakase rules guide formatting tweaks.

## Testing Guidelines
Write new unit tests alongside models and controllers, mirroring existing naming (`*_test.rb`). System tests under `test/system/` should describe the user interaction being covered, e.g., `visits_blog_test.rb`. Keep fixtures minimal and prefer factories within tests when setup complexity grows. Ensure `bin/rails test` passes locally before pushing, and add regression coverage whenever you fix a bug.

## Commit & Pull Request Guidelines
Adopt short, imperative commit messages (`Add post teaser component`). Group related changes; avoid mixing refactors with functional updates. For pull requests, include: 1) a concise summary of intent, 2) screenshots or recordings for UI changes, and 3) a test plan listing commands run (e.g., `bin/rails test`). Link back to issues or discussions when available, and call out deployment impacts (migrations, Kamal config adjustments) explicitly.

## Deployment & Operations
Kamal configuration in `config/deploy.yml` drives container releases. Validate changes with `bin/kamal verify` in staging before production deploys. When migrations are involved, note them in the PR and ensure `bin/rails db:migrate` succeeds locally. Keep secrets out of version control; use `bin/rails credentials:edit` to update encrypted credentials and share through the team’s secure channel.
