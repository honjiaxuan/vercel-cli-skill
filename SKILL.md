---
name: vercel-cli
description: |
  Comprehensive guide for using the Vercel Command-Line Interface (CLI) to manage and configure Vercel Projects. Use this when you need to deploy, manage environment variables, link projects, or interact with Vercel services from the terminal.
license: MIT
compatibility: opencode
allowed-tools:
  - bash
  - write
  - read
  - grep
  - glob
  - skill
  - question
  - todowrite
---

# Vercel CLI

## Problem
Developers need a way to programmatically or manually interact with Vercel's platform to manage deployments, environment variables, and project configurations without using the web dashboard.

## Context / Trigger Conditions  
- When deploying a project to production or preview environments.
- When syncing local environment variables with Vercel.
- When linking a local directory to a Vercel Project.
- When managing domains, DNS, SSL certificates, or team scopes from the command line.
- When looking up Vercel documentation for specific features or troubleshooting.

## Solution

### Documentation

Fetch any Vercel docs page as markdown:

```bash
curl -s "https://vercel.com/docs/<path>" -H 'accept: text/markdown'
```

**Get the full sitemap to discover all available pages:**
```bash
curl -s "https://vercel.com/docs/sitemap.md" -H 'accept: text/markdown'
```

### Global Options
- `--token`: Authenticate using a token (essential for CI/CD).
- `--version`: Display the installed version.
- `--help`: Get information about available commands.
- `--debug`: Enable verbose logging.
- `--cwd [path]`: Set the working directory.

### Major Commands & Essential Flags

| Command | Description | Essential Flags / Subcommands |
| :--- | :--- | :--- |
| **deploy** | Deploy Vercel projects (default command). | `--prod` (production), `--target=[env]`, `--yes` (skip prompts), `--build-env [key=val]` |
| **dev** | Replicate Vercel environment locally. | `--port [number]` (default 3000), `--listen [address]` |
| **env** | Manage environment variables. | `add [name] [env]`, `update [name] [env]`, `rm [name]`, `pull [file]`, `ls`, `run -- <cmd>` |
| **pull** | Sync local project with remote settings. | `--environment=[production\|preview\|development]`, `--yes` |
| **link** | Link local directory to a Vercel Project. | `[path-to-directory]`, `--project [name]`, `--yes` |

### Management & Configuration

| Command | Description | Key Subcommands / Flags |
| :--- | :--- | :--- |
| **alias** | Manage custom domain aliases. | `ls`, `set [deployment-url] [alias]`, `rm [alias]` |
| **project** | Manage Vercel Projects. | `add`, `ls`, `rm`, `inspect [name]` |
| **domains** | Manage domains. | `add [domain]`, `rm [domain]`, `buy [domain]`, `inspect [domain]`, `transfer [domain]` |
| **dns** | Manage DNS records. | `add [domain] [name] [type] [value]`, `ls [domain]`, `rm [id]` |
| **certs** | Manage SSL certificates. | `ls`, `issue [domain]`, `rm [id]` |
| **teams** | Manage team scopes. | `add`, `ls`, `switch [team]`, `invite [email]` |
| **login** | Authenticate with Vercel. | `--github`, `--gitlab`, `--bitbucket` |
| **logout** | End the current session. | - |
| **whoami** | Show current user. | - |
| **switch** | Switch team scope. | `[team-name]` |

### Deployment Operations

| Command | Description | Key Flags |
| :--- | :--- | :--- |
| **list** | List recent deployments. | `[project-name]`, `--app` |
| **inspect** | Get deployment details. | `[id\|url]`, `--logs`, `--wait` |
| **logs** | Stream runtime logs. | `[url]`, `--follow`, `--limit [n]` |
| **remove** | Delete deployments. | `[id\|url]`, `--yes` |
| **rollback** | Revert production deployment. | `[id\|url]`, `status` |
| **promote** | Promote deployment to production. | `[id\|url]`, `status` |
| **redeploy** | Rebuild and redeploy. | `[id\|url]`, `--no-wait` |

### Advanced & Utilities

| Command | Description | Notes |
| :--- | :--- | :--- |
| **bisect** | Binary search for issues. | `--good [url]`, `--bad [url]` |
| **blob** | Vercel Blob storage. | `put`, `get`, `del`, `copy`, `ls` |
| **build** | Local/CI build. | `--prod`, `--output [path]` |
| **cache** | Manage CDN/Data cache. | `purge --type [cdn\|data]`, `invalidate --tag [tag]` |
| **init** | Initialize from examples. | `[example-name]` |
| **integration** | Manage Integrations. | `add`, `ls`, `open`, `remove` |
| **redirects** | Project-level redirects. | `add`, `upload [file]`, `promote` |
| **rolling-release** | Gradual rollouts. | `start`, `approve`, `complete` |
| **telemetry** | CLI telemetry. | `enable`, `disable`, `status` |

## Verification
1. Run `vercel --version` to check installation.
2. Run `vercel login` to authenticate.
3. Use `vercel help [command]` to verify specific flags and subcommands.

## Notes
- Commands like `curl` and `httpstat` are in beta and include protection bypass features.
- CI/CD environments should use `--token` with a Vercel Access Token.
