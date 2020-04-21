## 同一个github.com下多用户切换
我有两个用户需要切换github的信息。这是因为github.com对qq邮箱不支持，老是要验证。但是换gmail.com的则不会。这太排斥中国用户了。

```bash
# 配置两个id_rsa的私钥对
ssh-keygen -t rsa -C "liweilijie@gmail.com" -f id_rsa_liweiliji
ssh-keygen -t rsa -C "453220764@qq.com" -f id_rsa

# 删除配置的全局信息
git config --global --unset user.email
git config --global --unset user.name

# 下载并编译giter
git clone https://github.com/jsmartx/giter.git

# 用giter.git增加两个用户
 giter ls
   liweilijie - https://github.com
 * emacsvi - https://github.com

giter use liweilijie

```

- 切换的时候：`giter use liweilijie`
- 修改相关的配置路径`~/.ssh/config`
```toml
Host github.com
  HostName github.com
  User git
  Port 22
# IdentityFile ~/.ssh/id_rsa
  IdentityFile ~/.ssh/id_rsa_liweilijie
  TCPKeepAlive yes
  IdentitiesOnly yes
```
