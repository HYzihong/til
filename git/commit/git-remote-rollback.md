# git-remote-rollback 远程回滚


#### `revert` 和 `reset` 的区别

- `revert`  放弃指定提交的修改，但是会生成一次新的提交，需要填写提交注释，以前的历史记录都在.
-  `reset` 指将HEAD指针指到指定提交，历史记录中不会出现放弃的提交记录.


#### 回滚策略

##### 撤回某次提交的commit的提交代码，创建一个新commit来说明本次代码回滚

```bash


git revert HEAD # 撤销上次提交的代码，形成新的commit

git push origin master # 提交远程

```




##### 只撤回某次提交的commit和提交的代码


```bash

git reset --hard HEAD^ # 撤回上一次提交

git push origin master -f # 强制提交，


```