---
dg-publish: true
tags:
  - Linux
---
Termux
https://github.com/termux/termux-app/releases/tag/v0.118.3

tmoe
`awk -f <(curl -L l.tmoe.me/2.awk)`

Pacman配置
因为刚装好本地密钥库（keyring）太旧了，导致 Pacman 根本不信任新下载的软件包。但如果直接 pacman -S archlinux-keyring 更新密钥，Pacman 又会因为旧密钥校验不过去而拒绝下载它，陷入“先有鸡还是先有蛋”的死循环。

禁用密钥签名校验
`sed -i 's/SigLevel = .*/SigLevel = Never/g' /etc/pacman.conf`

沙盒
`sed -i 's/#DisableSandbox/DisableSandbox/g' /etc/pacman.conf`

2. 初始化密钥环目录

```
pacman-key --init
pacman-key --populate archlinux
```

3. 强行安装/更新 keyring
   `pacman -S --noconfirm archlinux-keyring`

改回

```
sed -i 's/SigLevel = .*/SigLevel = Required DatabaseOptional/g; s/SigLevel = Never/SigLevel = Required DatabaseOptional/g' /etc/pacman.conf
```
