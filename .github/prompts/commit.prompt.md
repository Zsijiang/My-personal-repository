---
mode: 'agent'
description: 'Stage, commit, create PR, and merge to main. Standard commit-PR-merge workflow for academic projects.'
---

# Commit, PR, and Merge

Stage changes, commit with a descriptive message, create a PR, and merge to main.

## Steps

1. **Check current state:**

```bash
git status
git diff --stat
git log --oneline -5
```

2. **Create a branch** from the current state:

```bash
git checkout -b <short-descriptive-branch-name>
```

3. **Stage files** — add specific files (never use `git add -A`):

```bash
git add <file1> <file2> ...
```

Do NOT stage:
- `.claude/settings.local.json` or local config files
- Files containing secrets or credentials
- Large binary files (PDFs, datasets) unless intentional
- Generated files that should be in `.gitignore`

4. **Commit** with a descriptive message explaining *why*, not just *what*:

```bash
git commit -m "Add supply-demand diagram to Lecture 3 slides"
# Or for multi-line:
git commit -m "$(cat <<'EOF'
Refactor data analysis script for Lecture 4

- Switch from lfe to fixest for panel regressions
- Add event study plot with confidence intervals
- Export tables in both .tex and .html format
EOF
)"
```

5. **Push and create PR:**

```bash
git push -u origin <branch-name>
gh pr create --title "<short title>" --body "$(cat <<'EOF'
## Summary
- [Bullet point 1]
- [Bullet point 2]

## Test plan
- [ ] LaTeX compiles without errors
- [ ] R scripts run without errors
- [ ] Quarto renders correctly
EOF
)"
```

6. **Merge and clean up:**

```bash
gh pr merge <pr-number> --merge --delete-branch
git checkout main
git pull
```

7. **Report** the PR URL and what was merged.

---

## Important

- Always create a **NEW branch** — never commit directly to main
- Use `--merge` (not `--squash` or `--rebase`) unless asked otherwise
- Keep commits focused: one logical change per commit
- If given a specific commit message, use it exactly
