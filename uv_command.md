# uv Command Reference

`uv`는 Rust로 작성된 매우 빠른 Python 패키지 및 프로젝트 관리 도구입니다 (제작: Astral). `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `virtualenv` 등을 대체할 수 있습니다.

---

## 설치

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# pip / pipx 로 설치
pip install uv
pipx install uv

# Homebrew
brew install uv
```

```bash
# uv 자체 업데이트
uv self update

# 버전 확인
uv --version
```

---

## 프로젝트 관리 (`uv init`, `uv add`, `uv sync` ...)

| 명령어 | 설명 |
| --- | --- |
| `uv init <name>` | 새 프로젝트 생성 |
| `uv init --lib <name>` | 라이브러리 프로젝트 생성 |
| `uv init --app <name>` | 애플리케이션 프로젝트 생성 |
| `uv add <pkg>` | 의존성 추가 (pyproject.toml + lock 갱신) |
| `uv add <pkg> --dev` | 개발 의존성으로 추가 |
| `uv add <pkg>==1.2.3` | 버전 지정 추가 |
| `uv add -r requirements.txt` | requirements 파일에서 추가 |
| `uv remove <pkg>` | 의존성 제거 |
| `uv sync` | lock 파일 기준으로 환경 동기화 |
| `uv sync --all-extras` | 모든 extras 포함 동기화 |
| `uv lock` | lock 파일 생성/갱신 |
| `uv lock --upgrade` | 모든 의존성 업그레이드 |
| `uv lock --upgrade-package <pkg>` | 특정 패키지만 업그레이드 |
| `uv tree` | 의존성 트리 출력 |

```bash
# 예시: 새 프로젝트 만들고 패키지 추가
uv init myproject
cd myproject
uv add requests fastapi
uv add --dev pytest ruff
```

---

## 코드 실행 (`uv run`)

```bash
# 프로젝트 환경에서 스크립트 실행
uv run python main.py
uv run main.py

# 모듈/도구 실행
uv run pytest
uv run ruff check .

# 일회성 의존성과 함께 실행
uv run --with requests python script.py

# 인라인 스크립트 메타데이터(PEP 723) 자동 처리
uv run script.py
```

`uv run`은 실행 전에 환경이 lock 파일과 맞는지 자동으로 확인/동기화합니다.

---

## 가상환경 (`uv venv`)

```bash
# .venv 생성
uv venv

# 이름/경로 지정
uv venv myenv

# 특정 Python 버전으로 생성
uv venv --python 3.12

# 활성화 (macOS/Linux)
source .venv/bin/activate

# 활성화 (Windows PowerShell)
.venv\Scripts\Activate.ps1
```

---

## 패키지 설치 (pip 호환 인터페이스)

`uv pip`은 익숙한 `pip` 명령을 거의 그대로 제공하되 훨씬 빠릅니다.

```bash
uv pip install requests
uv pip install -r requirements.txt
uv pip install -e .                 # editable 설치
uv pip uninstall requests
uv pip list                         # 설치된 패키지 목록
uv pip show requests                # 패키지 정보
uv pip freeze                       # freeze 출력
```

### 의존성 컴파일 (pip-tools 대체)

```bash
# requirements.in -> requirements.txt 로 lock
uv pip compile requirements.in -o requirements.txt

# pyproject.toml 기준 컴파일
uv pip compile pyproject.toml -o requirements.txt

# 환경을 파일과 정확히 일치시키기
uv pip sync requirements.txt
```

---

## Python 버전 관리 (`uv python`)

```bash
uv python list                 # 사용 가능/설치된 Python 목록
uv python install 3.12         # 특정 버전 설치
uv python install 3.11 3.12    # 여러 버전 설치
uv python pin 3.12             # 프로젝트에 버전 고정 (.python-version)
uv python find                 # 현재 사용될 Python 경로 찾기
uv python uninstall 3.11       # 버전 제거
```

---

## 도구 실행/설치 (`uv tool`, `uvx`)

`pipx`를 대체합니다.

```bash
# 설치 없이 일회성 실행 (uvx = uv tool run)
uvx ruff check .
uvx black .
uv tool run ruff

# 전역 도구로 설치
uv tool install ruff
uv tool install "black[d]"

# 관리
uv tool list                   # 설치된 도구 목록
uv tool upgrade ruff           # 업그레이드
uv tool upgrade --all          # 전체 업그레이드
uv tool uninstall ruff         # 제거
```

---

## 빌드 & 배포 (`uv build`, `uv publish`)

```bash
uv build                       # sdist + wheel 빌드 (dist/)
uv build --wheel               # wheel 만
uv build --sdist               # sdist 만

uv publish                     # PyPI 업로드
uv publish --token <TOKEN>     # 토큰 지정
uv publish --index testpypi    # 특정 인덱스로 업로드
```

---

## 캐시 관리 (`uv cache`)

```bash
uv cache dir                   # 캐시 디렉터리 경로
uv cache clean                 # 캐시 전체 삭제
uv cache clean <pkg>           # 특정 패키지 캐시 삭제
uv cache prune                 # 불필요한 캐시 정리
```

---

## 자주 쓰는 전역 옵션

| 옵션 | 설명 |
| --- | --- |
| `--python <ver>` | 사용할 Python 버전/경로 지정 |
| `--verbose`, `-v` | 상세 로그 |
| `--quiet`, `-q` | 출력 최소화 |
| `--offline` | 네트워크 없이 캐시만 사용 |
| `--no-cache` | 캐시 미사용 |
| `--index-url <url>` | 패키지 인덱스 URL 지정 |
| `--help`, `-h` | 도움말 |

---

## 유용한 환경 변수

| 환경 변수 | 설명 |
| --- | --- |
| `UV_PYTHON` | 기본 Python 버전 지정 |
| `UV_INDEX_URL` | 기본 인덱스 URL |
| `UV_CACHE_DIR` | 캐시 디렉터리 위치 |
| `UV_NO_CACHE` | 캐시 비활성화 |
| `UV_SYSTEM_PYTHON` | 시스템 Python 사용 허용 |
| `VIRTUAL_ENV` | 대상 가상환경 경로 |

---

## 빠른 시작 워크플로우 예시

```bash
# 1. 프로젝트 생성
uv init my-app && cd my-app

# 2. Python 버전 고정
uv python pin 3.12

# 3. 의존성 추가
uv add fastapi uvicorn
uv add --dev pytest ruff

# 4. 코드 실행
uv run uvicorn main:app --reload

# 5. 테스트
uv run pytest

# 6. 배포용 빌드
uv build
```

---

> 공식 문서: https://docs.astral.sh/uv/
