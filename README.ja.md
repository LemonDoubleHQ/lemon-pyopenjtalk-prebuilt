# lemon-pyopenjtalk-prebuilt

[![PyPI](https://img.shields.io/pypi/v/lemon-pyopenjtalk-prebuilt.svg)](https://pypi.python.org/pypi/lemon-pyopenjtalk-prebuilt)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE.md)

**言語 / Language:** [한국어](README.md) | [English](README.en.md) | 日本語 | [中文](README.zh.md)

---

[pyopenjtalk](https://github.com/r9y9/pyopenjtalk) のビルド済みバイナリ wheel パッケージです。
pyopenjtalk は日本語 TTS エンジン [OpenJTalk](http://open-jtalk.sp.nitech.ac.jp/) の Python ラッパーです。

オリジナルの `pyopenjtalk` はインストール時に CMake・C++ コンパイラ・Cython などのビルドツールが必要です。
このパッケージは**ビルド済み wheel** を提供するため、ビルドツールなしで即インストールでき、**Python 3.10 以上**の最新バージョンに対応しています。

## インストール

```bash
pip install lemon-pyopenjtalk-prebuilt
```

## 使い方

`pyopenjtalk` と完全に同じ API を提供します — モジュール名はそのまま `pyopenjtalk` です:

```python
import pyopenjtalk
from scipy.io import wavfile
import numpy as np

# TTS (テキスト → 音声)
x, sr = pyopenjtalk.tts("おめでとうございます")
wavfile.write("output.wav", sr, x.astype(np.int16))

# G2P (Grapheme-to-Phoneme、読み変換)
pyopenjtalk.g2p("こんにちは")           # → 'k o N n i ch i w a'
pyopenjtalk.g2p("こんにちは", kana=True) # → 'コンニチワ'
```

詳細な使い方は [オリジナル pyopenjtalk の README](https://github.com/r9y9/pyopenjtalk) を参照してください。

## 対応プラットフォーム

| プラットフォーム | アーキテクチャ | Python バージョン |
|-----------------|-------------|-----------------|
| Linux           | x86_64      | 3.10 以上        |
| Windows         | AMD64       | 3.10 以上        |

新しい Python バージョンは毎月自動検出され、プルリクエストで追加されます。

## CI/CD ワークフロー

### Build and Release Wheels (`build_and_release.yml`)

バージョンタグ (`v*`) のプッシュ、またはマニュアル実行時に動作します。

| ステップ | 説明 |
|---------|------|
| **Build wheels** | Ubuntu・macOS (Intel/Apple Silicon)・Windows で cibuildwheel を使い各プラットフォーム向け wheel をビルド |
| **Build sdist** | ソース配布物 (`.tar.gz`) をビルド |
| **Publish** | タグプッシュ時に OIDC Trusted Publisher 方式で PyPI へ自動公開 |

ビルド環境:

| プラットフォーム | 環境 | 備考 |
|-----------------|------|------|
| Linux | manylinux_2_28 (x86_64) | glibc 2.28 ベースコンテナ |
| Windows | AMD64 | |

### Check for new Python versions (`check_new_python.yml`)

毎月 1 日に自動実行されます。手動実行も可能です。

[endoflife.date](https://endoflife.date/python) から現在サポート中の Python バージョンを取得し、
`pyproject.toml` のビルド対象に不足しているバージョンがあれば自動でプルリクエストを作成します。

## 作った理由

- `pyopenjtalk` — ビルド済み wheel なし（ソースビルドのみ）
- `pyopenjtalk-prebuilt` — Python 3.11 でアップデート停止
- このパッケージは Python 3.10 以上を対象にビルド済み wheel を提供し、月次の自動バージョンチェックで最新 Python を継続サポートします。

## ライセンス

- **lemon-pyopenjtalk-prebuilt**: MIT License
- **pyopenjtalk**: MIT License ([LICENSE.md](LICENSE.md)) — © Ryuichi Yamamoto
- **Open JTalk**: Modified BSD License ([COPYING](https://github.com/r9y9/open_jtalk/blob/1.10/src/COPYING))
- **hts_engine_API**: Modified BSD License
- **marine** (オプション): Apache 2.0 License

## 謝辞

コアライブラリのすべての功績は [r9y9](https://github.com/r9y9) と HTS Working Group にあります。
このリポジトリはオリジナルの pyopenjtalk にビルド済み wheel 配布機能を追加したものです。
