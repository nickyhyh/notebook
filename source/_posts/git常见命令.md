---
title: git常用命令
---
# 创建仓库命令
git init - 初始化仓库
git clone - 拷贝一份远程仓库
# 提交与修改
git add - 添加文件到暂存区
git commit - 将暂存区内容添加到仓库中
git status - 查看仓库当前状态，显示有变更的文件
git diff - 比较暂存区和工作区文件的不同
git rm- 删除工作区文件
git reset  - 回退版本
# 远程操作
git remote - 远程仓库操作
git fetch - 从远程获取代码块
git pull - 下载远程代码并合并
git push - 上传远程代码并合并
# 发布笔记步骤
1.`npm run build`
2.commit修改的内容
3.push修改内容
4.`npm run publish`
## 发布报错
1.git status:检查commit状态 
2.git clean:清除未被 add 或被 commit 的本地修改
3.git checkout -f:强制切换分支
4.git branch -D gh-pages-xxx:删除xxx分支
提示error: Cannot delete branch 'gh-pages-b039354' checked out at 'E:/note'
切换分支:
`git checkout master `
`git branch -D gh-pages-xxx`
`git push`
`npm run publish`