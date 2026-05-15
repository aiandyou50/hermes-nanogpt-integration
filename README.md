# Hermes AI × NanoGPT 통합 가이드

Hermes AI 에이전트에서 NanoGPT를 추가 공급자로 등록하여 600개 이상의 AI 모델을 활용하는 방법을 안내하는 실전 가이드입니다.

## 📖 프로젝트 개요

### NanoGPT란?

**NanoGPT** (https://nano-gpt.com/)는 600개 이상의 AI 모델을 한 플랫폼에서 제공하는 종합 AI 서비스입니다.

**$12/월 멤버십 혜택:**
- 📊 주 60,000,000 토큰 사용 가능
- 🖼️ 매일 100개 이미지 생성
- 🤖 600개 이상의 AI 모델 접근

### Hermes AI와의 통합

**Hermes AI** (https://github.com/NousResearch/hermes-agent)는 오픈소스 AI 에이전트 프레임워크로, 여러 공급자를 지원합니다.

이 가이드는 NanoGPT를 Hermes AI의 새로운 공급자로 추가하여 `/model` 명령어로 모델을 전환하는 방법을 제시합니다.

### 이 가이드가 해결하는 문제

- ✅ NanoGPT의 600+ 모델 중 원하는 모델만 선택하여 등록
- ✅ `config.yaml` 설정부터 문제 해결까지 실전 경험 기반
- ✅ 실제로 발생하는 오류와 해결법 수록
- ✅ 다중 프로필로 모드별 분리 운영

## 📁 파일 구조

```
hermes-nanogpt-integration/
├── README.md                          # 이 파일
├── LICENSE                            # MIT 라이선스
│
├── docs/                              # 핵심 가이드 문서
│   ├── AUTO_SETUP_PROMPT.md           # ⭐ AI 에이전트 자동 설정 프롬프트
│   ├── SETUP_GUIDE.md                # ⭐ NanoGPT 공급자 추가 (시작점)
│   ├── RECOMMENDED_MODELS.md         # ⭐ 추천 모델 27개 목록
│   ├── MODELS_SELECTION.md           # 모델 선택 및 관리
│   ├── QUICK_START.md                # /model 명령어 빠른 시작
│   ├── TROUBLESHOOTING.md            # ⭐ 실전 오류 해결법
│   └── MULTI_PROFILE.md             # 다중 프로필 분리 운영
│
└── examples/                          # 실제 설정 예시
    ├── basic_integration.md           # 최소/추천 설정 예시
    ├── custom_model_selection.md      # 시나리오별 모델 선택
    └── agent_prompt.md               # AI 에이전트 프롬프트 템플릿
```

## ⚡ 원클릭 자동 설정 (추천)

**[`docs/AUTO_SETUP_PROMPT.md`](./docs/AUTO_SETUP_PROMPT.md)**의 내용을 복사하여 AI 에이전트에게 전달하세요. 에이전트가 자동으로:
1. 가이드 레포지토리를 pull/분석
2. 사용자에게 모델 선택 받기
3. API 키 확인
4. config.yaml 자동 수정
5. 연결 검증 + 게이트웨이 재시작

**수동 설정이 필요하면 아래를 따라하세요:**

## 🚀 수동 시작

1. **[SETUP_GUIDE.md](./docs/SETUP_GUIDE.md)** — NanoGPT API 키 획득 + config.yaml 설정
2. **[RECOMMENDED_MODELS.md](./docs/RECOMMENDED_MODELS.md)** — 추천 모델 27개 확인
3. **[QUICK_START.md](./docs/QUICK_START.md)** — `/model nanogpt:모델명` 으로 전환

## ⚠️ 꼭 알아야 할 것

| 항목 | 내용 |
|------|------|
| API 키 필드명 | **`key_env`** (not `api_key_env`) — 틀리면 401 오류 |
| 모델 목록 관리 | **`discover_models: false`** — 안 하면 600+개 모두 로드 |
| 모델 전환 형식 | **`/model nanogpt:모델명`** — 콜론(`:`) 구분자 |

## 📚 문서 안내

| 문서 | 대상 | 설명 |
|------|------|------|
| **AUTO_SETUP_PROMPT.md** | 모두 | ⭐ AI 에이전트에게 전달하는 자동 설정 프롬프트 |
| **SETUP_GUIDE.md** | 초보자 | API 키 → config.yaml 설정 → 검증까지 단계별 |
| **RECOMMENDED_MODELS.md** | 모두 | 카테고리별 검증된 모델 27개 |
| **MODELS_SELECTION.md** | 중급자 | 모델 추가/제거, API 조회, tool calling 확인 |
| **QUICK_START.md** | 모두 | `/model` 명령어와 시나리오별 전환 |
| **TROUBLESHOOTING.md** | 문제 발생 시 | 실전에서 발견한 오류와 해결법 |
| **MULTI_PROFILE.md** | 고급자 | 메인/롤플레이 모드 분리 운영 |

## 📄 라이선스

MIT License

## 🔗 참고 링크

- **NanoGPT**: https://nano-gpt.com/
- **Hermes AI**: https://github.com/NousResearch/hermes-agent

---

**시작하기**: [`docs/SETUP_GUIDE.md`](./docs/SETUP_GUIDE.md)에서 NanoGPT 설정을 시작하세요! 🚀
