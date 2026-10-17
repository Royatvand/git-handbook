# Contributing to Git Handbook

Thank you for helping make this Git learning resource clearer, safer, and more useful. Contributions of all sizes are welcome, including corrections, examples, translations, and improved explanations.

## What makes a good contribution?

- Fix inaccurate or confusing explanations.
- Keep commands reproducible and explain any assumptions.
- Prefer small, focused changes over unrelated edits.
- Keep the English and Persian editions aligned when changing shared concepts.
- Add a warning when a command can discard work, rewrite history, or affect collaborators.
- Use respectful, beginner-friendly language and consistent Git terminology.

## Before opening a pull request

1. Read the relevant section in both language editions when possible.
2. Check that links point to the intended files or official documentation.
3. Review your changes carefully for spelling, formatting, and Markdown rendering.
4. Verify commands in a disposable practice repository when feasible.
5. Describe what changed and how you checked it.

## Suggested workflow

    git clone https://github.com/Royatvand/git-handbook.git
    cd git-handbook
    git switch -c docs/describe-your-change

Edit the relevant file, then review and commit your work:

    git status
    git diff
    git add path/to/changed-file
    git diff --staged
    git commit -m "docs: describe your change"
    git push -u origin docs/describe-your-change

Open a pull request on GitHub and explain the motivation, the main changes, and any checks you performed. The branch name and commit message above are examples; choose names that describe your contribution.

## Documentation style

- Write clear headings that help readers scan the page.
- Prefer short paragraphs and focused examples.
- Use placeholders such as OWNER/REPOSITORY when a command depends on a user's own repository.
- Never present a sample email, URL, token, or configuration value as a real credential.
- Explain the purpose and effect of destructive commands before showing them.
- Use official Git or GitHub documentation when a claim needs an authoritative reference.

## Security and privacy

Never commit passwords, access tokens, API keys, private keys, private user data, or confidential information. If a secret has already been pushed, removing it from the latest version is not enough: revoke or rotate it and follow the hosting provider's incident guidance.

## Language editions

The project currently maintains English and Persian guides. When a concept changes, please check whether the matching section, table of contents, examples, or navigation links also need updating in the other language.

## Scope

This repository is an educational handbook, not a replacement for the official Git documentation. Contributions should stay focused on learning Git, improving practical workflows, and helping readers avoid common mistakes.
