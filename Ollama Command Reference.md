# Ollama Command Reference

로컬에서 LLM을 실행·관리하기 위한 Ollama CLI 명령어 정리입니다.

## 목차
- [설치 및 버전](#설치-및-버전)
- [서버 실행](#서버-실행)
- [모델 실행 및 대화](#모델-실행-및-대화)
- [모델 관리](#모델-관리)
- [커스텀 모델 (Modelfile)](#커스텀-모델-modelfile)
- [REST API](#rest-api)
- [주요 환경 변수](#주요-환경-변수)
- [자주 쓰는 모델](#자주-쓰는-모델)

---

## 설치 및 버전

| 명령어 | 설명 |
| --- | --- |
| `ollama --version` | 설치된 Ollama 버전 확인 |
| `ollama help` | 전체 명령어 도움말 |
| `ollama <command> --help` | 특정 명령어 도움말 |

**설치**
- macOS / Windows: [ollama.com/download](https://ollama.com/download) 에서 설치 프로그램 실행
- Linux: `curl -fsSL https://ollama.com/install.sh | sh`

---

## 서버 실행

| 명령어 | 설명 |
| --- | --- |
| `ollama serve` | Ollama 백그라운드 서버 수동 실행 (기본 포트 `11434`) |

> 데스크톱 앱 설치 시 서버는 자동으로 실행됩니다. CLI만 사용할 때 또는 환경 변수를 바꿔 띄울 때 `ollama serve`를 사용합니다.

---

## 모델 실행 및 대화

| 명령어 | 설명 |
| --- | --- |
| `ollama run <model>` | 모델을 내려받고(없으면) 대화형 세션 시작 |
| `ollama run <model> "프롬프트"` | 한 번만 질문하고 결과 출력 |
| `ollama run <model> --verbose` | 응답과 함께 토큰/속도 통계 출력 |
| `echo "질문" \| ollama run <model>` | 파이프로 입력 전달 |
| `ollama run <model> "이미지 설명" ./img.png` | 멀티모달 모델에 이미지 전달 |

**대화 세션 내 명령어** (`ollama run` 실행 중)

| 입력 | 설명 |
| --- | --- |
| `/?` | 세션 명령어 도움말 |
| `/set system "..."` | 시스템 프롬프트 설정 |
| `/show info` | 현재 모델 정보 출력 |
| `/clear` | 대화 컨텍스트 초기화 |
| `/bye` 또는 `Ctrl+D` | 세션 종료 |

---

## 모델 관리

| 명령어 | 설명 |
| --- | --- |
| `ollama list` | 로컬에 받은 모델 목록 |
| `ollama ps` | 현재 메모리에 로드되어 실행 중인 모델 |
| `ollama pull <model>` | 모델만 내려받기 (실행 X) |
| `ollama push <model>` | 모델을 레지스트리에 업로드 |
| `ollama cp <src> <dest>` | 모델 복제 |
| `ollama rm <model>` | 모델 삭제 |
| `ollama show <model>` | 모델 상세 정보 (파라미터, 템플릿 등) |
| `ollama stop <model>` | 메모리에 로드된 모델 언로드 |

---

## 커스텀 모델 (Modelfile)

`Modelfile`을 작성해 기존 모델에 시스템 프롬프트·파라미터를 입힌 커스텀 모델을 만들 수 있습니다.

**Modelfile 예시**
```dockerfile
FROM llama3.2

# 샘플링 파라미터
PARAMETER temperature 0.7
PARAMETER num_ctx 4096

# 시스템 프롬프트
SYSTEM """
당신은 간결하게 한국어로 답하는 비서입니다.
"""
```

**빌드 및 실행**
```bash
ollama create my-assistant -f ./Modelfile
ollama run my-assistant
```

**자주 쓰는 Modelfile 지시어**

| 지시어 | 설명 |
| --- | --- |
| `FROM` | 베이스 모델 (필수) |
| `SYSTEM` | 시스템 프롬프트 |
| `PARAMETER` | 샘플링 파라미터 (`temperature`, `top_p`, `num_ctx` 등) |
| `TEMPLATE` | 프롬프트 템플릿 |
| `ADAPTER` | LoRA 어댑터 적용 |

---

## REST API

Ollama는 기본적으로 `http://localhost:11434`에서 REST API를 제공합니다.

**텍스트 생성 (`/api/generate`)**
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "하늘이 파란 이유는?",
  "stream": false
}'
```

**채팅 (`/api/chat`)**
```bash
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "안녕!" }
  ],
  "stream": false
}'
```

**주요 엔드포인트**

| 엔드포인트 | 설명 |
| --- | --- |
| `POST /api/generate` | 단일 프롬프트 생성 |
| `POST /api/chat` | 멀티턴 채팅 |
| `POST /api/embeddings` | 임베딩 생성 |
| `GET /api/tags` | 로컬 모델 목록 |
| `GET /api/ps` | 실행 중인 모델 |

> OpenAI 호환 엔드포인트도 지원합니다: `http://localhost:11434/v1`

---

## 주요 환경 변수

| 변수 | 설명 | 예시 |
| --- | --- | --- |
| `OLLAMA_HOST` | 서버 바인딩 주소/포트 | `0.0.0.0:11434` |
| `OLLAMA_MODELS` | 모델 저장 경로 | `D:\ollama\models` |
| `OLLAMA_KEEP_ALIVE` | 모델 메모리 유지 시간 | `5m`, `-1`(무제한) |
| `OLLAMA_NUM_PARALLEL` | 동시 처리 요청 수 | `4` |
| `OLLAMA_MAX_LOADED_MODELS` | 동시에 로드할 모델 수 | `2` |

**Windows (PowerShell) 설정 예시**
```powershell
$env:OLLAMA_HOST = "0.0.0.0:11434"
ollama serve
```

---

## 자주 쓰는 모델

| 모델 | 명령어 | 비고 |
| --- | --- | --- |
| Llama 3.2 | `ollama run llama3.2` | 범용, 경량 |
| Gemma 3 | `ollama run gemma3` | Google 경량 모델 |
| Qwen 3 | `ollama run qwen3` | 다국어 강점 |
| Phi-4 | `ollama run phi4` | 소형 고효율 |
| Mistral | `ollama run mistral` | 범용 |
| DeepSeek-R1 | `ollama run deepseek-r1` | 추론 특화 |
| nomic-embed-text | `ollama pull nomic-embed-text` | 임베딩 전용 |

> 모델 크기 변형은 태그로 지정: `ollama run llama3.2:1b`, `ollama run qwen3:14b` 등.
> 전체 목록은 [ollama.com/library](https://ollama.com/library) 참고.
