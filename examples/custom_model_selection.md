# 커스텀 모델 선택 코드 예시

상황에 맞는 모델 선택과 설정 예시입니다.

---

## 시나리오 1: 에이전트 모드 (Tool Calling)

Hermes의 파일 읽기, 터미널 실행, 웹 검색 등 핵심 기능을 사용하려면 **tool calling 지원 모델**이 필요합니다.

```yaml
# config.yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - deepseek/deepseek-v4-flash      # ✅ tool calling
      - deepseek/deepseek-v4-pro        # ✅ tool calling
      - xiaomi/mimo-v2.5-pro            # ✅ tool calling
      - moonshotai/kimi-k2.6            # ✅ tool calling
      - minimax/minimax-m2.7            # ✅ tool calling
```

---

## 시나리오 2: 롤플레이 / 창작 전용

제한이 완화된 모델로 자유로운 글쓰기:

```yaml
# config.yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - Gemma-4-31B-DarkIdol
      - Gemma-4-31B-Queen
      - Gemma-4-31B-Cognitive-Unshackled
      - Qwen3.5-27B-Queen-Derestricted
      - Qwen3.5-27B-RpRMax-v1
      - Qwen3.5-27B-NaNovel-Derestricted
```

---

## 시나리오 3: 비용 최적화

토큰 소비를 최소화하면서 품질 유지:

```yaml
# config.yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - deepseek/deepseek-v4-flash           # 빠르고 저렴
      - deepseek/deepseek-v4-pro-cheaper     # Pro 대비 저렴
      - xiaomi/mimo-v2.5-pro                 # 균형 잡힌 성능
model:
  default: "nanogpt:deepseek/deepseek-v4-flash"
```

---

## 시나리오 4: 추론 중심

복잡한 수학, 논리, 코딩 문제에 reasoning 모드 활용:

```yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - deepseek/deepseek-v4-pro:thinking
      - deepseek/deepseek-v4-flash:thinking
      - moonshotai/kimi-k2.6:thinking
      - zai-org/glm-5.1:thinking
```

---

## 모델 검증 스크립트

config에 등록한 모델이 실제로 NanoGPT에서 사용 가능한지 확인:

```bash
#!/bin/bash
# check_models.sh — 등록된 모델이 API에서 사용 가능한지 확인

API_KEY="${NANOGPT_API_KEY}"
BASE_URL="https://nano-gpt.com/api/v1"

# API에서 전체 모델 목록 가져오기
AVAILABLE=$(curl -s "$BASE_URL/models" \
  -H "Authorization: Bearer $API_KEY" \
  | python3 -c "import sys,json; [print(m['id']) for m in json.load(sys.stdin).get('data',[])]")

# 확인할 모델 목록
MODELS=(
  "deepseek/deepseek-v4-flash"
  "xiaomi/mimo-v2.5-pro"
  "moonshotai/kimi-k2.6"
  "Gemma-4-31B-DarkIdol"
)

echo "=== 모델 가용성 확인 ==="
for model in "${MODELS[@]}"; do
  if echo "$AVAILABLE" | grep -q "^${model}$"; then
    echo "✅ $model"
  else
    echo "❌ $model — 사용 불가"
  fi
done
```

---

**관련 문서**: [RECOMMENDED_MODELS.md](../docs/RECOMMENDED_MODELS.md) | [MODELS_SELECTION.md](../docs/MODELS_SELECTION.md)
