# Socratic Chatbot

一个苏格拉底式对话网页项目。后端使用 FastAPI，前端页面位于 `web/`。

## 目录结构

```text
app.py              FastAPI 后端入口
web/                前端页面与静态资源
prompts/            系统提示词与风格说明
inference/          推理与对话生成代码
train/              训练/数据构建脚本
data/               小规模训练与示例数据
eval/               测试提示词
requirements.txt    Python 依赖
start_autodl.sh     AutoDL 一键启动脚本
```

## 运行

### 模型与 Adapter

本项目当前使用的默认模型配置来自 `app.py`：

```text
Base model:
/root/autodl-tmp/models/Qwen3-4B-Instruct-2507

LoRA adapter:
/root/socratic-chatbot/outputs/socratic-qwen3-4b-lora-v6

默认端口:
6006
```

也就是说，我实际部署时用的是：

```text
Qwen3-4B-Instruct-2507 + socratic-qwen3-4b-lora-v6
```

注意：GitHub 仓库里不包含模型权重和 LoRA adapter。你需要自己把模型和 adapter 放到对应路径，或者启动时手动指定路径。

### 依赖环境

推荐环境：

```text
Python >= 3.10
PyTorch >= 2.4
transformers >= 4.51
peft >= 0.15
accelerate >= 1.6
fastapi >= 0.115
uvicorn >= 0.34
```

如果你想完全复现 AutoDL 上的环境，建议在原服务器运行：

```bash
pip freeze > requirements-freeze.txt
```

然后把 `requirements-freeze.txt` 也保存下来。

安装依赖：

```bash
pip install -r requirements.txt
```

启动服务：

```bash
bash start_autodl.sh
```

默认端口为 `6006`。如果需要自定义模型路径：

```bash
SOCRATIC_BASE_MODEL=/path/to/base-model \
SOCRATIC_ADAPTER=/path/to/lora-adapter \
PORT=6006 \
bash start_autodl.sh
```

## 注意

本仓库不包含大模型权重、LoRA adapter、缓存文件和训练输出。运行前需要自行准备：

- base model：`Qwen3-4B-Instruct-2507`
- LoRA adapter：`socratic-qwen3-4b-lora-v6`
- Python / PyTorch 环境
