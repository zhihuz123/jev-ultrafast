# Security and privacy

Jev Ultrafast runs a real browser with real accounts, so a committed file can expose
far more than source code. Treat personal data and credentials as local-only.

## Never commit

- API keys, access tokens, cookies, session IDs, and passwords.
- `.env` or any `.env.*` file with real values. Only `.env.example` belongs in git,
  and it must keep empty values.
- Task scripts, traces, screenshots, and recordings that contain a shipping address,
  phone number, order details, or account data.
- `iherb_script.py`, which is a local-only run script. It contains personal shipping
  details and discount codes, is listed in `.gitignore`, and must never be added with
  `git add -f`.

`secrets/`, `credentials/`, `*.pem`, `*.key`, `*.token`, `*.secret`, and `*.local.py`
are ignored for the same reason.

## Before committing

```bash
git status --short
git check-ignore -v .env iherb_script.py
git diff --cached
```

Confirm that the staged diff contains no credentials or personal data. Ignored files
are skipped by `git add .`; naming a file explicitly, using `git add -f`, or staging
from another clone can still leak it.

## If something leaks

1. Remove the file from the current commit and from history; a later delete commit
   leaves it readable in the repository history.
2. Rotate every exposed key, token, cookie, and password. Assume a public remote has
   already been copied.
3. If personal data was pushed to a public repository, treat it as disclosed and take
   the appropriate account and identity precautions. GitHub support can help purge
   cached views and forks, but cannot recall what was already downloaded.
4. Force-pushing a rewritten branch is destructive and requires explicit approval.

## Reporting

Report a security or privacy issue privately to the repository owner rather than
opening a public issue with the sensitive details.
