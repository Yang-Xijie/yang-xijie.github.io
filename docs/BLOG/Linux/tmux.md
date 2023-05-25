# tmux 使用指南

这篇教程已经写得很详细了 [tmux 使用教程-阮一峰](http://www.ruanyifeng.com/blog/2019/10/tmux.html)

- 新建 `tmux new -s <session-name>`
- 查看 `tmux ls`
- 连接 `tmux attach -t <session-name>`
- 分离 `ctrl B D` `tmux` `detach`
- 退出 `exit` `ctrl D`

```
alias tnew="tmux new -s "
alias tls="tmux ls"
alias tat="tmux attach -t "
alias tkill="tmux kill-session -t "
```
