# Test Renovate

## Self-Hosting Examples
* See: https://docs.renovatebot.com/examples/self-hosting/

- Install:

  ```
  npm install renovate
  npm install yarn pnpm
  ```

## Run renovate locally

### 1. Run locally and output a report locally
Run renovate locally in dry-run mode to see what it would do without affecting the remote repository.

- Command:

  ```bash
  npm run renovate:local
  ```
  *(or manually: `set -a; . ./.env; set +a; LOG_LEVEL=debug npx renovate --platform=local --dry-run=full`)*

  > **Note**: To save the output report to a file, you can run:
  > `npm run renovate:local > renovate-report.log 2>&1`

### 2. Run locally and update the Renovate dashboard on GitHub
Run renovate locally but execute against the GitHub repository to create/update PRs and the Dependency Dashboard. You need to provide your personal GitHub token in a `.env` file.

**Setup your GitHub Token:**
1. Go to [GitHub Tokens settings](https://github.com/settings/tokens/new?scopes=repo,read:org,user:email&description=Renovate+Local).
2. Generate a new Personal Access Token (classic) with `repo`, `read:org`, and `user:email` scopes.
3. Copy the `.env.example` file to `.env`:
   ```bash
   cp .env.example .env
   ```
4. Edit the `.env` file and replace `your_github_token_here` with your generated token.

- Command:

  ```bash
  npm run renovate:github
  ```
  *(or manually: `set -a; . ./.env; set +a; LOG_LEVEL=debug npx renovate`)*