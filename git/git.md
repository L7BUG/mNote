# git
---
* # git reset --hard HEAD~2 代表后退2个版本
* # reflog
    > 查看提交历史
* # git log --graph --pretty=oneline --abbrev-commit
    > --graph 分支合并图
    > --pretty=oneline 只看基本信息
* # git merge `--no-ff -m "merge with no-ff"` dev (合并dev 分支)
* # `stash` 储藏
- # 查看远程库信息，使用`git remote -v`
-  # `git push origin --delete new_a` 删除远程分支