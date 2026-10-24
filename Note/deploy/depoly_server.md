# 【服务器端】（显存要求 >= 24G）
## 1. 创建并激活环境
```bash
conda create -n openpi_env python=3.11 -y
conda activate openpi_env
```

## 2. 克隆项目代码

### 2.1 子模块（由`.gitmodules`定义）
| 子模块 | 主要作用 | 与 π0 / π0.5 的关系 |
|---|---|---|
| `third_party/aloha` | 提供 ALOHA 机器人平台相关的硬件控制、数据采集与操作代码 | 支持真实机器人实验及相关数据工作流 |
| `third_party/libero` | 提供机器人操作仿真环境、任务定义和评测机制 | 用于测试模型在仿真任务中的执行能力与成功率 |

### 2.2 克隆项目带子模块（--recurse-submodules）
```bash
git clone --recurse-submodules https://ghfast.top/https://github.com/Physical-Intelligence/openpi.git
```
### 2.3 不带子模块：只克隆 OpenPI 主仓库，不下载 Git 子模块
```bash
git clone https://ghfast.top/https://github.com/Physical-Intelligence/openpi.git
```
## 3. 安装项目依赖（需科学上网）

### 3.1 设置 pip 的清华镜像源（持久生效）
```bash
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```
### 3.2 安装 uv（uv的cache默人conda所有环境共享）
```bash
pip install uv
```
### 3.3 设置 uv 清华镜像源（仅当前终端生效）
```bash
export UV_DEFAULT_INDEX=https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```

### 3.4 进入 OpenPI 项目目录
```bash
cd openpi/
```

### 3.5 跳过 Git LFS 大文件自动下载，并依据 pyproject.toml 和 uv.lock 文件安装项目依赖

1. `GIT_LFS_SKIP_SMUDGE=1`：跳过 Git LFS 大文件的自动下载（仅对相关 Git 操作生效）。
2. `pyproject.toml`：定义项目依赖、Python 版本要求及项目配置。
3. `uv.lock`：锁定依赖包的具体版本及解析结果，保证环境的可复现性。
4. `uv sync`：根据 `pyproject.toml` 和 `uv.lock` 创建或同步虚拟环境，并安装项目依赖。

```bash
GIT_LFS_SKIP_SMUDGE=1 uv sync
```

## 4. 下载并解压模型权重（10G）
```bash
wget https://www.modelscope.cn/models/masheng/pi0-fine-Tuned-Models/resolve/master/pi0_fast_libero.zip
mkdir -p  $HOME/.cache/openpi/openpi-assets/checkpoints
unzip pi0_fast_libero.zip -d $HOME/.cache/openpi/openpi-assets/checkpoints/
```

## 5. 启动推理服务(会自动连接到HuggingFace)
```bash
export HF_ENDPOINT=https://hf-mirror.com
uv run scripts/serve_policy.py --env LIBERO
```