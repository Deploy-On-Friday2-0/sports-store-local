# Sports Store Local Environment

Docker Compose environment for running the complete Sports Store platform locally.

## Scope

- `docker-compose.yml`: MongoDB, Redis, frontend, gateway, and backend orchestration
- `seed/init-mongo.js`: First-start development data
- `.env.example`: Safe local configuration template

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) with Compose v2 (`docker compose version`)
- Git
- GitHub access to the `Deploy-On-Friday2-0` org

## Setup

1. Clone this repository and every service repo as **siblings** in the same parent directory:

   ```bash
   mkdir sports-store && cd sports-store
   for repo in local frontend gateway auth-service catalog-service cart-service order-service payment-service; do
     git clone "https://github.com/Deploy-On-Friday2-0/sports-store-$repo.git"
   done
   ```

   You should end up with `sports-store-local/`, `sports-store-frontend/`, `sports-store-gateway/`, and the five `sports-store-*-service/` repos all side by side (this compose file builds each service with `build: ../sports-store-<name>`).

2. From `sports-store-local/`:

   ```bash
   cp .env.example .env
   docker compose up --build -d
   ```

3. Open **http://localhost** — the gateway is the only container that publishes a host port; everything else is reached over the internal `sports-store-net` network.

Check status/logs with `docker compose ps` and `docker compose logs -f <service>`. Stop everything with `docker compose down` (add `-v` to also drop the Mongo volume and reseed next start).

## PR Diff Review Runner

The provider-independent pipeline and trusted post-CI GitHub Actions integration are documented in [`review_runner/README.md`](review_runner/README.md). Local use accepts a supplied unified patch and uses the mock provider. In GitHub, the trusted workflow retrieves Pull Request diffs as data and invokes OpenRouter only after branch-name, Compose configuration, and secret-scanning checks succeed.
