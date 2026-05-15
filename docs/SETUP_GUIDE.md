# NanoGPT를 Hermes AI 공급자로 추가하기

Hermes AI에 NanoGPT를 커스텀 공급자로 등록하여 600개 이상의 AI 모델을 활용하는 방법을 안내합니다.

## 전제 조건

- **NanoGPT 구독**: $12/월 멤버십 가입 (주 60,000,000 토큰, 일 100 이미지)
- **Hermes AI**: 로컬 또는 서버에 설치 완료 (`hermes --version`으로 확인)
- **NanoGPT API 키**: 대시보드에서 발급

## 1단계: NanoGPT API 키 획득

1. https://nano-gpt.com/ 접속 후 로그인
2. 대시보드에서 **API Keys** 메뉴 진입
3. **Create New Key** 클릭
4. 생성된 키를 복사 (형식: `sk-nan...xxxx`)

> ⚠️ API 키는 한 번만 표시됩니다. 반드시 안전한 곳에 저장하세요.

## 2단계: 환경 변수 설정

Hermes의 `.env` 파일에 API 키를 추가합니다:

```bash
# ~/.hermes/.env 파일에 추가
NANOGPT_API_KEY=sk-nano-여기에-실제-키-입력
```

> ⚠️ `.env` 파일에 직접 값을 넣어야 합니다. `export` 명령어는 재시작 시 사라집니다.

## 3단계: config.yaml에 공급자 등록

`~/.hermes/config.yaml` 파일을 열고 `providers:` 섹션에 NanoGPT를 추가합니다:

```yaml
# ~/.hermes/config.yaml

providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      # DeepSeek 시리즈
      - deepseek/deepseek-latest
      - deepseek/deepseek-v4-flash
      - deepseek/deepseek-v4-flash:thinking
      - deepseek/deepseek-v4-pro
      - deepseek/deepseek-v4-pro:thinking
      - deepseek/deepseek-v4-pro-cheaper
      - deepseek/deepseek-v4-pro-cheaper:thinking
      # Xiaomi MiMo
      - xiaomi/mimo-v2.5-pro
      # Moonshot Kimi
      - moonshotai/kimi-k2.6
      - moonshotai/kimi-k2.6:thinking
      # GLM
      - zai-org/glm-5.1
      - zai-org/glm-5.1:thinking
      # MiniMax
      - minimax/minimax-m2.7
      # Gemma (커스텀 파인튠)
      - Gemma-4-31B-Cognitive-Unshackled
      - Gemma-4-31B-DarkIdol
      - gemma-4-31B-MeroMero
      - Gemma-4-31B-Queen
      # Qwen (커스텀 파인튠)
      - Qwen3.5-27B-Omega-Evolution-v2.2-Derestricted
      - Qwen3.5-27B-BlueStar-v3-Derestricted
      - Qwen3.5-27B-Infracelestial
      - Qwen3.5-27B-RpRMax-v1
      - Qwen3.5-27B-earica-Derestricted
      - Qwen3.5-27B-Marvin-DPO-V2-Derestricted
      - Qwen3.5-27B-NaNovel-Derestricted
      - Qwen3.5-27B-Queen-Derestricted
      # 기타
      - huihui-ai/DeepSeek-R1-Distill-Qwen-32B-abliterated
      - nousresearch/hermes-3-llama-3.1-70b
```

### ⚠️ 꼭 알아야 할 설정

| 설정 | 값 | 이유 |
|------|-----|------|
| `key_env` | `"NANOGPT_API_KEY"` | **`api_key_env`가 아닙니다!** 이 필드명을 틀리면 401 오류가 발생합니다 |
| `discover_models` | `false` | **안 하면 API의 600+개 모델이 모두 로드되어 목록이혼란됩니다** |
| `base_url` | `"https://nano-gpt.com/api/v1"` | 반드시 `/v1` 포함 |

## 4단계: 연결 확인

### API 키 동작 테스트

```bash
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer *** \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4-flash",
    "messages": [{"role": "user", "content": "Hello"}],
    "max_tokens": 10
  }'
```

정상 응답이 오면 API 키가 올바른 것입니다.

### 모델 목록 확인

```bash
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer *** | python3 -m json.tool | head -20
```

### Hermes에서 모델 전환

게이트웨이를 재시작한 후:

```
/model nanogpt:deepseek/deepseek-v4-flash
```

> 💡 모델명 형식은 `공급자:모델명`입니다. 슬래시(`/`)가 아닌 **콜론(`:`)**으로 구분합니다.

## 5단계: 기본 모델 설정 (선택)

특정 모델을 기본값으로 설정하려면:

```yaml
# ~/.hermes/config.yaml
model:
  default: "nanogpt:deepseek/deepseek-v4-flash"
```

## 다음 단계

- [추천 모델 목록](./RECOMMENDED_MODELS.md) — 카테고리별 검증된 모델
- [모델 선택 가이드](./MODELS_SELECTION.md) — 커스텀 모델 목록 관리
- [트러블슈팅](./TROUBLESHOOTING.md) — 문제 해결

---

**관련 문서**: [README.md](../README.md) | [QUICK_START.md](./QUICK_START.md)
