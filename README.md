# lemon-pyopenjtalk-prebuilt

[![PyPI](https://img.shields.io/pypi/v/lemon-pyopenjtalk-prebuilt.svg)](https://pypi.python.org/pypi/lemon-pyopenjtalk-prebuilt)
[![License](http://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat)](LICENSE.md)

[pyopenjtalk](https://github.com/r9y9/pyopenjtalk)의 사전 빌드(prebuilt) 바이너리 wheel 패키지입니다.
pyopenjtalk는 일본어 TTS 엔진 [OpenJTalk](http://open-jtalk.sp.nitech.ac.jp/)의 Python 래퍼입니다.

원본 `pyopenjtalk`는 설치 시 CMake, C++ 컴파일러, Cython 등 빌드 도구가 필요합니다.
이 패키지는 **사전 빌드된 wheel**을 제공하여 별도의 빌드 도구 없이 바로 설치할 수 있으며, **Python 3.10 이상**의 최신 버전을 지원합니다.

## 설치

```bash
pip install lemon-pyopenjtalk-prebuilt
```

## 사용법

`pyopenjtalk`와 완전히 동일한 API를 제공합니다 — 모듈명은 그대로 `pyopenjtalk`입니다:

```python
import pyopenjtalk
from scipy.io import wavfile
import numpy as np

# TTS (텍스트 → 음성)
x, sr = pyopenjtalk.tts("おめでとうございます")
wavfile.write("output.wav", sr, x.astype(np.int16))

# G2P (Grapheme-to-Phoneme, 발음 변환)
pyopenjtalk.g2p("こんにちは")           # → 'k o N n i ch i w a'
pyopenjtalk.g2p("こんにちは", kana=True) # → 'コンニチワ'
```

더 자세한 사용법은 [원본 pyopenjtalk README](https://github.com/r9y9/pyopenjtalk)를 참고하세요.

## 지원 플랫폼

| 플랫폼  | 아키텍처        | Python 버전    |
|---------|----------------|----------------|
| Linux   | x86_64         | 3.10 ~ 최신    |
| macOS   | x86_64, arm64  | 3.10 ~ 최신    |
| Windows | AMD64          | 3.10 ~ 최신    |

새로운 Python 버전은 매월 자동으로 감지되어 PR로 추가됩니다.

## 만든 이유

- `pyopenjtalk` — 사전 빌드 wheel 없음 (소스 빌드만 지원)
- `pyopenjtalk-prebuilt` — Python 3.11에서 업데이트 중단
- 이 패키지는 Python 3.10 이상을 대상으로 사전 빌드 wheel을 제공하고, 월간 자동 버전 체크로 최신 Python을 지속 지원합니다.

## 라이선스

- **lemon-pyopenjtalk-prebuilt**: MIT License
- **pyopenjtalk**: MIT License ([LICENSE.md](LICENSE.md)) — © Ryuichi Yamamoto
- **Open JTalk**: Modified BSD License ([COPYING](https://github.com/r9y9/open_jtalk/blob/1.10/src/COPYING))
- **hts_engine_API**: Modified BSD License
- **marine** (선택): Apache 2.0 License

## 감사의 말

핵심 라이브러리의 모든 공로는 [r9y9](https://github.com/r9y9)와 HTS Working Group에 있습니다.
이 저장소는 원본 pyopenjtalk 위에 사전 빌드 wheel 배포 기능만 추가한 것입니다.
