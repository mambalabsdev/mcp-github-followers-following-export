# GitHub Followers and Following Export MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-github-followers-following-export)](https://www.npmjs.com/package/@mambalabsdev/mcp-github-followers-following-export) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-github-followers-following-export)](https://github.com/mambalabsdev/mcp-github-followers-following-export/blob/main/LICENSE)

An MCP server for the Mamba Labs GitHub Followers and Following Export actor on Apify. Export the followers and following lists of public GitHub accounts as flat rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give GitHub usernames or profile URLs. For each one you get a row per follower or followed account, with login, name, company, location, bio, profile URL, and user ID, and a free report row per list that states the count GitHub declares and whether the list was read to the end.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-github-followers-following-export": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-github-followers-following-export"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `export_github_followers_following` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Export who sindresorhus follows on GitHub."
- "Get the first 500 followers of octocat with their locations."
- "Did this export reach the end of the followers list?"

## Tool

`export_github_followers_following`. One tool. Example arguments:

```json
{
  "users": [
    "sindresorhus"
  ],
  "list": "following",
  "max_results_per_list": 20
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `users` | array | no | Usernames or profile URLs of public GitHub accounts, up to 100 a run. Clay users: wrap a column in a one item list. |
| `list` | string | no | followers, following, or both (default). |
| `max_results_per_list` | number | no | Rows to return per list, from 1 to 100000. Default 1000. Each row is charged. Large lists also need a longer run timeout: about 400 rows a minute. |
| `github_token` | string | no | Optional. Your own GitHub token reads through the REST API at up to 5,000 requests an hour, with login, user ID, and avatar only: no name, company, location, or bio. Never stored or logged. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `user-row`, one follower or followed account returned | $0.002 | $0.0019 | $0.0018 | $0.0017 |
| `apify-actor-start`, per run start | $0.0015 | $0.0015 | $0.0015 | $0.0015 |

List reports, a user with no public account, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/github-followers-following-export](https://apify.com/mambalabs/github-followers-following-export)

## License

MIT. See [LICENSE](LICENSE).
