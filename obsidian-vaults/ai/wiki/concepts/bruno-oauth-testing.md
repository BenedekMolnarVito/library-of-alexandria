---
title: "Bruno OAuth Testing"
type: concept
domain: ai
tags:
  - developer-tooling
  - oauth
  - testing
  - api-clients
created: 2026-10-12
updated: 2026-10-12
sources:
  - "[[wiki/sources/dev-tooling-gotchas]]"
---

# Bruno OAuth Testing

How to obtain and use a valid Bearer token in [Bruno](https://www.usebruno.com/) when testing OAuth2-protected APIs. The key gotcha: Bruno can return **200 OK even without a valid Bearer token** — the auth failure is silent.

## The silent-200 gotcha

If you hit a protected endpoint without a valid Bearer token, you may still see `200 OK` — but the response will be wrong or empty (often the service returns a generic error body at HTTP 200 rather than a proper 401). Always confirm you have a green, non-expired token in the Auth tab before trusting any result.

## Step-by-step: get a Bearer token via OAuth2 client credentials

1. **Set the environment** — select the correct environment (dev / test / prod) in Bruno's environment dropdown.
2. **Obtain the `client_secret`** — retrieve it from wherever your secrets are stored (e.g. a vault, a `.env` file, a secrets manager). Do not commit it to the repo.
3. **Configure the Auth tab** — in the collection's Auth tab, set the grant type to **Client Credentials**, paste in the `client_id` and `client_secret`, and set the token URL for your OAuth2 server.
4. **Fetch the token** — verify the credentials are shown in green, then click **Get Access Token**. Make sure **"Use system browser for OAuth"** is **unticked** (leave it for browser-based flows; client credentials are headless).
5. **Use the token** — subsequent Bruno calls in the collection automatically attach the Bearer token. You can also copy the raw token value from the Access Token dropdown for use in other tools.

## Tips

- **Token expiry:** OAuth2 client-credentials tokens typically expire in seconds to minutes. Re-fetch before a test run if you've been idle.
- **Scope mismatches:** A token issued without the right scopes will cause 403s, not 401s. Check the token's decoded payload (`jwt.io`) to confirm expected scopes are present.
- **Redirect URIs:** Client credentials flows have no redirect URI; if Bruno prompts for one, you are on the wrong grant type.

## Related Concepts

- [[wiki/concepts/agentic-arch-tools-mcp]] — MCP and API tool design principles
- [[wiki/concepts/langchain-mcp-client]] — HTTP auth patterns for MCP servers

## Sources

- [[wiki/sources/dev-tooling-gotchas]]
