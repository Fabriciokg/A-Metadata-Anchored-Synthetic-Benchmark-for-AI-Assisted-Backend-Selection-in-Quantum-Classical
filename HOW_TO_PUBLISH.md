# How to publish this repository on GitHub or GitLab

Run these commands from the repository folder:

```bash
git init
git add README.md README.pt-BR.md LICENSE requirements.txt environment.yml .gitignore .env.example CHANGELOG.md HOW_TO_PUBLISH.md docs outputs notebooks paper
git commit -m "Initial open-science release"
```

Create an empty repository on GitHub or GitLab. Then add the remote URL.

For GitHub:

```bash
git branch -M main
git remote add origin https://github.com/your-username/ai-quantum-backend-selection.git
git push -u origin main
```

For GitLab:

```bash
git branch -M main
git remote add origin https://gitlab.com/your-username/ai-quantum-backend-selection.git
git push -u origin main
```

Before pushing, make sure no credentials are staged:

```bash
git status
```

The file `.env` must never appear in the files to be committed.
