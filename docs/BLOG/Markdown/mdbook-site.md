# Publish a Website with mdBook and GitHub Pages

template at <https://github.com/Yang-Xijie/mdbook-site>

## mdbook init

```
$ mkdir mdbook-site
$ cd mdbook-site
$ mdbook init

Do you want a .gitignore to be created? (y/n)
y
What title would you like to give the book?
my-book
2022-05-21 17:50:25 [INFO] (mdbook::book::init): Creating a new book with stub content

All done, no errors...
```

```
$ tree -a
.
├── .gitignore
├── book
├── book.toml
└── src
    ├── SUMMARY.md
    └── chapter_1.md
```

## Add GitHub Workflow

```
$ mkdir .github
$ cd .github
$ mkdir workflows
$ cd workflows
$ vim PublishMySite.yml
```

```yml
name: PublishMySite

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      # Build markdown files to a static site.
      - name: Setup mdBook
        uses: peaceiris/actions-mdbook@v1
        with:
          mdbook-version: "latest"
      - run: mdbook build . --dest-dir ./book # --dest-dir is relative to <dir>
      
      # Publish the static site to gh-pages branch.
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN}}
          publish_dir: ./book
          publish_branch: gh-pages
```

```
$ tree -a
.
├── .github
│   └── workflows
│       └── PublishMySite.yml
├── .gitignore
├── book.toml
└── src
    ├── SUMMARY.md
    └── chapter_1.md
```

## Git and GitHub

### git init

```
$ git init
$ git add .
$ git commit -m "init"
```

### GitHub - New Repository

GitHub > New Repository

GitHub > Repository > Settings > Actions > General > 

- Actions permissions: Allow all actions and reusable workflows
- Workflow permissions: Read and write permissions
- Click Save

```
$ git remote add origin git@github.com:Yang-Xijie/mdbook-site.git # change to your github repo
$ git branch -M main
$ git push -u origin main
```

GitHub > Repository > Settings > Pages > Source > gh-pages > Click Save

## Postscript

View your site at <https://yang-xijie.github.io/mdbook-site/>.

Modify your markdown files in src/, make a new commit and push your site to GitHub. GitHub will automatically publish the newest contents.
