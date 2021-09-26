# Git Common Advanced use

## 1 命令图解
![Result](/asset/1896029811-19a1c8c9ad5326cf_fix732.png "")


## 2. 暂存
暂存不止是 git stash 和 git stash pop
```shell
# 保存所有正在追踪的文件
git stash save "日志信息"

# 列出所有的暂存项
git stash list

# 获取并删除暂存项
git stash apply stash@{1}
git stash drop stash@{1}
# ……或使用一条命令……
git stash pop stash@{1}
```

## 3. 清理
```shell
# 移除远程仓库上不存在的分支
git fetch -p

# 移除所有包含 `greenkeeper` 的分支
git fetch -p && git branch --remote | fgrep greenkeeper | sed 's/^.\{9\}//' | xargs git push origin --delete

```


Refer：  
https://segmentfault.com/a/1190000021643071?utm_source=sf-similar-article