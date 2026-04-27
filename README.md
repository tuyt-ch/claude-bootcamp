# Claude Bootcamp

Hands-on workshop environment for Claude Code and the Anthropic SDK.
Runs in a dev container — Docker + VS Code Dev Containers extension required, or use GitHub Codespaces.

---

## Setup

### 1. Create `.env`

The container loads credentials via `--env-file .env`. Copy the example and fill in both tokens:

```bash
cp .env.example .env
```

```dotenv
GH_TOKEN=<github-fine-grained-pat>
CLAUDE_CODE_OAUTH_TOKEN=<claude-code-oauth-token>
```

**`GH_TOKEN`** — Fine-grained PAT from [github.com/settings/tokens](https://github.com/settings/tokens). Repository permissions: **Contents → Read-only**.

**`CLAUDE_CODE_OAUTH_TOKEN`** — Run `claude setup-token` on an authenticated machine and copy the output.

### 2. Open the Dev Container

**VS Code:** Open the repo folder, then **Dev Containers: Reopen in Container**. First build takes 1-5 minutes.

**Codespaces:** Add `GH_TOKEN` and `CLAUDE_CODE_OAUTH_TOKEN` as [Codespaces secrets](https://github.com/settings/codespaces) with access to this repo.
Then create the Codespace. Once the terminal is up, run `cp .env.example .env`, fill in the tokens, and **Dev Containers: Rebuild Container**.

> Codespaces secrets inject as env vars, but the container also needs the `.env` file on disk because of the `--env-file` run arg.

### 3. Verify

```bash
source .venv/bin/activate
python testclaude.py
```

Expected: both Test 1 and Test 2 print success messages.

---

## Troubleshooting

| Error | Fix |
|-------|-----|
| `cannot open .env` | `.env` is missing — `cp .env.example .env` |
| `NoCredentials` / `could not resolve credentials` | AWS session expired — re-authenticate as instructed by your trainer |
| `ModuleNotFoundError: No module named 'anthropic'` | `source .venv/bin/activate` first |
| Claude Code not authenticated | Verify `CLAUDE_CODE_OAUTH_TOKEN` in `.env` or run `claude login` |
| Codespace container fails to start | Create `.env`, fill in tokens, then rebuild the container |
