# Git branch

## 1.Sort Branches by Committer date
Base Use:
```
git for-each-ref --sort=-committerdate refs/heads/

# Or using git branch (since version 2.7.0)
git branch --sort=-committerdate  # DESC
git branch --sort=committerdate  # ASC
```

Advanced Usage:
```
git for-each-ref --sort=committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'  

git for-each-ref --sort=-committerdate refs/heads/ --format='%(committerdate:short) %(authorname) %(refname:short)'  
git for-each-ref --sort='-committerdate' --format='%(refname)%09%(committerdate)' refs/heads | sed -e 's-refs/heads/--'
```

Pro Usage (Unix):  
You can put the following snippet in your ~/.gitconfig.  
The recentb alias accepts two arguments:  
* refbranch: which branch the ahead and behind columns are calculated against. Default master
* count: how many recent branches to show. Default 20
```
[alias]  
    # ATTENTION: All aliases prefixed with ! run in /bin/sh make sure you use sh syntax, not bash/zsh or whatever
    recentb = "!r() { refbranch=$1 count=$2; git for-each-ref --sort=-committerdate refs/heads --format='%(refname:short)|%(HEAD)%(color:yellow)%(refname:short)|%(color:bold green)%(committerdate:relative)|%(color:blue)%(subject)|%(color:magenta)%(authorname)%(color:reset)' --color=always --count=${count:-20} | while read line; do branch=$(echo \"$line\" | awk 'BEGIN { FS = \"|\" }; { print $1 }' | tr -d '*'); ahead=$(git rev-list --count \"${refbranch:-origin/master}..${branch}\"); behind=$(git rev-list --count \"${branch}..${refbranch:-origin/master}\"); colorline=$(echo \"$line\" | sed 's/^[^|]*|//'); echo \"$ahead|$behind|$colorline\" | awk -F'|' -vOFS='|' '{$5=substr($5,1,70)}1' ; done | ( echo \"ahead|behind||branch|lastcommit|message|author\\n\" && cat) | column -ts'|';}; r"
```
Result:  
![Result](https://i.stack.imgur.com/Q8Buq.png "")

Refer:  
https://stackoverflow.com/questions/5188320/how-can-i-get-a-list-of-git-branches-ordered-by-most-recent-commit
https://www.commandlinefu.com/commands/view/2345/show-git-branches-by-date-useful-for-showing-active-branches
https://www.cnblogs.com/v5captain/p/9428893.html