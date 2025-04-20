Github进行fork后如何与原仓库同步
step 1、执行命令 git remote add upstream https://github.com/selfteaching/the-craft-of-selfteaching.git 
把远端fork的仓库设置成你的upsteam
step 2、git checkout -b new-branch upsteam/master 切换到新的remote的仓库分支，继续开发
