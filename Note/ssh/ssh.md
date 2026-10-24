# SSH

# 1. 生成 Ed25519 SSH 密钥（邮箱用于标识密钥）
```bash
ssh-keygen -t ed25519 -C "tonybryant2084@gmail.com"
```

# 2. 查看 SSH 公钥（Public Key）
```bash
cat ~/.ssh/id_ed25519.pub
```

# 3. 查看 SSH 私钥（Private Key）
```bash
cat ~/.ssh/id_ed25519
```

# 4. 测试 GitHub SSH 连接
```bash
ssh -T git@github.com
```