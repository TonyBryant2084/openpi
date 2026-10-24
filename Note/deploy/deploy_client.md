# 【客户端】
## 1. 创建并激活环境
```bash
conda create -n pi0_demo python=3.10
conda activate pi0_demo
```

## 3. 克隆 pi0_fast_deploy 项目
```bash
git clone https://github.com/yueduduo/pi0_fast_deploy.git
```

## 4. 进入项目目录
```
cd pi0_fast_deploy
```

## 5. 根据 requirements.txt 安装项目依赖
```
pip install -r requirements.txt
```

## 6. 配置远程推理服务器地址和端口
```bash
打开 demo.py，修改 Args 类中的以下参数：

Args.host：远程 OpenPI 推理服务器的 IP 地址。

Args.port：远程 OpenPI 推理服务器的端口号，需与服务器实际监听端口一致。

确保本地客户端能够通过网络连接远程推理服务器。
```

## 7. 运行仿真实验
```bash
python demo.py
```

## 8. 程序启动后，在终端输入自然语言任务指令：
```bash
grasp the red box

按下回车，程序通过远程 π0 模型推理控制 robosuite 仿真环境中的 Panda 机械臂执行抓取任务。

注意： 项目作者指出，首次运行可能出现 段错误 (核心已转储)（Segmentation Fault），重新运行后可能恢复。但这并非正常现象或必然规律，如果持续出现，需要排查 MuJoCo、robosuite 及相关依赖的兼容性。
```

## 9. 保存仿真实验结果
```bash
运行生成的视频保存至 Args.video_out_path 指定的目录。

默认保存路径：

./output/videos

可以通过修改 demo.py 中的 Args.video_out_path 参数调整视频保存位置。
```

## 10. 拓展不同仿真环境
```bash
通过修改 demo.py 中的以下函数，可以尝试适配不同的仿真环境和机器人操作任务：

getenv()：负责创建或获取仿真环境，可修改环境名称、机器人类型及相关配置。

eval_my_env()：负责执行仿真评测流程，可修改观测数据处理、模型推理、动作执行和任务评测逻辑。

注意： 切换仿真环境时，还需要确保模型输入输出与新环境兼容，包括相机图像、机器人状态、动作维度及控制方式等。
```

## 11. 注意事项：跨机器人部署
```bash
当前使用的 π0 模型不能保证直接迁移到不同机器人平台后仍然正常完成任务。

例如，从 Panda 机械臂切换到 UR5 机械臂时，由于机器人运动学结构、关节数量、状态表示及动作空间等可能存在差异，模型可能无法直接适配，导致任务执行失败。

因此，更换机器人平台时，通常需要：

调整机器人观测数据和动作空间的适配方式。

确保模型输入输出维度及控制接口与目标机器人一致。

根据目标机器人的数据进行微调（Fine-tuning），以提高任务执行成功率
```