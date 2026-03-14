# lemon-pyopenjtalk-prebuilt

[![PyPI](https://img.shields.io/pypi/v/lemon-pyopenjtalk-prebuilt.svg)](https://pypi.python.org/pypi/lemon-pyopenjtalk-prebuilt)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE.md)

**Language:** [한국어](README.md) | English | [日本語](README.ja.md) | [中文](README.zh.md)

---

Prebuilt binary wheel package for [pyopenjtalk](https://github.com/r9y9/pyopenjtalk).
pyopenjtalk is a Python wrapper for the Japanese TTS engine [OpenJTalk](http://open-jtalk.sp.nitech.ac.jp/).

The original `pyopenjtalk` requires build tools such as CMake, a C++ compiler, and Cython at install time.
This package provides **prebuilt wheels** so you can install without any build tools, supporting **Python 3.10 and above**.

## Installation

```bash
pip install lemon-pyopenjtalk-prebuilt
```

## Usage

Provides the exact same API as `pyopenjtalk` — the module name stays `pyopenjtalk`:

```python
import pyopenjtalk
from scipy.io import wavfile
import numpy as np

# TTS (text → speech)
x, sr = pyopenjtalk.tts("おめでとうございます")
wavfile.write("output.wav", sr, x.astype(np.int16))

# G2P (Grapheme-to-Phoneme)
pyopenjtalk.g2p("こんにちは")           # → 'k o N n i ch i w a'
pyopenjtalk.g2p("こんにちは", kana=True) # → 'コンニチワ'
```

For more details, see the [original pyopenjtalk README](https://github.com/r9y9/pyopenjtalk).

## Supported Platforms

| Platform | Architecture   | Python Version |
|----------|----------------|----------------|
| Linux    | x86_64         | 3.10+          |
| macOS    | x86_64, arm64  | 3.10+          |
| Windows  | AMD64          | 3.10+          |

New Python versions are automatically detected monthly and added via pull request.

## CI/CD Workflows

### Build and Release Wheels (`build_and_release.yml`)

Triggered on version tag push (`v*`) or manual dispatch.

| Step | Description |
|------|-------------|
| **Build wheels** | Builds platform wheels using cibuildwheel on Ubuntu, macOS (Intel/Apple Silicon), and Windows |
| **Build sdist** | Builds a source distribution (`.tar.gz`) |
| **Publish** | Automatically publishes to PyPI via OIDC Trusted Publisher on tag push |

Build environments:

| Platform | Environment | Notes |
|----------|-------------|-------|
| Linux | manylinux_2_28 (x86_64) | glibc 2.28 based container |
| macOS 14 | x86_64, arm64 | x86_64 cross-compiled on arm64 runner |
| Windows | AMD64 | |

### Check for new Python versions (`check_new_python.yml`)

Runs automatically on the 1st of every month, or manually on demand.

Queries currently supported Python versions from [endoflife.date](https://endoflife.date/python)
and automatically opens a pull request if any version is missing from the build targets in `pyproject.toml`.

## Why This Exists

- `pyopenjtalk` — no prebuilt wheels (source build only)
- `pyopenjtalk-prebuilt` — stopped updating at Python 3.11
- This package provides prebuilt wheels for Python 3.10+ with monthly automated version checks to keep up with the latest Python releases.

## License

- **lemon-pyopenjtalk-prebuilt**: MIT License
- **pyopenjtalk**: MIT License ([LICENSE.md](LICENSE.md)) — © Ryuichi Yamamoto
- **Open JTalk**: Modified BSD License ([COPYING](https://github.com/r9y9/open_jtalk/blob/1.10/src/COPYING))
- **hts_engine_API**: Modified BSD License
- **marine** (optional): Apache 2.0 License

## Acknowledgements

All credit for the core libraries goes to [r9y9](https://github.com/r9y9) and the HTS Working Group.
This repository only adds prebuilt wheel distribution on top of the original pyopenjtalk.
