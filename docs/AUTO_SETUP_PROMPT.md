# NanoGPT 자동 설정 프롬프트

> **사용법**: 이 파일의 내용을 복사하여 AI 에이전트(Hermes, Claude, GPT 등)에게 전달하세요.
> 에이전트가 대화하면서 자동으로 NanoGPT를 설정해줍니다.

---

```markdown
# NanoGPT × Hermes AI 자동 설정

## 너의 임무

Hermes AI 사용자의 시스템에 NanoGPT를 공급자로 자동 설정해줘.
사용자가 복잡한 수작업을 하지 않도록, 너가 직접 파일을 수정하고 검증까지 해야 해.

## 1단계: 가이드 레포지토리 분석

먼저 hermes-nanogpt-integration 레포지토리를 pull하고 분석해줘.

```bash
# 레포지토리 클론 (이미 있으면 pull)
REPO_DIR="$HOME/.hermes/hermes-nanogpt-integration"
if [ -d "$REPO_DIR" ]; then
  cd "$REPO_DIR" && git pull
else
  git clone https://github.com/aiandyou50/hermes-nanogpt-integration.git "$REPO_DIR"
fi
```

클론 후 아래 파일들을 모두 읽고 분석해:
- `README.md` — 프로젝트 전체 구조
- `docs/SETUP_GUIDE.md` — 설정 방법
- `docs/RECOMMENDED_MODELS.md` — 추천 모델 목록
- `docs/TROUBLESHOOTING.md` — 실전 오류 해결법

## 2단계: 사용자에게 모델 선택 받기

**⚠️ 중요: 모델 목록은 하드코딩하지 마!**

1단계에서 clone한 레포의 `docs/RECOMMENDED_MODELS.md` 파일을 반드시 읽어.
이 파일에는 레포 관리자가 최신으로 유지하는 추천 모델 목록이 들어있어.
아래는 **예시일 뿐**이니, 실제 파일에서 카테고리와 모델명을 읽어서 사용자에게 보여줘.

```
읽어야 할 파일: $HOME/.hermes/hermes-nanogpt-integration/docs/RECOMMENDED_MODELS.md
```

파일을 읽은 후:
1. 각 카테고리(에이전트 모드, 롤플레이/창작 등)의 모델을 사용자에게 표로 보여줘
2. 사용자에게 물어봐:
   - "어떤 용도로 사용하실 건가요? (에이전트/롤플레이/Both)"
   - "위 목록에서 사용할 모델을 선택해주세요. 여러 개 선택 가능합니다."
   - "기본 모델로 사용할 모델을 하나 선택해주세요."


## 3단계: NanoGPT API 키 확인

사용자에게 NanoGPT API 키가 있는지 물어봐.

- **없으면**: https://nano-gpt.com/ 에서 가입하고 API Keys 메뉴에서 생성하도록 안내
- **있으면**: 키를 입력받아서 `.env`에 저장

```bash
# .env 파일에 API 키 추가 (기존 키가 있으면 덮어쓰지 않도록 확인)
ENV_FILE="$HOME/.hermes/.env"
KEY_VAR="NANOGPT_API_KEY"

if grep -q "^${KEY_VAR}=" "$ENV_FILE" 2>/dev/null; then
  echo "이미 NANOGPT_API_KEY가 설정되어 있습니다."
else
  echo "${KEY_VAR}=사용자가-입력한-키" >> "$ENV_FILE"
  echo "API 키가 .env에 추가되었습니다."
fi
```

## 4단계: config.yaml 설정

분석한 가이드를 바탕으로 `~/.hermes/config.yaml`을 수정해줘.

**반드시 지켜야 할 규칙:**

1. **`key_env` 사용** — `api_key_env`가 아님! 틀리면 401 오류 발생
2. **`discover_models: false` 설정** — 안 하면 600+개 모델이 모두 로드됨
3. **`base_url`에 `/v1` 포함** — `https://nano-gpt.com/api/v1`
4. **모델명 정확히 복사** — 대소문자 구분

```yaml
# config.yaml에 추가할 내용 (예시)
providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      # 사용자가 선택한 모델 여기에 추가
      - deepseek/deepseek-v4-flash
      - xiaomi/mimo-v2.5-pro
      # ...
```

**중요**: 기존 `providers:` 섹션에 다른 공급자가 이미 있으면, nanogpt만 추가해야 해. 기존 설정을 덮어쓰면 안 돼!

## 5단계: API 연결 검증

설정 후 반드시 검증해줘:

```bash
# 1. API 키 동작 확인
curl -s https://nano-gpt.com/api/v1/chat/completions \
  -H "Authorization: Bearer $NANOGPT_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4-flash",
    "messages": [{"role": "user", "content": "Say OK"}],
    "max_tokens": 5
  }' | python3 -c "
import sys, json
data = json.load(sys.stdin)
if 'choices' in data:
    print('✅ API 연결 성공')
else:
    print('❌ API 연결 실패:', data.get('error', {}).get('message', 'Unknown'))
"

# 2. config.yaml에서 nanogpt 설정 확인
python3 -c "
import yaml
with open('$HOME/.hermes/config.yaml') as f:
    config = yaml.safe_load(f)
ng = config.get('providers', {}).get('nanogpt', {})
print('base_url:', ng.get('base_url', '❌ 없음'))
print('key_env:', ng.get('key_env', '❌ 없음'))
print('discover_models:', ng.get('discover_models', '⚠️ 설정 안됨 (기본값 true)'))
print('models:', len(ng.get('models', [])), '개')
"
```

## 6단계: 게이트웨이 재시작

```bash
hermes gateway restart
```

또는 사용자에게 `/restart` 명령어를 안내.

## 7단계: 최종 확인

사용자에게 다음과 같이 안내:

```
✅ NanoGPT 설정이 완료되었습니다!

사용 방법:
  /model nanogpt:모델명

예시:
  /model nanogpt:deepseek/deepseek-v4-flash

기본 모델이 설정되어 있으므로, 별도 전환 없이 바로 사용 가능합니다.
```

## 에러 발생 시

아래 파일을 참조하여 해결해줘:
- `$HOME/.hermes/hermes-nanogpt-integration/docs/TROUBLESHOOTING.md`

주요 오류:
- **401 Unauthorized** → `key_env` 필드명 확인 (`api_key_env` ❌)
- **Model not found** → `discover_models: false` 설정 확인
- **Unknown provider** → 모델명 구분자가 `:`인지 확인 (`/` ❌)

---

## 관련 문서

- `docs/RECOMMENDED_MODELS.md` — 레포 관리자가 관리하는 최신 추천 모델 목록 (2단계에서 반드시 참조)
- `docs/SETUP_GUIDE.md` — 수동 설정 가이드
- `docs/TROUBLESHOOTING.md` — 실전 오류 해결법
- `docs/MULTI_PROFILE.md` — 다중 프로필 분리 운영

---

위 단계를 순서대로 실행해줘. 각 단계에서 문제가 생기면 사용자에게 알려주고 해결해.
```
