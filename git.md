##常用linux命令
*    cd：改变目录。
*   cd...回退到上一个目录，直接cd进入默认目录
*   pwd：显示当前所在的目录路径。
*   Is（II）：都是列出当前目录中的所有文件，只不过1I（两个II）列出的内容更为详细。
*   touch：新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。
*   rm：删除一个文件，rm index.js就会把index.js文件删除。
*   mkdir：新建一个目录，就是新建一个文件夹。
*   rm-r：删除一个文件夹，rm-rsrc删除src目录
*   mv移动文件，mv index.html src index.html是我们要移动的文件，src是目标文件夹，当然，这样写，必须保证文件和目标文件夹在同一目录下。
*    reset重新初始化终端/清屏。
*   clear 清屏。
*   history查看命令历史。
*   help帮助。
*   exit 退出。
*   #表示注释

##git文件操作
```

#查看指定文件状态
git status [filename]

#查看所有文件状态
git status

# git add .                  添加所有文件到暂存区
# git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```
```

#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt


```

##分支
```

# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```