# 트러블슈팅 — 실전에서 발견한 오류와 해결법

Hermes AI + NanoGPT 통합 과정에서 실제로 발생한 문제들과 해결 방법입니다.

---

## ❌ 401 Unauthorized

### 증상
```
Error: 401 Unauthorized
```

### 원인
`config.yaml`에서 API 키 환경 변수 필드명을 잘못 지정한 경우.

### 해결
`api_key_env`가 아닌 **`key_env`**를 사용해야 합니다:

```yaml
# ❌ 잘못된 설정
providers:
  nanogpt:
    api_key_env: "NANOGPT_API_KEY"  # 이 필드명은 인식 안 됨

# ✅ 올바른 설정
providers:
  nanogpt:
    key_env: "NANOGPT_API_KEY"  # 반드시 key_env 사용
```

### 확인 방법
```bash
# .env 파일에 키가 있는지 확인
grep NANOGPT_API_KEY ~/.hermes/.env

# 직접 API 테스트
curl -s https://nano-gpt.com/api/v1/models \
  -H "Authorization: Bearer $NANOGPT_API_KEY" | head -c 200
```

---

## ❌ Model not found in provider's model listing

### 증상
```
Error: Model nousresearch/hermes-3-llama-3.1-70b was not found in this provider's model listing.
```

### 원인
`discover_models`가 `true`(기본값)이면, Hermes가 NanoGPT API에서 **전체 모델 목록을 가져와서** config에 등록한 모델을 덮어씁니다. API에서 해당 모델을 찾을 수 없으면 오류가 발생합니다.

### 해결
`discover_models: false`를 추가합니다:

```yaml
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false   # ← 이 줄 추가
    models:
      - deepseek/deepseek-v4-flash
      # ... 원하는 모델만 나열
```

### 왜 이런 일이 발생하나?
Hermes의 모델 로딩 로직:
1. 먼저 config의 `models:` 필드에서 모델 목록을 읽음
2. `discover_models`가 true이면 API의 `/v1/models` 엔드포인트에서 전체 목록을 가져옴
3. API 목록으로 **덮어씀** → config에 없던 600+개 모델이 모두 로드됨
4. 일부 모델이 API 목록과 config 이름이 다르면 "not found" 오류 발생

---

## ❌ Unknown provider: nanogpt

### 증상
```
/model nanogpt/deepseek-v4-flash
→ Unknown provider: nanogpt
```

### 원인
모델명 구분자를 슬래시(`/`)로 사용한 경우.

### 해결
**콜론(`:`)**을 사용합니다:

```bash
# ❌ 잘못된 형식
/model nanogpt/deepseek-v4-flash

# ✅ 올바른 형식
/model nanogpt:deepseek/deepseek-v4-flash
```

---

## ❌ 모델 목록이 600개 이상으로 표시됨

### 증상
`/model` 명령어나 텔레그램 피커에서 수백 개의 모델이 나타남.

### 원인
`discover_models: false`를 설정하지 않은 경우.

### 해결
위의 "Model not found" 해결법과 동일 — `discover_models: false` 추가.

---

## ❌ 게이트웨이 재시작 후 변경사항 미반영

### 증상
config.yaml을 수정했지만 `/model` 목록에 변경이 없음.

### 해결
게이트웨이를 재시작합니다:

```bash
hermes gateway restart
```

또는 텔레그램에서:
```
/restart
```

---

## ❌ 텔레그램 피커에서 모델이 안 보임

### 증상
텔레그램 `/model` 버튼 목록에 NanoGPT 모델이 없음.

### 원인
`providers.nanogpt` 설정이 올바르지 않거나, 게이트웨이가 재시작되지 않은 경우.

### 확인 순서
1. `config.yaml`의 `providers.nanogpt` 섹션 확인
2. `key_env` 필드명 확인 (`api_key_env` ❌)
3. `.env`에 `NANOGPT_API_KEY` 존재 확인
4. 게이트웨이 재시작 확인

---

## 빠른 진단 체크리스트

```bash
# 1. .env 파일 확인
cat ~/.hermes/.env | grep NANOGPT

# 2. config.yaml 확인
cat ~/.hermes/config.yaml | grep -A 5 nanogpt

# 3. API 직접 테스트
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer $NANOGPT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"deepseek/deepseek-v4-flash","messages":[{"role":"user","content":"hi"}],"max_tokens":5}'

# 4. 게이트웨이 상태 확인
hermes gateway status
```

---

**관련 문서**: [SETUP_GUIDE.md](./SETUP_GUIDE.md) | [README.md](../README.md)
