

## Git and GitHub Behavior
- Don't bother making PRs for git development branches
- Always work off of a development branch, don't start new work off of 'main' or a production branch
- Always make PRs for main and important branches you come across (beta, preprod)
- Always run regression tests as a precommit before pushing large amounts of changes. Make precommit rules to help yourself
- If we have a code linter set up, use it on large commits

## Velocity
- When prototyping new features, fail fast and plan for failures, if you are making a network test to an API or resource make sure the app isn't in the middle of a build before trying, double check  app is up
- Try and look around the corner to predict what configurations are not scalable. Always build for scale.
- If a process, script, or action is long running (15s+), ask me about what to do. Sometimes a workflow is getting stuck in a silent loop.

## Credential Handling
- Never transmit a credential in plaintext
- Never use query parameters to pass secrets

## Scripts
- Prefer idempontency over non-idempotentcy when building scripts and automations, this way if something is accidentally ran multiple times its typically safe to assume nothing unexpected will change because the script was designed to be ran multiple times in a safe manner

## Network, Deployments, and Errors
- Do not expose ports or API endpoints to the public internet unless you have thoroughly discussed this with me
- Utilize the template method pattern when building an API client for network resources, this is because we want a consistent and reliable mechanism for making network requests for data that provides us with exponential back off and configurable retries
- Build and make API requests in a reliable and 
- Never hardcode URLs or Ports in code, utilize variables and config files
- If you finish a large feature or feat, provide a URL so I can view it if possible
- Build a /health resource on every endpoint that is served over HTTP or HTTPS
- Build and use smoke tests after deployments. Smoke tests should ensure that the /health resource is available
- Do not wait for a response from a network resource for more than 2 seconds. Ask me and notify me if something you need on the network is not responding to your request within 2 seconds, don't silently move on
- Make error messages actionable, don't leave the user confused
- After making a large amount of changes or finishing a feat ask me if I want to rebuild the application and run all regression tests to verify code stability
- Simulate and test changes locally as much as possible before we deploy to a remote host

## Configs
- Utilize a 'config' folder inside an app for app specific config settings
- Utilize the repo level 'config' folder for global config settings that applies across all apps
- Utilize .env.development for development purposes
- Utilize .env file for production that is never let the .env file commit  to the repo

## Testing
- Use a tests/ folder per app to hold any tests you make for that app
- Unit: Vitest, no I/O, colocated in tests/unit/
- Integration: Vitest, real Postgres via docker-compose, tests/integration/
- E2E: Playwright at 1280px AND 390px viewports
- Mock ALL external services (Twilio, Stripe, Google Solar, Maps). Never call real APIs unless I tell you to.
- Auth in tests: generateTestJWT() from packages/shared/src/test/jwt.ts
- Utilize request tracing if a request is going to pass through multiple systems
- SQS messages must include correlationId (from original requestId) for cross-service tracing
- Utilize TDD, test driven development with everything you can
- Build E2E tests and regression tests for everything you can
- Before making a commit & push, run all regression tests

## Web Styling and Accessibility
- Utilize tailwinds, build and maintain theme files 
- Always include a theme dector to prefer the users system theme, build styles for dark and light modes
- Ensure text colors and backgrounds do not clash and are readable as much as possible. E.g. Don't put blue text on dark background
