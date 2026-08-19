# Day 34 - Git & GitLab Commands Reference
*Thu, 13 Aug 2026*

## Git — Version Control Basics

Git is a **distributed version control system** — every clone is a full copy of the repository's history, not just a working copy.

### Setup & Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "code --wait"   # set default editor
git config --list                                # view all settings
```

### Starting a Repository

```bash
git init                          # initialize a new repo in the current folder
git clone <repo-url>              # copy an existing remote repo locally
git clone <repo-url> <folder>     # clone into a specific folder name
```

### Checking Status & History

```bash
git status                        # see staged/unstaged/untracked changes
git log                           # full commit history
git log --oneline                 # compact, one line per commit
git log --graph --oneline --all   # visualize branch history
git diff                          # unstaged changes vs last commit
git diff --staged                 # staged changes vs last commit
git show <commit-hash>            # details of a specific commit
```

### Staging & Committing

```bash
git add <file>                    # stage a specific file
git add .                         # stage everything in current directory
git add -A                        # stage everything, including deletions, repo-wide
git commit -m "message"           # commit staged changes
git commit -am "message"          # stage tracked files + commit in one step
git commit --amend                # edit the most recent commit (message or content)
```

### Branching

```bash
git branch                        # list local branches
git branch <name>                 # create a new branch
git branch -d <name>               # delete a branch (safe — checks it's merged)
git branch -D <name>               # force-delete a branch
git checkout <branch>              # switch to a branch
git checkout -b <branch>           # create AND switch to a new branch
git switch <branch>                # modern equivalent of checkout for switching
git switch -c <branch>             # modern equivalent of checkout -b
```

### Merging & Rebasing

```bash
git merge <branch>                 # merge <branch> into the current branch
git rebase <branch>                # replay current branch's commits on top of <branch>
git rebase -i HEAD~3                # interactive rebase — squash/reorder last 3 commits
```

| Merge | Rebase |
|---|---|
| Preserves full history, creates a merge commit | Rewrites commit history into a straight line |
| Safe for shared/public branches | Avoid on branches others have already pulled |
| Non-linear history | Cleaner, linear history |

### Working With Remotes

```bash
git remote -v                      # list remotes and their URLs
git remote add origin <url>        # link a local repo to a remote
git fetch                          # download remote changes, don't merge yet
git pull                           # fetch + merge in one step
git pull --rebase                  # fetch + rebase instead of merge
git push                           # push current branch to its remote
git push -u origin <branch>        # push and set upstream tracking
git push --force-with-lease        # safer force-push (checks for others' work first)
```

### Undoing Changes

```bash
git restore <file>                 # discard unstaged changes to a file
git restore --staged <file>        # unstage a file (keep the changes)
git reset --soft HEAD~1            # undo last commit, keep changes staged
git reset --mixed HEAD~1           # undo last commit, keep changes unstaged (default)
git reset --hard HEAD~1            # undo last commit, DISCARD all changes
git revert <commit-hash>           # create a new commit that undoes a previous one (safe for shared history)
```

### Stashing

```bash
git stash                          # temporarily shelve uncommitted changes
git stash list                     # see all stashes
git stash pop                      # reapply the most recent stash and remove it
git stash apply                    # reapply the most recent stash, keep it in the list
git stash drop                     # delete a stash without applying it
```

### Tags

```bash
git tag                            # list tags
git tag v1.0.0                     # create a lightweight tag
git tag -a v1.0.0 -m "Release 1.0" # create an annotated tag
git push origin v1.0.0             # push a single tag
git push origin --tags             # push all tags
```

### Inspecting Differences Between Branches

```bash
git diff main..feature             # what's in feature but not main
git log main..feature              # commits in feature but not main
git cherry-pick <commit-hash>       # apply a specific commit from another branch
```

---
## GitLab — Hosting, CI/CD & Workflow

GitLab is a **DevOps platform** that hosts Git repositories and adds project management, CI/CD, and issue tracking on top.

### Typical GitLab Workflow

```
Create Project → Clone Locally → Create Feature Branch
    → Commit & Push → Open Merge Request → Code Review
    → CI Pipeline Runs → Merge → Deploy
```

### Merge Requests (MRs) — GitLab's Term for Pull Requests

```bash
git push -u origin feature/my-branch
```
Then, on GitLab: **Repository → Merge Requests → New Merge Request**, selecting source (`feature/my-branch`) and target (`main`) branches.

### `.gitlab-ci.yml` — CI/CD Pipeline Configuration

Lives at the repo root — defines the pipeline GitLab runs on every push.

```yaml
stages:
  - build
  - test
  - deploy

build-job:
  stage: build
  script:
    - mvn clean compile

test-job:
  stage: test
  script:
    - mvn test

deploy-job:
  stage: deploy
  script:
    - mvn deploy
  only:
    - main    # only deploy from the main branch
```

### Key CI/CD Concepts

| Term | Meaning |
|---|---|
| **Pipeline** | The full sequence of stages run for a commit/MR |
| **Stage** | A phase in the pipeline (e.g. build, test, deploy) — stages run in order |
| **Job** | An individual task within a stage — jobs in the same stage run in parallel |
| **Runner** | The agent that actually executes pipeline jobs |
| **Artifact** | A file/output from a job, passed to later stages (e.g. a built JAR) |

```yaml
build-job:
  stage: build
  script:
    - mvn clean package
  artifacts:
    paths:
      - target/*.jar
```

### Useful GitLab CLI (`glab`) Commands

```bash
glab auth login                    # authenticate with GitLab
glab repo clone <project>          # clone a project
glab mr create                     # create a merge request from the current branch
glab mr list                       # list open merge requests
glab mr merge <id>                 # merge an MR
glab ci status                     # check pipeline status for current branch
glab issue create                  # create a new issue
```

### GitLab Protected Branches & Approvals

- **Protected branches** (usually `main`) prevent direct pushes — changes must go through an MR
- **Approval rules** require a set number of reviewers to approve before merging
- Configured under **Settings → Repository → Protected Branches** / **Merge Request Approvals**

### `.gitignore` (Applies to Both Git & GitLab)

```
# Java build output
target/
*.class

# IDE files
.idea/
*.iml
.vscode/

# Logs
*.log

# Environment secrets
.env
```
