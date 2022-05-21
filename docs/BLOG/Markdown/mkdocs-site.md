# Publish a Website with Material for MkDocs and GitHub Pages

template at <https://github.com/Yang-Xijie/mkdocs-site>

## mkdocs new

```
$ mkdocs new mkdocs-site
INFO     -  Creating project directory: mkdocs-site
INFO     -  Writing config file: mkdocs-site/mkdocs.yml
INFO     -  Writing initial docs: mkdocs-site/docs/index.md
$ cd mkdocs-site
```

```
$ tree -a
.
├── docs
│   └── index.md
└── mkdocs.yml
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
name: publish site
on: # 在什么时候触发工作流
  push: # 在从本地main分支被push到GitHub仓库时
    branches:
      - main
  pull_request: # 在main分支合并别人提的pr时
    branches:
      - main
jobs: # 工作流的具体内容
  deploy:
    runs-on: ubuntu-latest # 创建一个新的云端虚拟机 使用最新Ubuntu系统
    steps:
      - uses: actions/checkout@v2 # 先checkout到main分支
      - uses: actions/setup-python@v2 # 再安装Python3和相关环境
        with:
          python-version: 3.x
      - run: pip install mkdocs-material # 使用pip包管理工具安装mkdocs-material
      - run: mkdocs gh-deploy --force # 使用mkdocs-material部署gh-pages分支
```

```
$ tree -a
.
├── .github
│   ├── .DS_Store
│   └── workflows
│       └── PublishMySite.yml
├── docs
│   └── index.md
└── mkdocs.yml
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
$ git remote add origin git@github.com:Yang-Xijie/mkdocs-site.git # change to your github repo
$ git branch -M main
$ git push -u origin main
```

GitHub > Repository > Settings > Pages > Source > gh-pages > Click Save

## Postscript

View your site at <https://yang-xijie.github.io/mkdocs-site/>.

Modify your markdown files in docs/, make a new commit and push your site to GitHub. GitHub will automatically publish the newest contents.
