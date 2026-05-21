# Aisance Action

Turn every pull request into a 60-second lesson. The merge stays blocked
until the PR author passes a short, personalized question about their own diff.

Part of [Aisance](https://aisance.dev) — learn while you ship.

## Usage

Add `.github/workflows/aisance.yml` to your repository:

```yaml
name: Aisance
on: pull_request

jobs:
  lesson:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
      contents: read
    steps:
      - uses: hanzili/aisance-action@v1
        with:
          token: ${{ secrets.AISANCE_TOKEN }}
```

Get your `AISANCE_TOKEN` from [aisance.dev](https://aisance.dev) and add it as
a repository secret: **Settings → Secrets and variables → Actions → New secret**.

## How it works

1. On every pull request, the Action sends the diff to Aisance.
2. Aisance generates a lesson — a short tutorial plus one question — and this
   check goes red.
3. A comment links the PR author to the lesson.
4. Pass it, and the check turns green on its own. Merge unblocked.

Trivial diffs (formatting, config) are skipped automatically. If Aisance is
unreachable, the check fails open — it never permanently blocks your PR.
