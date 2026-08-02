# Sports Store Local Environment

Docker Compose environment for running the complete Sports Store platform locally.

## Scope

- `docker-compose.yml`: MongoDB, frontend, gateway, and backend orchestration
- `seed/init-mongo.js`: First-start development data
- `.env.example`: Safe local configuration template

Clone the component repositories as siblings of this repository. The Compose starter still contains TODO markers and monorepo-relative examples that must be updated during the containerization milestone.

## Intended Usage

```bash
cp .env.example .env
docker compose up --build -d
```

Only the gateway should publish a host port.

## PR Diff Review Runner

The provider-independent pipeline and trusted post-CI GitHub Actions integration are documented in [`review_runner/README.md`](review_runner/README.md). Local use accepts a supplied unified patch and uses the mock provider. In GitHub, the trusted workflow retrieves Pull Request diffs as data and invokes OpenRouter only after branch-name, Compose configuration, and secret-scanning checks succeed.
