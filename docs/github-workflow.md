# GitHub Workflow Guide

Complete guide to understanding and using GitHub workflows for collaboration.

---

## Table of Contents

1. [GitHub Essentials](#github-essentials)
2. [The Fork & Pull Request Workflow](#the-fork--pull-request-workflow)
3. [Creating Your First Pull Request](#creating-your-first-pull-request)
4. [Code Review Process](#code-review-process)
5. [Merge Strategies](#merge-strategies)
6. [Advanced Workflows](#advanced-workflows)
7. [GitHub Features](#github-features)
8. [Best Practices](#best-practices)

---

## GitHub Essentials

### GitHub vs Git

| Git | GitHub |
|-----|--------|
| Version control system | Web-based Git hosting |
| Local or server | Cloud-based service |
| Command-line tool | Web interface + API |
| Manages code history | Collaboration platform |

### Your GitHub Workflow Overview

```
1. Fork Repository
   ↓
2. Clone to Local Machine
   ↓
3. Create Feature Branch
   ↓
4. Make Changes
   ↓
5. Commit & Push
   ↓
6. Create Pull Request
   ↓
7. Code Review
   ↓
8. Merge to Main
```

---

## The Fork & Pull Request Workflow

### Why Fork?

- ✅ You get your own copy to modify
- ✅ You can't accidentally break the main repo
- ✅ Easy to submit changes via Pull Request
- ✅ Maintains a clean project history

### Step 1: Fork the Repository

```
On GitHub.com:
1. Go to repository page
2. Click "Fork" button (top right)
3. Select where to fork (your account)
4. Wait for fork to complete
```

**Result**: You now have `your-username/repo-name`

### Step 2: Clone Your Fork

```bash
# Clone your forked repository
git clone https://github.com/YOUR-USERNAME/repo-name.git

# Navigate into the directory
cd repo-name

# Add upstream remote (original repo)
git remote add upstream https://github.com/original-owner/repo-name.git

# Verify remotes
git remote -v
# Output:
# origin    https://github.com/YOUR-USERNAME/repo-name.git (fetch)
# origin    https://github.com/YOUR-USERNAME/repo-name.git (push)
# upstream  https://github.com/original-owner/repo-name.git (fetch)
# upstream  https://github.com/original-owner/repo-name.git (no push)
```

### Step 3: Create Feature Branch

```bash
# Update local main with latest from upstream
git fetch upstream
git checkout main
git merge upstream/main

# Create and switch to feature branch
git checkout -b feature/my-feature

# Or use newer syntax
git switch -c feature/my-feature
```

### Step 4: Make Changes

```bash
# Edit your files
# Make logical, focused changes

# View what changed
git status
git diff

# Stage changes
git add .

# Commit with clear message
git commit -m "feat: add new feature"
```

### Step 5: Push to Your Fork

```bash
# Push your branch to your fork
git push origin feature/my-feature

# First time pushing? Use:
git push -u origin feature/my-feature
```

### Step 6: Create Pull Request

On GitHub.com:

1. Go to your forked repository
2. Notice a "Compare & pull request" button
3. Click it
4. Fill in PR details:
   - **Title**: Clear, concise description
   - **Description**: Explain changes and why
   - **Reference issues**: `Closes #123`
5. Click "Create pull request"

---

## Creating Your First Pull Request

### PR Title Best Practices

```
✅ Good titles:
- feat: add dark mode support
- fix: correct button alignment
- docs: update installation guide
- refactor: simplify authentication logic

❌ Avoid:
- Update
- Fix stuff
- asdfgh
- WIP
```

### PR Description Template

```markdown
## Description
Brief explanation of what this PR does.

## Related Issues
Closes #123
Related to #456

## Changes Made
- Change 1
- Change 2
- Change 3

## Testing
Steps to test this feature:
1. Step 1
2. Step 2
3. Step 3

## Screenshots (if applicable)
Add screenshots showing the changes

## Checklist
- [ ] Code follows style guidelines
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Added tests for new features
- [ ] All tests passing
```

### PR Do's and Don'ts

✅ **Do:**
- Focus on a single feature or fix
- Write clear, descriptive messages
- Keep PR size reasonable (< 400 lines)
- Reference related issues
- Respond to feedback promptly
- Test your changes thoroughly

❌ **Don't:**
- Mix multiple features in one PR
- Make unrelated changes
- Push directly without PR
- Ignore feedback
- Leave PR stale for weeks
- Commit sensitive information

---

## Code Review Process

### When Someone Reviews Your PR

Reviewers will:
- ✓ Check code quality
- ✓ Verify functionality
- ✓ Suggest improvements
- ✓ Catch bugs or issues
- ✓ Provide learning opportunities

### Types of Comments

| Type | Example | Response |
|------|---------|----------|
| **Suggestion** | "Consider using...?" | Think about it, reply |
| **Question** | "Why did you do X?" | Explain your reasoning |
| **Request** | "Please change..." | Acknowledge & change |
| **Praise** | "Great solution!" | Thank you 🙏 |

### Responding to Review

```bash
# 1. View comments on GitHub

# 2. Make requested changes locally
# (edit files)

# 3. Commit changes
git commit -m "refactor: address review feedback"

# 4. Push to same branch
git push origin feature/my-feature

# PR updates automatically!

# 5. Reply to comments on GitHub
# "Done! Made the changes as requested."
```

### Resolving Conversations

After making requested changes:
1. Click "Resolve conversation" on GitHub
2. Maintainer will re-review
3. Process repeats until approved

---

## Merge Strategies

### Merge Commit

```
Preserves full history

Main:     A --- B --- M (merge commit)
Feature:        └--- C --- D ---┘

Good for: Complex features, important changes
```

```bash
git merge feature/branch
```

### Squash and Merge

```
Combines all commits into one

Main:     A --- B --- S (squashed commit)
Feature:        └--- C --- D ---┘

Good for: Small fixes, keeping history clean
```

```bash
git merge --squash feature/branch
git commit -m "feat: descriptive message"
```

### Rebase and Merge

```
Rewrites history linearly

Main:     A --- B --- C --- D
Feature:        └--- C' --- D' ---┘ (replayed)

Good for: Linear history, feature branches
```

```bash
git rebase main
git push origin feature/branch
# Then merge via GitHub
```

---

## Advanced Workflows

### Keeping Your Fork Updated

```bash
# Fetch latest from upstream
git fetch upstream

# Rebase your changes on latest main
git rebase upstream/main

# Or merge (creates merge commit)
git merge upstream/main

# Push updated branch
git push origin feature/branch
```

### Resolving Conflicts

```bash
# During merge/rebase, conflicts occur
git status  # See conflicts

# Edit conflicted files
# Look for:
# <<<<<<< HEAD
# your changes
# =======
# their changes
# >>>>>>>

# Fix conflicts manually

# Mark as resolved
git add .

# Continue merge/rebase
git commit  # or git rebase --continue
```

### Cherry-picking Commits

```bash
# Apply specific commit to current branch
git cherry-pick abc123

# Cherry-pick range
git cherry-pick abc123..def456

# Cherry-pick with editing
git cherry-pick -e abc123
```

---

## GitHub Features

### Issues

- Report bugs or request features
- Track project tasks
- Organize work with labels
- Assign to team members

### Pull Request Templates

Create `.github/pull_request_template.md`:

```markdown
## Description


## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation

## Related Issues
Closes #

## Checklist
- [ ] Tests pass
- [ ] Documentation updated
```

### Labels

Common labels:
- `bug` - Something isn't working
- `enhancement` - New feature
- `documentation` - Docs improvement
- `good first issue` - Good for beginners
- `help wanted` - Need assistance

### Milestones

Group related issues/PRs:
- v1.0.0
- Q3 2026
- Roadmap items

### GitHub Projects

Kanban board for tracking work:
- To Do
- In Progress
- In Review
- Done

---

## Best Practices

### Before Creating a PR

✅ **Preparation**
```bash
# 1. Sync with upstream
git fetch upstream
git rebase upstream/main

# 2. Test thoroughly
npm test  # or your test command

# 3. Run linter
npm run lint

# 4. Review your own changes first
git diff upstream/main

# 5. Create PR
```

### PR Etiquette

1. **Be respectful** - Reviewers are helping
2. **Respond promptly** - Don't leave PRs stale
3. **Ask questions** - If feedback is unclear
4. **Give credit** - Thank reviewers
5. **Accept feedback** - Learn and improve

### Commit Quality

Each commit should:
- ✅ Represent a single logical change
- ✅ Have a clear message
- ✅ Pass all tests
- ✅ Not break the build

### PR Size Guidelines

- **Small**: < 100 lines (easy review)
- **Medium**: 100-300 lines (normal)
- **Large**: > 300 lines (consider splitting)
- **Huge**: > 1000 lines (almost always split)

**Smaller PRs are easier to review and merge!**

---

## Quick Reference

| Action | Command |
|--------|---------|
| Fork repo | Click "Fork" on GitHub |
| Clone fork | `git clone <fork-url>` |
| Add upstream | `git remote add upstream <orig-url>` |
| Create branch | `git checkout -b feature/name` |
| Push branch | `git push origin feature/name` |
| Create PR | Click on GitHub website |
| Update PR | Push more commits to same branch |
| Sync fork | `git fetch upstream && git rebase upstream/main` |
| Delete branch | `git branch -d feature/name` |

---

## Troubleshooting

### "Your branch is ahead of upstream"

```bash
# You have commits not in upstream
git fetch upstream
git rebase upstream/main
git push -f origin feature/branch
```

### PR has conflicts

```bash
# Update with latest main
git fetch upstream
git rebase upstream/main

# Resolve conflicts (fix files)
git add .
git rebase --continue
git push -f origin feature/branch
```

### Accidentally committed to main

```bash
# Create new branch with commits
git branch feature/new-feature

# Reset main to upstream
git reset --hard upstream/main
```

---

## Next Steps

- Learn about [Pull Requests](pull-requests.md)
- Read [Collaboration Guide](collaboration.md)
- Check [Git Basics](git-basics.md)

---

**Happy collaborating! 🚀**
