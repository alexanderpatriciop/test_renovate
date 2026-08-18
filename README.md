# Test Renovate

## Self-Hosting Examples
* See: https://docs.renovatebot.com/examples/self-hosting/

- Install:

  First, ensure you are running the correct Node.js version (Node 24+ is required by the latest Renovate). If you use `nvm`, you can load it by running:
  ```bash
  nvm install
  nvm use
  ```

  Then install the dependencies:
  ```bash
  npm install
  npm install -g yarn pnpm
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

## Resetting Renovate State (Troubleshooting)

If Renovate creates a PR that you did not want, simply closing it is not enough. Renovate will remember the closed PR, assume you rejected the update, and place it under the "Ignored or Blocked" section of the Dependency Dashboard. 

To completely wipe Renovate's memory of a PR so you can re-test your configuration freshly (e.g., to have it show up as an unchecked box on the dashboard again), follow these steps:

1. **Close the PR** on GitHub.
2. **Delete the branch** that Renovate created (e.g., `renovate/drupal-core-10.x`).
3. **Rename the closed PR title**: Add a prefix like `[CLOSED]` or `[ABANDONED]` to the beginning of the title.
   *Example:* Change `Update dependency drupal/core to v10.6.13` ➡️ `[CLOSED] Update dependency drupal/core to v10.6.13`.

*Why it works: Renovate searches past PRs using the exact PR title. By changing the title on GitHub, Renovate fails to find it in its history and will treat the update as completely new the next time you run `npm run renovate:github`.*