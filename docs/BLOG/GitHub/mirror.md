# GitHub 镜像到 Gitee

```
$ ssh-keygen
Enter file in which to save the key (/Users/yangxijie/.ssh/id_rsa): key
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in key
Your public key has been saved in key.pub
```

1. Gitee > Settings > Security Settings > SSH Keys > Add key > Title: GitHub Mirror & Key: key.pub
1. Gitee > Settings > Security Settings > Personal access tokens > Generate new token > Token Description: GitHub Mirror > copy
1. GitHub > Project > Settings > Security > Secrets > Actions / New secret > Name: Gitee Mirror & Value: key
1. GitHub > Project > Settings > Security > Secrets > Actions / New secret > Name: Gitee Access & Value: paste

./github/workflows/gitee-mirror.yml

```yml
on:
  push:
    branchs: main  
  schedule:
    # every UTC 17:00 -> CST (China) 1:00
    - cron: '0 17 * * *'
name: mirror Github repos to Gitee
jobs:
  run:
    name: Sync-GitHub-to-Gitee
    runs-on: ubuntu-latest
    steps:
    - name: get repository list exclude private and fork
      id: repo
      uses: yi-Xu-0100/repo-list-generator@v1.0.1
    - name: mirror Github repos to Gitee
      uses: Yikun/hub-mirror-action@master
      with:
        src: github/Yang-Xijie # change to your name
        dst: gitee/yang-xijie # change to your name
        dst_key: ${{ secrets.GITEE_PRIVATE_KEY }}
        dst_token: ${{ secrets.GITEE_TOKEN }}
        force_update: true
        account_type: user
        debug: true
```

## 60 days

You might receive an email like this after 60 days:

> [GitHub] The "mirror Github repos to Gitee" workflow in Yang-Xijie/Gitee-Mirror will be disabled soon
> 
> GitHub Actions scheduled workflow
> 
> Scheduled workflows are disabled automatically after 60 days of repository inactivity.
>
> You can prevent mirror Github repos to Gitee from being disabled on the workflows page.

Just update your repo to reactive the sync action.

## References

- [自动镜像 GitHub 仓库到 Gitee](https://shixiangwang.github.io/sync2gitee/)
- [GitHub / Yikun/hub-mirror-action](https://github.com/Yikun/hub-mirror-action)
