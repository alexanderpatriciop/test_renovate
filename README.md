# Test Renovate

Modifying readme only for test.

## Self-Hosting Examples
* See: https://docs.renovatebot.com/examples/self-hosting/

- Install:

  ```
  npm install renovate
  npm install yarn pnpm
  ```

## Run renovate

- Command to get the updates:

	```
	LOG_LEVEL=debug npx renovate --platform=local --repository-cache=reset
    ```

- To created the Dashboard and PRs:

Add ```config.js``` file with the following settings:
  ```
module.exports = {
  endpoint: 'https://api.github.com/',
  token: '**TOKEN**',
  platform: 'github',
  onboardingConfig: {
    extends: ['config:recommended'],
  },
  repositories: ['REPOSIROTY'],
  repository-cache: reset
};
  ```
And run the command:
  ```
  LOG_LEVEL=debug npx renovate
  ```