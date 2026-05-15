# 모델 선택 및 관리 가이드

NanoGPT의 600+ 모델 중 원하는 모델만 선택하여 Hermes AI에 등록하는 방법을 설명합니다.

---

## 핵심: discover_models 설정

Hermes는 기본적으로 공급자 API에서 **전체 모델 목록을 가져와서** 표시합니다. NanoGPT는 600+ 모델이 있으므로, 설정하지 않으면 목록이혼란됩니다.

**반드시 `discover_models: false`를 설정하세요:**

```yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false   # ← 필수
    models:
      - 원하는 모델만 나열
```

---

## 모델 추가/제거 방법

### 1. config.yaml 직접 수정

```bash
# 설정 파일 열기
nano ~/.hermes/config.yaml
```

`providers.nanogpt.models:` 섹션에 모델을 추가하거나 제거합니다:

```yaml
providers:
  nanogpt:
    models:
      # 여기에 원하는 모델만 나열
      - deepseek/deepseek-v4-flash
      - xiaomi/mimo-v2.5-pro
      - moonshotai/kimi-k2.6
      # 새 모델 추가 ↓
      - 새-모델-이름
```

### 2. 게이트웨이 재시작

변경 후 반드시 재시작:
```bash
hermes gateway restart
```

또는 텔레그램에서 `/restart`

---

## NanoGPT에서 사용 가능한 모델 확인

### API로 전체 모델 목록 조회

```bash
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer *** \
  | python3 -c "
import sys, json
data = json.load(sys.stdin)
models = [m['id'] for m in data.get('data', [])]
for m in sorted(models):
    print(m)
print(f'\n총 {len(models)}개 모델')
"
```

### 특정 키워드로 모델 검색

```bash
# DeepSeek 관련 모델만
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer *** \
  | python3 -c "
import sys, json
data = json.load(sys.stdin)
models = [m['id'] for m in data.get('data', []) if 'deepseek' in m['id'].lower()]
for m in sorted(models):
    print(m)
"

# Qwen 관련 모델만
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer *** \
  | python3 -c "
import sys, json
data = json.load(sys.stdin)
models = [m['id'] for m in data.get('data', []) if 'qwen' in m['id'].lower()]
for m in sorted(models):
    print(m)
"
```

---

## 모델 테스트 방법

### 간단한 응답 테스트

```bash
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer *** \
  -H "Content-Type: application/json" \
  -d '{
    "model": "모델명-여기에-입력",
    "messages": [{"role": "user", "content": "Say hello in Korean"}],
    "max_tokens": 50
  }' | python3 -m json.tool
```

### Tool Calling 지원 여부 확인

```bash
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer *** \
  -H "Content-Type: application/json" \
  -d '{
    "model": "모델명-여기에-입력",
    "messages": [{"role": "user", "content": "Search the web for today weather"}],
    "tools": [{"type": "function", "function": {"name": "web_search", "parameters": {"type": "object", "properties": {"query": {"type": "string"}}}}}],
    "max_tokens": 100
  }' | python3 -c "
import sys, json
data = json.load(sys.stdin)
choice = data.get('choices', [{}])[0]
msg = choice.get('message', {})
if msg.get('tool_calls'):
    print('✅ Tool calling 지원')
else:
    print('❌ Tool calling 미지원 (또는 무시됨)')
"
```

> 💡 Tool calling은 Hermes 에이전트의 핵심 기능(파일 읽기, 터미널 실행, 웹 검색 등)에 필수입니다.
> 에이전트 모드로 사용하려면 tool calling 지원 모델을 선택하세요.

---

## :thinking 모델이란?

모델명에 `:thinking`이 붙으면 **reasoning 모드**가 활성화됩니다:

- `deepseek/deepseek-v4-flash` — 일반 모드
- `deepseek/deepseek-v4-flash:thinking` — 추론 모드 (Chain-of-Thought)

**차이점:**
- 추론 모드는 "생각 과정"을 보여주면서 더 깊은 분석 수행
- 응답 시간이 길어지고 토큰 소비가 늘어남
- 복잡한 수학, 논리, 코딩 문제에 유리

---

## 모델 관리 팁

1. **5-10개만 선택**: 너무 많으면 `/model` 전환이 불편
2. **에이전트용 + 대화용 분리**: tool calling 지원 여부에 따라 구분
3. **정기적으로 테스트**: NanoGPT에서 모델이 제거될 수 있음
4. **`:thinking` 모델은 별도 카테고리**: 같은 모델의 일반/추론 버전을 구분

---

**관련 문서**: [RECOMMENDED_MODELS.md](./RECOMMENDED_MODELS.md) | [SETUP_GUIDE.md](./SETUP_GUIDE.md)
