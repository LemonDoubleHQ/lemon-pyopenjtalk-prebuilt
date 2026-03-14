# lemon-pyopenjtalk-prebuilt

[![PyPI](https://img.shields.io/pypi/v/lemon-pyopenjtalk-prebuilt.svg)](https://pypi.python.org/pypi/lemon-pyopenjtalk-prebuilt)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE.md)

Prebuilt binary wheels for [pyopenjtalk](https://github.com/r9y9/pyopenjtalk) — a Python wrapper for [OpenJTalk](http://open-jtalk.sp.nitech.ac.jp/).

The original `pyopenjtalk` requires CMake, C++ compiler, and Cython to build from source.
This package provides **prebuilt wheels** so you can install without any build tools, and supports **Python 3.10+** including the latest versions.

## Installation

```bash
pip install lemon-pyopenjtalk-prebuilt
```

## Usage

Drop-in replacement for `pyopenjtalk` — the module name stays the same:

```python
import pyopenjtalk
from scipy.io import wavfile
import numpy as np

# TTS
x, sr = pyopenjtalk.tts("おめでとうございます")
wavfile.write("output.wav", sr, x.astype(np.int16))

# Grapheme-to-Phoneme
pyopenjtalk.g2p("こんにちは")           # → 'k o N n i ch i w a'
pyopenjtalk.g2p("こんにちは", kana=True) # → 'コンニチワ'
```

For full documentation and advanced usage, see the [original pyopenjtalk README](https://github.com/r9y9/pyopenjtalk).

## Supported Platforms

| Platform | Architecture | Python |
|----------|-------------|--------|
| Linux    | x86_64      | 3.10 ~ latest |
| macOS    | x86_64, arm64 | 3.10 ~ latest |
| Windows  | AMD64       | 3.10 ~ latest |

New Python versions are automatically detected monthly and added via pull request.

## Motivation

- `pyopenjtalk` has no prebuilt wheels at all (source-only)
- `pyopenjtalk-prebuilt` stopped updating at Python 3.11
- This package maintains prebuilt wheels for Python 3.10+ with automated monthly version checks

## License

- **lemon-pyopenjtalk-prebuilt**: MIT License
- **pyopenjtalk**: MIT License ([LICENSE.md](LICENSE.md)) — © Ryuichi Yamamoto
- **Open JTalk**: Modified BSD License ([COPYING](https://github.com/r9y9/open_jtalk/blob/1.10/src/COPYING))
- **hts_engine_API**: Modified BSD License
- **marine** (optional): Apache 2.0 License

## Acknowledgements

All credit for the core library goes to [r9y9](https://github.com/r9y9) and the HTS Working Group.
This repository only adds prebuilt wheel distribution on top of the original work.
