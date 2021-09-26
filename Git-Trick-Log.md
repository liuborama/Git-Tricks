# Git Log

## 1.格式化日志输出

--oneline 标记的作用是把每一个提交信息压缩为一行。  
--decorate 标记让git log展示所有指向每个提交引用（如分支，标签等）。  
--stat 与 -p  展示每个提交差异的选项  
git shortlog  创建发布公告的一种特殊的git log命令。按作者对每个提交分组，并展示每个提交信息的第一行。  
--graph 选项将会绘制一幅表示分支结构提交历史的ASCII图。该选项通常会结合--oneline与--decorate一起使用  
```shell
git log --graph --oneline --decorate
```
--pretty=format:"<string>" 这可以让你使用 printf 风格的占位符来展示每条提交。
```shell
git log --pretty=format:"%cn committed %h on %cd"
```

## 2. 过滤日志
### 1）按数量输出 
通过使用 -<n> 选项可以限制日志的输出数量   
```shell
git log -20 
```
### 2）按日期
使用 --after 或 --before 来按日期过滤提交  
```shell
git log --after="2021-8-1"
get log --after="yesterday"
git log --after="2021-8-1" --before="2021-8-1"
```
### 3）按作者/提交者
使用 --author / --committer 选项来过滤作者或提交者。该可用接受一个字符串或是正则表达式。  
```shell
git log --author="John"
git log --author="John\|Mary"
```
### 4）按消息
使用 --grep 选项来按提交信息筛选。
```shell
git log --grep="feature1234:"
```

### 5）按文件
-- 标记用于告知git log命令随后的参数是文件名而非分支名。如果命令中并不包含分支名，该标记也可省略。  
```shell
git log -- readme.md license
```

### 6）按内容
采用 -S"<string>" 格式的方式被称为 pickaxe ，例如，你想要知道字符串“Hello”被添加的提交你可以使用以下命令：
```shell
git log -S"Hello"
```
可以使用正则表达式，只需要用 -G"<regex>" 代替上述格式即可。

### 7）按范围
采用 -S"<string>" 格式的方式被称为 pickaxe ，例如，你想要知道字符串“Hello, World!”被添加的提交你可以使用以下命令：
```shell
#<since>和<until>是提交引用：
git log <since>..<until>
#master..feature 包含所有不在主分支中的功能分支的提交。
git log master..feature
```
也可以使用正则表达式，只需要用 -G"<regex>" 代替上述格式即可。


## 3. Show first commit by 'git log'
```shell
git rev-list --max-parents=0 HEAD
git log --pretty=oneline --reverse | head -1
```
## 4.滤掉日志中的大量无用的合并提交
```shell
git log --no-merges
```

Refer:  
https://segmentfault.com/a/1190000008039809