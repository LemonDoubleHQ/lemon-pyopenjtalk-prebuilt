# lemon-pyopenjtalk-prebuilt

[![PyPI](https://img.shields.io/pypi/v/lemon-pyopenjtalk-prebuilt.svg)](https://pypi.python.org/pypi/lemon-pyopenjtalk-prebuilt)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE.md)

**语言 / Language:** [한국어](README.md) | [English](README.en.md) | [日本語](README.ja.md) | 中文

---

[pyopenjtalk](https://github.com/r9y9/pyopenjtalk) 的预编译二进制 wheel 包。
pyopenjtalk 是日语 TTS 引擎 [OpenJTalk](http://open-jtalk.sp.nitech.ac.jp/) 的 Python 封装库。

原版 `pyopenjtalk` 在安装时需要 CMake、C++ 编译器、Cython 等构建工具。
本包提供**预编译 wheel**，无需任何构建工具即可直接安装，支持 **Python 3.10 及以上**版本。

## 安装

```bash
pip install lemon-pyopenjtalk-prebuilt
```

## 使用方法

提供与 `pyopenjtalk` 完全相同的 API — 模块名仍为 `pyopenjtalk`：

```python
import pyopenjtalk
from scipy.io import wavfile
import numpy as np

# TTS（文本 → 语音）
x, sr = pyopenjtalk.tts("おめでとうございます")
wavfile.write("output.wav", sr, x.astype(np.int16))

# G2P（字形转音素）
pyopenjtalk.g2p("こんにちは")           # → 'k o N n i ch i w a'
pyopenjtalk.g2p("こんにちは", kana=True) # → 'コンニチワ'
```

更多使用细节请参阅 [原版 pyopenjtalk README](https://github.com/r9y9/pyopenjtalk)。

## 支持平台

| 平台    | 架构    | Python 版本 |
|---------|--------|-------------|
| Linux   | x86_64 | 3.10+       |
| Windows | AMD64  | 3.10+       |

每月自动检测新 Python 版本并通过 Pull Request 添加。

## CI/CD 工作流

### Build and Release Wheels (`build_and_release.yml`)

在版本标签（`v*`）推送或手动触发时运行。

| 步骤 | 说明 |
|------|------|
| **Build wheels** | 使用 cibuildwheel 在 Ubuntu、macOS（Intel/Apple Silicon）、Windows 上构建各平台 wheel |
| **Build sdist** | 构建源码发行包（`.tar.gz`） |
| **Publish** | 标签推送时通过 OIDC Trusted Publisher 自动发布至 PyPI |

构建环境：

| 平台 | 环境 | 备注 |
|------|------|------|
| Linux | manylinux_2_28 (x86_64) | 基于 glibc 2.28 的容器 |
| Windows | AMD64 | |

### Check for new Python versions (`check_new_python.yml`)

每月 1 日自动运行，也可手动触发。

从 [endoflife.date](https://endoflife.date/python) 获取当前受支持的 Python 版本，
若 `pyproject.toml` 的构建目标中缺少某个版本，则自动创建 Pull Request。

## 创建原因

- `pyopenjtalk` — 无预编译 wheel（仅支持源码构建）
- `pyopenjtalk-prebuilt` — 在 Python 3.11 后停止更新
- 本包为 Python 3.10+ 提供预编译 wheel，并通过每月自动版本检查持续支持最新 Python 版本。

## 许可证

- **lemon-pyopenjtalk-prebuilt**: MIT License
- **pyopenjtalk**: MIT License ([LICENSE.md](LICENSE.md)) — © Ryuichi Yamamoto
- **Open JTalk**: Modified BSD License ([COPYING](https://github.com/r9y9/open_jtalk/blob/1.10/src/COPYING))
- **hts_engine_API**: Modified BSD License
- **marine**（可选）: Apache 2.0 License

## 致谢

核心库的所有功劳归属于 [r9y9](https://github.com/r9y9) 与 HTS Working Group。
本仓库仅在原版 pyopenjtalk 基础上添加了预编译 wheel 分发功能。
