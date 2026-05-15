# 기본 통합 예시

NanoGPT를 Hermes AI에 통합하는 실제 설정 예시입니다.

---

## 예시 1: 최소 설정

```yaml
# ~/.hermes/config.yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - deepseek/deepseek-v4-flash
```

```bash
# ~/.hermes/.env
NANOGPT_API_KEY=sk-nano-여기에-키-입력
```

---

## 예시 2: 다중 모델 설정 (추천)

```yaml
# ~/.hermes/config.yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      # 에이전트 모드 (tool calling 지원)
      - deepseek/deepseek-v4-flash
      - deepseek/deepseek-v4-pro
      - xiaomi/mimo-v2.5-pro
      - moonshotai/kimi-k2.6
      - minimax/minimax-m2.7
      # 추론 모드
      - deepseek/deepseek-v4-flash:thinking
      - deepseek/deepseek-v4-pro:thinking
      - moonshotai/kimi-k2.6:thinking
      - zai-org/glm-5.1:thinking
      # 롤플레이/창작
      - Gemma-4-31B-DarkIdol
      - Qwen3.5-27B-Queen-Derestricted

model:
  default: "nanogpt:deepseek/deepseek-v4-flash"
```

---

## 예시 3: 기본 모델 포함 설정

```yaml
# ~/.hermes/config.yaml
model:
  default: "nanogpt:deepseek/deepseek-v4-flash"

providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      - deepseek/deepseek-v4-flash
      - deepseek/deepseek-v4-pro
      - xiaomi/mimo-v2.5-pro
      - moonshotai/kimi-k2.6
```

---

## API 연결 테스트

### 1. 환경 변수 확인
```bash
echo $NANOGPT_API_KEY
# sk-nano-xxxx-xxxx 형태로 출력되어야 함
```

### 2. 모델 목록 조회
```bash
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer $NANOGPT_API_KEY" \
  | python3 -c "import sys,json; d=json.load(sys.stdin); print(len(d.get('data',[])), '개 모델')"
```

### 3. 채팅 완성 테스트
```bash
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer $NANOGPT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4-flash",
    "messages": [{"role": "user", "content": "안녕하세요! 짧게 인사해주세요."}],
    "max_tokens": 50
  }' | python3 -c "
import sys, json
data = json.load(sys.stdin)
print(data['choices'][0]['message']['content'])
"
```

### 4. Hermes에서 전환 테스트
```
/model nanogpt:deepseek/deepseek-v4-flash
안녕하세요!
```

정상 응답이 오면 설정이 완료된 것입니다.

---

**관련 문서**: [SETUP_GUIDE.md](../docs/SETUP_GUIDE.md) | [TROUBLESHOOTING.md](../docs/TROUBLESHOOTING.md)
