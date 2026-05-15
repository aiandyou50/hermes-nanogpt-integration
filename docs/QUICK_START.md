# 빠른 시작 — Hermes AI에서 NanoGPT 사용하기

이미 설정을 완료했다면, 여기서 바로 사용법을 익히세요.

---

## 모델 전환 명령어

### 기본 형식
```
/model 공급자:모델명
```

> ⚠️ 구분자는 **콜론(`:`)**입니다. 슬래시(`/`)가 아닙니다!

### NanoGPT 모델 전환 예시

```
/model nanogpt:deepseek/deepseek-v4-flash
/model nanogpt:xiaomi/mimo-v2.5-pro
/model nanogpt:moonshotai/kimi-k2.6
/model nanogpt:Gemma-4-31B-DarkIdol
```

### 현재 모델 확인
```
/model
```

---

## 텔레그램에서 모델 전환

텔레그램 봇과 대화 중에도 `/model` 명령어로 전환할 수 있습니다:

1. `/model` 입력 → 모델 선택 피커 표시
2. 원하는 모델 탭 → 즉시 전환
3. 이어서 대화 계속

---

## 빠른 시나리오별 설정

### 시나리오 1: 일반 대화
```
/model nanogpt:xiaomi/mimo-v2.5-pro
```

### 시나리오 2: 코딩 작업
```
/model nanogpt:deepseek/deepseek-v4-pro
```

### 시나리오 3: 깊은 추론이 필요한 작업
```
/model nanogpt:deepseek/deepseek-v4-pro:thinking
```

### 시나리오 4: 롤플레이 / 창작
```
/model nanogpt:Gemma-4-31B-DarkIdol
```

### 시나리오 5: 한국어 대화
```
/model nanogpt:moonshotai/kimi-k2.6
```

---

## 기본 모델 설정

매번 전환하기 번거롭다면 기본 모델을 설정합니다:

```yaml
# ~/.hermes/config.yaml
model:
  default: "nanogpt:deepseek/deepseek-v4-flash"
```

게이트웨이 재시작 후 적용됩니다.

---

## AI 에이전트 프롬프트 템플릿

### NanoGPT 설정 요청 프롬프트
AI 에이전트에게 다음과 같이 요청할 수 있습니다:

```
Hermes AI에 NanoGPT를 공급자로 추가해줘.
API 키는 .env의 NANOGPT_API_KEY를 사용하고,
config.yaml의 providers 섹션에 등록해줘.
discover_models는 false로 설정하고,
다음 모델들을 추가해줘:
- deepseek/deepseek-v4-flash
- xiaomi/mimo-v2.5-pro
- moonshotai/kimi-k2.6
```

### 모델 테스트 요청 프롬프트
```
NanoGPT 연결이 잘 되는지 확인해줘.
curl로 deepseek/deepseek-v4-flash 모델에 "Hello"를 보내고
응답이 정상인지 확인해줘.
```

### 모델 추가 요청 프롬프트
```
config.yaml의 nanogpt 모델 목록에 다음 모델을 추가해줘:
- 새-모델-이름
추가 후 게이트웨이 재시작도 해줘.
```

---

## 주요 제약사항

| 항목 | 제한 |
|------|------|
| 주간 토큰 | 60,000,000 (멤버십 기준) |
| 일일 이미지 | 100개 |
| 동시 요청 | NanoGPT 정책에 따름 |
| Tool calling | 모델별 상이 (지원 모델 사용 권장) |

---

**관련 문서**: [SETUP_GUIDE.md](./SETUP_GUIDE.md) | [RECOMMENDED_MODELS.md](./RECOMMENDED_MODELS.md)
