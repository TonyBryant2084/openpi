# Git 常用配置

## 1. 查看当前 Git 可执行文件路径

```bash
which git
```

### 2. 设置 Git 全局用户名和邮箱

```bash
# 设置全局用户名
git config --global user.name "TonyBryant2084"

# 设置全局邮箱（替换为自己的邮箱）
git config --global user.email "your_email@example.com"
```

## 3. 查看当前生效的 Git 用户名和邮箱

```bash
# 查看当前生效的用户名
git config user.name

# 查看当前生效的邮箱
git config user.email
```

## 4. 查看、添加和删除 Git 远程仓库（Remote）
```bash
# 1. 查看当前仓库配置的所有远程仓库名称及地址
git remote -v

# 2. 添加远程仓库
# origin：远程仓库名称，通常默认使用 origin
git remote add origin https://github.com/TonyBryant2084/PI_0.git

# 3. 删除远程仓库
git remote remove origin
```

## 5. 查看当前所在分支
```bash
git branch --show-current
```