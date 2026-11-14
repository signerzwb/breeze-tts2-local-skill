# Breeze TTS 2 本地部署与试听研究

神都猫整理的 Breeze TTS 2 部署记录与 Codex Skill，适合希望在 NVIDIA 显卡上复现中文、英文声音设计和语音控制测试的读者。

## 重要：模型及音频许可

[BreezeBlue 官方模型与许可](https://huggingface.co/BreezeBlue/Breeze-TTS-2)：代码为 Apache-2.0；模型权重、衍生模型及自托管生成内容使用 BreezeBlue Research and Non-Commercial License，仅限研究及非商业用途。**代码开源不等于模型或音频可商用。**非商业展示请遵守原许可、注明合成与出处；商业使用须另获授权。本项目不包含模型权重。

## 内容

- [本地部署 Skill](skills/breeze-tts2-local/SKILL.md)：安装、验证、模型文件、测试与许可注意事项。
- [官方代码和推理方式](https://github.com/breezeblue-ai/breeze-tts)
- [官方模型权重和模型卡](https://huggingface.co/BreezeBlue/Breeze-TTS-2)

## 首次本地测试

设备是 Windows 主机上的 NVIDIA RTX 3080 20 GiB，使用 WSL2 Ubuntu、Python 3.12、PyTorch 2.9.1+cu128 及官方普通推理路径。首个中文声音设计样本成功输出 9.28 秒、24 kHz、单声道 WAV；单次端到端（包含首次模型加载）约 221.83 秒，GPU 总使用峰值采样约 9320 MiB。复用模型后另外五条声音设计样本各约 64–83 秒，生成 6.8–8 秒音频；不等于实时。这是特定机器和有限样本下的观察，不能当通用速度、最低配置、内容准确率或音质保证。

本次另生成两条以合成音频为参考的声音克隆／语气引导样例，并用同一参考音和文本生成了一条 IndexTTS 2.5 对照。两款模型后端、环境和默认参数不同，这些样本只用于试听，不构成公平的模型性能排名。样本、文本、实际参数和许可见仓库 Release。

模型快照 `3e28c5151381a722f1d8661b4118c298caa77aa4`，官方代码提交 `daa6cb2efe5471f09369229f322d20bb956cb3c3`。文档和 Skill 是独立整理；具体模型与代码归其各自权利人所有。
