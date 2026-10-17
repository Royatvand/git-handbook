# Git: Zero to Hero

> A practical, step-by-step guide to Git — from your first repository to teamwork, conflict resolution, recovery, and automation.
>
> **Prepared by: Royatvand**

Work through one section at a time. Run commands in a practice repository, and inspect the repository before using commands that rewrite history or discard files.

## Table of contents

1. [What is Git?](#1-what-is-git)
2. [Installation and configuration](#2-installation-and-configuration)
3. [Core concepts](#3-core-concepts)
4. [Create your first repository](#4-create-your-first-repository)
5. [The daily workflow](#5-the-daily-workflow)
6. [Inspect changes and history](#6-inspect-changes-and-history)
7. [Ignore files with .gitignore](#7-ignore-files-with-gitignore)
8. [Undo and recover changes](#8-undo-and-recover-changes)
9. [Branches](#9-branches)
10. [Merge branches](#10-merge-branches)
11. [Resolve merge conflicts](#11-resolve-merge-conflicts)
12. [Rebase](#12-rebase)
13. [Remotes](#13-remotes)
14. [Clone, fetch, pull, and push](#14-clone-fetch-pull-and-push)
15. [Stash temporary changes](#15-stash-temporary-changes)
16. [Tags and releases](#16-tags-and-releases)
17. [Cherry-pick a commit](#17-cherry-pick-a-commit)
18. [Recover with reflog](#18-recover-with-reflog)
19. [Find a bug with bisect](#19-find-a-bug-with-bisect)
20. [Submodules](#20-submodules)
21. [Git hooks](#21-git-hooks)
22. [Git internals](#22-git-internals)
23. [Write useful commit messages](#23-write-useful-commit-messages)
24. [Team workflows](#24-team-workflows)
25. [Pull requests and code review](#25-pull-requests-and-code-review)
26. [GitHub Actions basics](#26-github-actions-basics)
27. [Useful advanced commands](#27-useful-advanced-commands)
28. [Common problems](#28-common-problems)
29. [Command cheat sheet](#29-command-cheat-sheet)
30. [Suggested learning path](#30-suggested-learning-path)

---

## 1. What is Git?

Git is a **distributed version control system**. It records changes over time, lets you compare versions, and helps people work on the same project without having to exchange folders manually.

Git and GitHub are different:

| Git | GitHub |
|---|---|
| Version-control tool | Online platform for hosting Git repositories and collaborating |
| Works locally for many operations | Provides remote hosting, pull requests, issues, and other collaboration features |
| Alternatives include Mercurial | Alternatives include GitLab, Bitbucket, and Gitea |

A Git repository can exist on your computer without GitHub. GitHub is one place where you can host a remote copy.

## 2. Installation and configuration

Install Git from the [official download page](https://git-scm.com/downloads). On Debian or Ubuntu:

    sudo apt update
    sudo apt install git

Check the installation:

    git --version

Set the name and email recorded in your commits. Replace the example email with the one you intend to use:

    git config --global user.name "Your Name"
    git config --global user.email "you@example.com"

Useful settings:

    git config --global init.defaultBranch main
    git config --global color.ui auto
    git config --list
    git config user.name

The `--global` flag applies to your user account. Omit it when you want a setting to apply only to the current repository.

## 3. Core concepts

- **Working tree:** the files you see and edit.
- **Staging area (index):** the proposed set of changes for the next commit.
- **Commit:** a saved snapshot with metadata and a message.
- **Repository:** the database and metadata Git uses to track history.
- **Branch:** a movable reference to a line of development.
- **Remote:** a named reference to another repository, commonly hosted online.

The common cycle is: edit files → stage selected changes → commit. Staging is useful because it lets you choose exactly what belongs in a commit.

## 4. Create your first repository

Create a new project:

    mkdir git-practice
    cd git-practice
    git init
    git status

Create a file named `README.md`, then stage and commit it:

    git add README.md
    git commit -m "docs: add project introduction"

To copy an existing remote repository:

    git clone https://github.com/OWNER/REPOSITORY.git
    cd REPOSITORY

Replace the URL with the actual repository address. If the project already exists locally, do not run `git init` blindly in a directory that belongs to another repository.

## 5. The daily workflow

A simple, dependable routine:

    git status
    git diff
    git add path/to/file
    git diff --staged
    git commit -m "Describe the change"

Stage a specific file when possible rather than automatically staging every change. Use `git add -p` to select parts of a file interactively.

A commit should represent one meaningful unit of work. Smaller, focused commits are easier to review and, if necessary, revert.

## 6. Inspect changes and history

    git status
    git diff
    git diff --staged
    git log --oneline
    git log --oneline --graph --decorate --all
    git show <commit>

`git diff` shows unstaged changes; `git diff --staged` shows what will be included in the next commit. `git show` displays a commit and the changes it introduced.

To see who last changed each line of a tracked file:

    git blame path/to/file

Use blame to investigate context, not to assign blame to a person.

## 7. Ignore files with .gitignore

A `.gitignore` file tells Git which **untracked** files it should normally ignore. Typical entries include:

    node_modules/
    dist/
    build/
    .env
    *.log
    .DS_Store

Ignore patterns are specific to your project. Do not blindly ignore files that are needed to reproduce the project. A file already tracked by Git remains tracked even after adding a matching pattern; to stop tracking it while leaving it on disk:

    git rm --cached path/to/file

Before committing, make sure secrets, API tokens, private keys, and personal data are not included. If a secret was committed, removing it in a later commit does not make the exposed secret safe; revoke or rotate it.

## 8. Undo and recover changes

Choose the command according to what you want to undo.

Discard unstaged changes in one tracked file (destructive):

    git restore path/to/file

Remove a file from the staging area but keep its edits:

    git restore --staged path/to/file

Create a new commit that reverses a previous commit, usually the safer option for shared history:

    git revert <commit>

Move a local branch to an earlier commit:

    git reset --soft <commit>
    git reset --mixed <commit>

A hard reset discards staged and working-tree changes that are not preserved elsewhere:

    git reset --hard <commit>

Do not use `reset --hard` as a routine cleanup command. Check `git status` and back up important work first. For a commit already shared with a team, prefer `git revert` unless the team has explicitly agreed to rewrite history.

## 9. Branches

Branches let you work on a feature or fix separately from the main line of development.

    git branch
    git switch -c feature/profile-page
    # Make and commit your changes
    git switch main
    git branch -d feature/profile-page

To switch to an existing branch:

    git switch main

Older tutorials often use `git checkout` for switching and creating branches. `git switch` is a clearer command when you only want to switch branches. Deleting a local branch does not delete a remote branch.

## 10. Merge branches

To merge a feature into the current branch:

    git switch main
    git merge feature/profile-page

Git may create a merge commit, or it may fast-forward the current branch when possible. If conflicts occur, resolve them before completing the merge. Inspect the result and run the project's tests before pushing.

## 11. Resolve merge conflicts

A conflict happens when Git cannot automatically combine changes. It may mark a file with sections like:

    <<<<<<< HEAD
    Current-branch version
    =======
    Incoming-branch version
    >>>>>>> feature/profile-page

Edit the file so it contains the intended final result, and remove the conflict markers. Then:

    git status
    git add path/to/resolved-file
    git commit

For a merge, Git may ask you to commit the resolution. For a rebase, continue with `git rebase --continue` after staging the resolved files. Never delete conflict markers without checking which changes should be retained.

## 12. Rebase

Rebase replays commits onto a new base. It can make a feature branch's history easier to follow:

    git switch feature/profile-page
    git fetch origin
    git rebase origin/main

If a conflict occurs, resolve it and continue:

    git add path/to/resolved-file
    git rebase --continue

To stop the rebase and return to its starting state:

    git rebase --abort

Avoid rebasing commits that other people have already based work on unless the team coordinates the rewrite. Rebase changes commit identities; it is not simply another name for merge.

### Rebase or merge?

- **Merge:** records how histories were combined; generally safe for shared branches.
- **Rebase:** replays commits to create a linear-looking history; useful for local or coordinated feature-branch updates.

Choose based on the project's workflow rather than assuming one option is always superior.

## 13. Remotes

A remote is a named connection to another Git repository.

    git remote -v
    git remote add origin https://github.com/OWNER/REPOSITORY.git
    git remote show origin
    git remote set-url origin https://github.com/OWNER/NEW-REPOSITORY.git

`origin` is only a conventional name; it is not a special requirement. Use the real URL for your repository and avoid embedding credentials in remote URLs.

## 14. Clone, fetch, pull, and push

Clone a repository:

    git clone https://github.com/OWNER/REPOSITORY.git

Download remote updates without integrating them into the current branch:

    git fetch origin

Fetch and integrate updates into the current branch:

    git pull

Publish the current branch and set its upstream:

    git push -u origin feature/profile-page

Conceptually, `fetch` updates your knowledge of the remote, `pull` fetches and integrates changes, and `push` sends your local commits to a remote. Review what you are pushing and do not force-push shared branches without agreement.

## 15. Stash temporary changes

Stash puts selected working changes aside so you can switch tasks.

    git stash push -m "work in progress"
    git stash list
    git stash show -p
    git stash pop

`pop` reapplies and removes the selected stash if it applies successfully. `apply` reapplies changes without removing the stash. Stash is temporary storage, not a durable backup.

## 16. Tags and releases

Tags label specific points in history, often releases.

    git tag
    git tag -a v1.0.0 -m "Release v1.0.0"
    git show v1.0.0
    git push origin v1.0.0
    git push origin --tags

Use annotated tags for releases. Agree on version naming with the project before creating public release tags.

## 17. Cherry-pick a commit

Cherry-pick applies the change introduced by a particular commit to the current branch:

    git switch release-fix
    git cherry-pick <commit>

This creates a new commit on the current branch with the selected change. Use it for focused fixes that need to be carried across branches, and verify the result because the surrounding context may differ.

## 18. Recover with reflog

Reflog records recent movements of local references and can help locate commits no longer reachable from the current branch:

    git reflog
    git show <commit>
    git switch -c recovery-branch <commit>

Create a recovery branch before trying more destructive operations. Reflog entries are local and expire; reflog is a recovery aid, not a substitute for backups.

## 19. Find a bug with bisect

`git bisect` uses binary search through commits to find the change that introduced a bug. Start with a known-bad and known-good commit:

    git bisect start
    git bisect bad
    git bisect good <known-good-commit>

Test the checked-out revision, then label it:

    git bisect good
    # or:
    git bisect bad

Repeat until Git identifies the first bad commit, then finish:

    git bisect reset

Choose good and bad points that you can reliably verify. A test or reproducible manual check makes bisect much more effective.

## 20. Submodules

A submodule records a specific commit of another repository inside your repository.

    git submodule add https://github.com/OWNER/DEPENDENCY.git vendor/dependency
    git submodule update --init --recursive
    git clone --recurse-submodules https://github.com/OWNER/REPOSITORY.git

Submodules require deliberate version updates and can surprise contributors who clone without initializing them. Consider whether a package manager or another dependency strategy is simpler for your project.

## 21. Git hooks

Hooks are scripts Git can run at particular points, such as before a commit or after receiving changes. They live in the repository's Git metadata by default, so ordinary hooks are not automatically shared when someone clones the repository.

Use hooks for checks such as formatting or tests, but document them and do not treat local hooks as the only security or quality control. Teams often combine local hooks with CI checks.

## 22. Git internals

Git stores content as objects and connects those objects through commits and references. Important concepts:

- **Blob:** file content.
- **Tree:** directory structure and references to files or subdirectories.
- **Commit:** a snapshot reference, parent commit(s), author/committer metadata, and a message.
- **Reference:** a readable name that points to a commit, such as a branch or tag.
- **HEAD:** indicates the currently checked-out commit or branch.

Understanding these ideas explains why branches are lightweight references and why the same file content can be reused in Git's object database.

## 23. Write useful commit messages

A good message explains the intent of the change. Prefer specific messages:

    docs: clarify the rebase section
    fix: handle an empty search query
    test: cover profile validation

A commonly used Conventional Commits format is:

    <type>(optional-scope): short description

Common types include `feat`, `fix`, `docs`, `test`, `refactor`, and `chore`. A project may define its own convention; consistency matters more than blindly following a template.

## 24. Team workflows

Common ways teams organize branches include:

- **GitHub Flow:** small feature branches and pull requests, often merging into the main branch frequently.
- **Git Flow:** a more structured model with feature, release, and hotfix branches.
- **Trunk-Based Development:** frequent integration into a shared mainline, using small changes and suitable testing.

No workflow is best for every team. Choose one that matches release needs, team size, and automation. Keep branches focused and avoid long-lived divergence when possible.

## 25. Pull requests and code review

A pull request (PR) proposes changes and gives teammates a place to discuss and review them.

Before opening a PR:

1. Sync with the project's target branch using its agreed workflow.
2. Review `git diff` and `git status`.
3. Run relevant tests, linting, and builds.
4. Explain the reason for the change and how it was tested.

In review, prioritize correctness, security, readability, maintainability, and clear reasoning. Keep discussions respectful and distinguish blocking problems from optional suggestions.

## 26. GitHub Actions basics

GitHub Actions can run automated checks when commits are pushed or pull requests are opened. Workflow files are YAML files stored under `.github/workflows/`. A minimal example for a documentation repository could be:

    name: Markdown checks
    on:
      pull_request:
      push:
        branches: [main]
    jobs:
      basic-check:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v4
          - name: Show repository files
            run: ls -la

Real projects should add checks that match their language and tooling. Review third-party actions and pin versions or commit SHAs according to your project's security policy.

## 27. Useful advanced commands

Compare two branches:

    git diff main...feature/profile-page

Find commits matching a message:

    git log --oneline --grep="profile"

Rename a tracked file:

    git mv old-name.md new-name.md

Remove untracked files and directories **after previewing them**:

    git clean -nd
    git clean -fd

The first command previews what would be removed; the second actually removes it. Be cautious with `git clean`, especially when using options that include ignored files.

Inspect remote settings:

    git remote -v
    git remote show origin

## 28. Common problems

**A file does not appear on GitHub.** Check `git status`, make sure the file is not ignored, stage it, commit it, and push the correct branch.

**Push is rejected.** Fetch the remote changes, integrate them using your project's workflow, resolve any conflicts, then push again. Do not immediately force-push.

**The wrong commit was made.** If it is local and not shared, inspect your state before choosing `reset`. If it is already shared, `revert` is usually safer.

**A secret was committed.** Revoke or rotate it first. Removing it from the latest version does not erase it from repository history. Follow the hosting provider's guidance for sensitive-data removal if history must also be cleaned.

**A commit was made on the wrong branch.** Do not panic. Inspect `git status` and the commit graph, create a branch to preserve the commit if needed, then move changes carefully. Avoid reset commands until you understand exactly what will move or be discarded.

## 29. Command cheat sheet

| Goal | Command |
|---|---|
| Check repository state | `git status` |
| Stage a file | `git add path` |
| Create a commit | `git commit -m "message"` |
| Review unstaged edits | `git diff` |
| Review staged edits | `git diff --staged` |
| View compact history | `git log --oneline` |
| Create and switch branch | `git switch -c branch-name` |
| Switch branch | `git switch branch-name` |
| Merge a branch | `git merge branch-name` |
| Fetch remote changes | `git fetch origin` |
| Push branch | `git push` |
| Show remotes | `git remote -v` |
| Temporarily save work | `git stash push` |
| Undo a public commit | `git revert commit` |

## 30. Suggested learning path

### Stage 1: Fundamentals
Create a repository, edit a file, stage changes, commit them, and inspect history.

### Stage 2: Branches and remotes
Create a feature branch, merge it, clone a repository, fetch changes, and push a branch to a remote.

### Stage 3: Recovery and collaboration
Practise a merge conflict, use stash, recover a reference with reflog, and reverse a commit with revert in a disposable repository.

### Final practice project
1. Create a repository with a README and a `.gitignore`.
2. Commit the initial structure.
3. Create a feature branch and make a focused change.
4. Merge it into the main branch.
5. Create a second branch and intentionally edit the same line as main to practise conflict resolution.
6. Push to a remote and open a pull request if you have a GitHub repository available.
7. Review the final history and write down which commands felt confusing.

Do not measure progress by how many commands you memorized. Measure it by whether you can explain what a command changes, predict its effect, and recover safely when something goes wrong.

---

## Official references

- [Git documentation](https://git-scm.com/doc)
- [Pro Git book](https://git-scm.com/book/en/v2)
- [GitHub Docs](https://docs.github.com/)

**Back to the project:** [Git Handbook README](./README.md) · [Persian guide](./Git-Zero-to-Hero-FA.md)
