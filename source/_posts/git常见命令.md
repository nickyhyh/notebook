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

# 全局配置用户信息
`git config --global user.name "Nicky"`
`git config --global user.email "smyhvae@163.com"`

# 分支的合并
1.基于master分支，创建一个新的分支，起名为first_item_recommend
`$ git branch first_item_recommend    // 创建新的分支`
`$ git checkout first_item_recommend  //切换到新的分支`
2.在新的分支first_item_recommend上，完成开发工作，并 commit 、push。
3.将分支first_item_recommend上的开发进度合并到master分支：
`$ git checkout master  //切换到master分支`
`$ git merge first_item_recommend    //将分支 first_item_recommend 的开发进度合并到 master 分支`
4.合并之后，master分支和first_item_recommend分支会指向同一个位置。
5.删除分支first_item_recommend：
`git branch -d first_item_recommend`