# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) (or [oxc](https://oxc.rs) when used in [rolldown-vite](https://vite.dev/guide/rolldown)) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## React Compiler

The React Compiler is enabled on this template. See [this documentation](https://react.dev/learn/react-compiler) for more information.

Note: This will impact Vite dev & build performances.

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default defineConfig([
  # Ephemeral Preview Workflows (GitHub Actions)

  This repository contains GitHub Actions that create and destroy ephemeral preview static-site services on Render for pull requests.

  **Purpose**
  - Automate spin-up of a preview static site per PR and teardown when the PR closes.

  **Primary workflow files**
  - `./.github/workflows/create_preview_env.yml`: creates or updates a Render static-site service for the PR, captures `service-id` and `service-url`, and uploads them as artifacts.
  - `./.github/workflows/destory_preview_env.yml`: (destroy) downloads the artifact or queries Render by service name to delete the preview service when the PR is closed.

  **Highlights**
  - **Create-or-update**: detects existing service by name and `PATCH`es it, otherwise `POST` to create a new service.
  - **Artifacts**: uploads `service-id.txt` and `service-url.txt` so downstream jobs can consume them.
  - **Robust API handling**: curl responses include HTTP status + body capture, `--noproxy` and retry handling, and jq is used for JSON parsing.
  - **Fallbacks**: destroy job will query Render for a service matching the PR naming convention when artifacts are not available.
  - **PR communication**: workflows attempt to publish the preview URL to the PR (with cleanup of previous bot comments); fallbacks exist for permission-limited contexts (e.g., forked PRs) such as job summaries and logs.

  **Required secrets / repo vars**
  - `RENDER_API_KEY` — Render API key used to call the Render REST API.
  - `RENDER_ENV_ID` or `RENDER_PROJECT_ID` / `RENDER_OWNER_ID` — depending on whether environments are created or an environment ID is provided.
  - `GITHUB_TOKEN` — used for PR comments; note: `GITHUB_TOKEN` has limitations for forked PRs so some comment actions may fall back to job summaries.

  **Service naming / defaults**
  - Default publish directory: `./dist` (adjustable in the workflow if your build outputs elsewhere).
  - Service name pattern used in the workflows: `wa-test-pr-${{ github.event.pull_request.number }}-static`.

  **Notes**
  - Artifacts are convenient but not guaranteed across all workflow runs; the workflows include API fallbacks to locate and remove preview services.
  - If you want me to commit these workflows, run them, or further DRY/refactor the scripts (extract curl helpers), tell me which approach you prefer.

  --
  Workflow-focused README added by automation helper.
export default defineConfig([
