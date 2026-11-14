---
name: breeze-tts2-local
description: 在本地安装、运行和验证 Breeze TTS 2 的中文或英文语音生成、声音设计与声音克隆；用于实际部署或复现实测，不自动发布内容。
---

# Breeze TTS 2 本地部署与测试

先查看上游 [官方代码](https://github.com/breezeblue-ai/breeze-tts) 和 [模型卡与权重](https://huggingface.co/BreezeBlue/Breeze-TTS-2)，核对更新与许可。模型权重和自托管输出限研究及非商业用途，代码 Apache-2.0 不改变此限制。使用真人参考音频须取得必要的权利和许可；研究展示标明合成及来源。勿将自托管输出视为可变现素材。

## 环境

官方支持 Linux、Python 3.10 以上和 NVIDIA CUDA，普通模式建议 12 GB 显存；不要把 H100 性能声明当消费级显卡实测。Windows 可在现有 WSL2 Ubuntu 中安装独立虚拟环境，不修改用户其他项目或停止已有服务。检查 WSL 内 `nvidia-smi`、可用存储、CUDA 与 GPU 显存后再开始；跑之前检查其他任务是否占用设备。

本次方案：官方代码固定提交 `daa6cb2efe5471f09369229f322d20bb956cb3c3`；官方模型固定快照 `3e28c5151381a722f1d8661b4118c298caa77aa4`。原始约 7.7 GB 权重使用官方文件列表和 LFS SHA-256 校验，缺文件或哈希不一致不能用于推理。镜像仅是下载渠道，版本、许可与哈希以官方模型仓库为准。

安装 Python 3.12 独立 venv，按官方 `requirements.txt` 安装 PyTorch 2.9.1 及相应 CUDA 版、torchaudio 和其余依赖；若解析器在新版 Gradio 反复回溯，可试 `gradio<6`，必须通过实际运行验证。先采用 eager，不默认启用需要额外编译的加速组件。

## 运行和验证

官方 `infer.py` 接受本地完整模型目录和 `--text`；无参考的声音设计传 `--instruction` 及 `--cfg-scale 4`。克隆时同时提供 `--ref-audio` 和其准确的 `--ref-text`；再加 instruction 才是参考引导的语音控制。随机种子、输入、版本、设备、输出时长与耗时一并记录。

本机观察：RTX 3080 20 GiB、Ubuntu WSL2、CUDA PyTorch 2.9.1、eager，首个中文音频 9.28 秒，包含模型加载的端到端耗时 221.83 秒，GPU 总显存采样峰值 9320 MiB；复用模型后 5 条声音设计样本生成 6.8–8 秒音频各约 64–83 秒，未装 flash-attn。这些是特定设置的有限样本，不代表实时或通用表现。启动时出现 SoX 可执行文件未找到提示，声音设计与使用 WAV 参考的克隆仍成功；其他模式不能由此推断。

核验 WAV 可解码、非空、有声，并试听判断效果；按实际需要测试中文、英文、情绪控制及合规参考音。文件可读不代表文字准确或音质达标。生成可复现样例、文档和 Skill 后是否上传发布，应按用户明确的范围及平台许可执行。
