# llm-security-lab

> **LLM · RAG 기반 AI 보안 실습** — Wins AI 교육과정에서 다룬 내용을 노트북으로 정리한 저장소입니다.

OpenAI·Gemini·Ollama 등 여러 LLM을 직접 호출해 보는 기초부터, CVE/CWE 보안 데이터를 활용한
RAG(검색 증강 생성) 파이프라인 구축까지 단계별로 담았습니다.

<p>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.13-3776AB?logo=python&logoColor=white">
  <img alt="Jupyter" src="https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white">
  <img alt="uv" src="https://img.shields.io/badge/packaging-uv-DE5FE9">
  <img alt="ChromaDB" src="https://img.shields.io/badge/VectorDB-ChromaDB-0C7D6E">
</p>

---

## 다루는 내용

### Day 1 — LLM 기초 다지기
여러 LLM을 직접 호출하며 동작 원리와 파라미터를 익힙니다.

| 주제 | 노트북 | 내용 |
| --- | --- | --- |
| OpenAI 호출 | `src/day1/1_1_openai.ipynb` | OpenAI API 기본 호출 |
| 샘플링 파라미터 | `src/day1/1_1_2_temperature.ipynb`, `src/day1/1_1_2_temp_maxtoken.ipynb` | temperature · max_token 영향 비교 |
| Gemini | `src/day1/1_2_gemini.ipynb` | Google Gemini 호출 |
| 로컬 LLM | `src/day1/1_3_ollama.ipynb`, `src/day1/1_3_2_qwen.ipynb` | Ollama · Qwen 로컬 실행 |
| 모델 비교 | `src/day1/1_4_llms.ipynb` | 같은 프롬프트에 대한 모델별 응답 비교 |
| 토크나이저 | `src/day1/1_5_tokenizer.ipynb` | 토큰화 방식과 토큰 수 확인 |
| 대화 상태 | `src/day1/1_6_stateless.ipynb`, `src/day1/1_6_2_stateful.ipynb` | stateless vs stateful 대화 관리 |
| 컨텍스트 | `src/day1/1_7_context_openai.ipynb` | 대화 맥락 유지 |
| 보안 모델 | `src/day1/ann_security_ko.ipynb` | PyTorch ANN 기반 보안 비용 회귀 모델 |

### Day 2 — RAG 파이프라인
청킹·임베딩·벡터 검색을 거쳐 보안 도메인 RAG까지 구축합니다.

| 주제 | 경로 | 내용 |
| --- | --- | --- |
| 청킹 기초 | `src/day2/chunk_basic_ko*.ipynb` | 문서 분할 전략 |
| RAG 기초 | `src/day2/rag_basic_ko.ipynb`, `rag_basic_en.ipynb` | ChromaDB 기반 기본 RAG |
| 보안 RAG (1단계) | `src/day2/security_rag/` | CVE ID → CWE 문서 검색 (교육용) |
| 보안 RAG (2단계) | `src/day2/security_rag_advance/` | CWE + 벤더 어드바이저리·KEV·EPSS 결합 (대응 판단용) |

> 보안 RAG는 "이건 어떤 유형의 취약점인가"(1단계)에서 "내 버전이 영향받나, 어느 버전으로 올려야 하나,
> 지금 공격에 쓰이고 있나"(2단계)까지 답하도록 발전시킵니다. 자세한 흐름은 각 폴더의
> `flow.md` / `README.md`를 참고하세요.

---

## 시작하기

### 1. 요구 사항
- Python 3.13 이상
- [uv](https://docs.astral.sh/uv/) (패키지 · 가상환경 관리)
- (선택) 로컬 LLM 실행을 위한 [Ollama](https://ollama.com/download)

### 2. 설치
```bash
git clone https://github.com/OhSoomin812/llm-security-lab.git
cd llm-security-lab
uv sync
```

### 3. 환경 변수
API를 사용하는 노트북은 키가 필요합니다. 저장소 루트에 `.env` 파일을 만들어 주세요.
```dotenv
OPENAI_API_KEY=sk-...
GOOGLE_API_KEY=...
```

### 4. 실행
```bash
uv run jupyter lab
```
또는 VS Code / Cursor에서 `.ipynb`를 열어 커널을 `.venv`로 지정해 실행합니다.

---

## 기술 스택
`openai` · `google-genai` · Ollama · `tiktoken` · `torch` · `chromadb` · `pandas` · `matplotlib` · `gradio`

## 참고 문서
- [`Ollama Command Reference.md`](./Ollama%20Command%20Reference.md) — Ollama CLI 명령어 정리
- [`uv_command.md`](./uv_command.md) — uv 자주 쓰는 명령어
- [`src/day1/comparison.md`](./src/day1/comparison.md) — 모델별 응답 비교 결과

---

## 라이선스 · 안내
학습 목적으로 작성한 개인 실습 저장소입니다. 보안 데이터(CVE/CWE/어드바이저리)는 공개 출처를
가공한 것으로, 실제 대응 판단 시에는 공식 출처를 함께 확인하세요.
