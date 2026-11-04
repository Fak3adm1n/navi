---
dg-publish: true
tags:
  - Github
---
GitHub SSH Key 配置与推送流程（超详细）
本指南适用于首次使用 SSH Key 连接 GitHub 并推送代码，适合本地终端、iSH、Termux 等环境。

一、生成 SSH Key
在终端执行以下命令（推荐 ed25519）：

1
`ssh-keygen -t ed25519 -C "你的GitHub邮箱"`
如果不支持 ed25519，也可以用：
`ssh-keygen -t rsa -b 4096 -C "你的GitHub邮箱"`
一路回车，默认保存在：

私钥：~~/.ssh/id_ed25519
公钥：~~/.ssh/id_ed25519.pub
二、启动 ssh-agent 并添加私钥（可选但推荐）
`eval "$(ssh-agent -s)"`
`ssh-add ~/.ssh/id_ed25519`
三、复制公钥内容
`cat ~/.ssh/id_ed25519.pub`
复制终端输出的一整行。

四、添加公钥到 GitHub
登录 GitHub
右上角头像 → Settings
左侧菜单 → SSH and GPG keys
点击 New SSH key
填名称、粘贴公钥 → Add SSH Key
> 新版变了，自己研究一下


五、测试是否连接成功
`ssh -T git@github.com`
成功时输出：
`Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.`
六、配置 Git 用户信息（首次使用）
(在此之前，在本地新建一个文件夹并打开作为你的github仓库，或者clone一个)
`git config --global user.name "你的GitHub用户名"`
`git config --global user.email "你的GitHub邮箱"`
七、检查或修改远程地址为 SSH
查看远程地址：
`git remote -v`
输出应为：
`origin  git@github.com:your-username/your-repo.git (fetch)`
如果是 https，则修改为 SSH：
`git remote set-url origin git@github.com:your-username/your-repo.git`
八、推送代码到 GitHub

```
git add .
git commit -m "更新内容"
git push
```
