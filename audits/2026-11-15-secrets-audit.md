# Secrets audit of my own GitHub repositories

Date: 2026-11-15
Author: Albert (kazanly)
Scope: 3 of my own repositories (Python bots and automation scripts)
Goal: find secrets (passwords, tokens, API keys) and personal data in code and git history

## Method
1. Checked repository visibility (Public / Private)
2. Checked .gitignore: which files are excluded from git
3. Searched current code for keywords:
   grep -rilE "token|api_key|secret|password|bearer|client_id" . --exclude-dir=.git
4. Followed variables to where they get their value (keyword search missed AMO_PASS)
5. Listed all files ever committed:
   git log --all --name-only --format="" | sort | uniq
6. Searched full git history:
   git log -p --all | grep -n "VARIABLE_NAME"
7. Searched history for Telegram bot token pattern:
   git log -p --all | grep -nE "[0-9]{8,10}:[A-Za-z0-9_-]{30,}"
8. Checked image metadata (EXIF, GPS): mdls file.jpg

## Findings

| # | Repository | Finding | Risk |
|---|---|---|---|
| 1 | CRM automation script | CRM login and password hardcoded in code and in git history | High |
| 2 | CRM automation script | Weak dictionary password | High |
| 3 | CRM automation script | Log file with real client phone numbers committed to git | Medium |
| 4 | CRM automation script | Browser profiles, WhatsApp sessions and JSON keys excluded by .gitignore from the first commit | Good |
| 5 | Telegram bot | No token in code or history, credentials file excluded | Good |
| 6 | Telegram bot | README says to use .env, but code does not load it | Low (code quality) |
| 7 | Telegram bot | Images have no GPS or device metadata | Good |

All repositories with code are private. This lowers the risk but does not remove it.

## Recommendations
- Rotate (change) any leaked password first. Deleting it from code is not enough: it stays in git history and copies.
- Never hardcode secrets. Load them from environment variables or a .env file listed in .gitignore.
- Do not commit logs with personal data. Add *.log, *_log.txt to .gitignore.
- Before making a repository public, scan the full history, not only current files.

## Lessons learned
- Keyword search is not enough: variable names can hide secrets (AMO_PASS did not match "password").
- Exact search can fail on small details (two spaces before "=").
- Git history keeps everything that was ever committed.
- Secrets must be masked even in private chats and screenshots.
