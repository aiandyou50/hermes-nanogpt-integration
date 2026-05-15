# AI 에이전트 프롬프트 템플릿

Hermes AI 또는 다른 AI 에이전트에 복사-붙여넣기로 전달 가능한 프롬프트 모음입니다.

---

## 1. 초기 설정 프롬프트

AI 에이전트에게 NanoGPT 설정을 요청할 때:

```
Hermes AI에 NanoGPT를 공급자로 추가해줘.

요구사항:
1. ~/.hermes/.env에 NANOGPT_API_KEY=sk-nano-실제키 추가
2. ~/.hermes/config.yaml의 providers 섹션에 nanogpt 공급자 등록
3. base_url: https://nano-gpt.com/api/v1
4. key_env: NANOGPT_API_KEY (api_key_env 아님!)
5. discover_models: false 설정
6. 원하는 모델만 models 목록에 추가
7. 게이트웨이 재시작

주의사항:
- key_env 필드명을 api_key_env로 쓰면 401 오류 발생
- discover_models를 설정하지 않으면 600+개 모델이 모두 로드됨
- 모델 전환은 /model nanogpt:모델명 형식 (콜론 구분자)
```

---

## 2. 모델 추가 프롬프트

새 모델을 추가할 때:

```
config.yaml의 nanogpt 모델 목록에 다음 모델을 추가해줘:
- 모델명1
- 모델명2

추가 후 게이트웨이도 재시작해줘.
```

---

## 3. 연결 확인 프롬프트

```
NanoGPT 연결 상태를 확인해줘:
1. .env에 NANOGPT_API_KEY가 있는지
2. config.yaml에 nanogpt 공급자가 올바르게 설정되어 있는지
3. curl로 API 테스트해서 응답이 오는지
4. 문제가 있으면 해결해줘
```

---

## 4. 모델 전환 프롬프트

```
현재 모델을 nanogpt의 deepseek/deepseek-v4-flash로 전환해줘.
/model 명령어를 사용해서.
```

---

## 5. 트러블슈팅 프롬프트

```
NanoGPT 연결에 문제가 있어. 다음을 확인해줘:
1. 401 오류 → key_env 필드명이 api_key_env로 잘못되어 있는지
2. Model not found → discover_models가 false로 설정되어 있는지
3. Unknown provider → 모델명 구분자가 콜론(:)인지
각 항목을 확인하고 문제가 있으면 수정해줘.
```

---

## 6. 롤플레이 분리 프롬프트

```
메인 모드와 롤플레이 모드를 분리하고 싶어.
메인은 xiaomi/mimo-v2.5-pro를 사용하고,
롤플레이는 Gemma-4-31B-DarkIdol을 사용할 거야.
새 프로필을 만들어서 설정해줘.
```

---

## 사용 팁

- 프롬프트의 `모델명` 부분을 실제 모델명으로 교체하세요
- `sk-nano-실제키` 부분을 실제 API 키로 교체하세요
- AI 에이전트가 모르는 내용이 있으면 [TROUBLESHOOTING.md](../docs/TROUBLESHOOTING.md)를 참조하세요

---

**관련 문서**: [QUICK_START.md](../docs/QUICK_START.md) | [SETUP_GUIDE.md](../docs/SETUP_GUIDE.md)
