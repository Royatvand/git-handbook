<div align="center">

# Git Handbook

**Learn Git by understanding the workflow — from your first commit to collaboration and recovery.**

[English guide](./Git-Zero-to-Hero-EN.md) · [راهنمای فارسی](./Git-Zero-to-Hero-FA.md) · [Persian project overview](./README.fa.md) · [Contributing](./CONTRIBUTING.md)

</div>

---

## Why this handbook?

Git is easier to learn when you understand what each command changes and why it matters. This handbook focuses on practical workflows, readable examples, safe recovery techniques, and the habits developers use when working together.

## Choose your language

| Resource | Language | Description |
|---|---|---|
| [Git: Zero to Hero](./Git-Zero-to-Hero-EN.md) | English | A structured, 30-section guide from the fundamentals to advanced workflows |
| [آموزش جامع Git از صفر تا حرفه‌ای](./Git-Zero-to-Hero-FA.md) | فارسی | راهنمای کامل فارسی با مثال‌های عملی، عیب‌یابی و برگه‌ی تقلب |
| [نمای کلی پروژه](./README.fa.md) | فارسی | معرفی پروژه، مسیر یادگیری و روش مشارکت |

## What you'll learn

- **Core concepts:** repositories, the working tree, the staging area, commits, and history
- **Everyday workflow:** {tick}status{tick}, {tick}diff{tick}, {tick}add{tick}, {tick}commit{tick}, {tick}pull{tick}, and {tick}push{tick}
- **Parallel work:** branches, merges, rebase, and conflict resolution
- **Recovery tools:** {tick}restore{tick}, {tick}revert{tick}, {tick}reflog{tick}, {tick}bisect{tick}, and {tick}cherry-pick{tick}
- **Team collaboration:** remotes, pull requests, code review, and common branching workflows
- **Advanced topics:** tags, submodules, hooks, and an introduction to GitHub Actions

## Recommended learning path

1. Read one section at a time; don't try to memorize every command.
2. Create a disposable practice repository and run the examples there.
3. Before changing or deleting anything, inspect the repository with {tick}git status{tick} and {tick}git diff{tick}.
4. Practise branches and merge conflicts with files you can safely recreate.
5. Learn the difference between local history changes and changes already shared with others.

> **Safety note:** Commands such as {tick}git reset --hard{tick}, {tick}git clean -fd{tick}, and force-push can discard work or affect collaborators. Understand the consequences before running them, and avoid experimenting on a project that contains work you cannot lose.

## Repository structure

{tick}{tick}{tick}text
git-handbook/
├── README.md
├── README.fa.md
├── Git-Zero-to-Hero-EN.md
├── Git-Zero-to-Hero-FA.md
└── CONTRIBUTING.md
{tick}{tick}{tick}

## Who is this for?

Beginners, students, and frontend or backend developers who want a dependable Git workflow and a practical reference they can return to while building projects.

## Contributing

Found a typo, unclear explanation, or a command that could be safer? Contributions are welcome. Please read the [contribution guidelines](./CONTRIBUTING.md) before opening an issue or pull request.

## Official references

- [Git documentation](https://git-scm.com/doc)
- [Pro Git book](https://git-scm.com/book/en/v2)
- [GitHub Docs](https://docs.github.com/)

## Maintainer

Created and maintained by [Royatvand](https://github.com/Royatvand).

---

<div align="center"><sub>Understand the workflow. Practise safely. Keep your history useful.</sub></div>
