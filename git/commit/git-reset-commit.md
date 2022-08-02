# git-reset-commit 撤销提交

``` bash



git log # 查看git提交记录

git reset commitId  # 撤销commit，但不修改代码
  
git stash # 可以先缓存一下代码

git reset --hard commitId  # 撤销commit，同时将代码恢复到对应ID的版本

git push origin HEAD --force # 强制提交，把远程的代码回退到这个commit

# 或者简写成 git push origin HEAD --f

git stash pop

```

---

扩展：

1. 版本回退： [[git-remote-rollback]]