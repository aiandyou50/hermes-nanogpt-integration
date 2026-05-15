# 다중 프로필 가이드 — 모드별 분리 운영

메인 모드와 롤플레이 모드를 완전히 분리하여 운영하는 방법을 설명합니다.

---

##为什么要 분리하나?

같은 Hermes 인스턴스에서 에이전트 모델과 롤플레이 모델을 섞어 쓰면:
- **대화 기록이 섞임** — 에이전트 작업 내역과 롤플레이 대화가 한 세션에混在
- **시스템 프롬프트 충돌** — 에이전트용 SOUL.md와 롤플레이용 SOUL.md가 다름
- **모델 전환 번거로움** —每次 `/model`을手动切换

**프로필을 분리하면 각각 독립적인 config, 메모리, 세션, SOUL.md를 가집니다.**

---

## 프로필 생성 방법

### 1단계: 롤플레이 프로필 생성

```bash
# 기본 프로필(config, .env)을 복사하면서 새 프로필 생성
hermes profile create roleplay --clone
```

`--clone` 옵션: config.yaml, .env, SOUL.md를 복사합니다.

### 2단계: 롤플레이 프로필 설정 수정

```bash
# 롤플레이 프로필의 config.yaml 수정
nano ~/.hermes/profiles/roleplay/config.yaml
```

```yaml
# 롤플레이 전용 설정
model:
  default: "nanogpt:Gemma-4-31B-DarkIdol"

providers:
  nanogpt:
    base_url: "https://nano-gpt.com/api/v1"
    key_env: "NANOGPT_API_KEY"
    discover_models: false
    models:
      # 롤플레이 전용 모델만
      - Gemma-4-31B-DarkIdol
      - Gemma-4-31B-Queen
      - Gemma-4-31B-Cognitive-Unshackled
      - Qwen3.5-27B-Queen-Derestricted
      - Qwen3.5-27B-RpRMax-v1
      - Qwen3.5-27B-NaNovel-Derestricted
```

### 3단계: SOUL.md 커스터마이즈 (선택)

```bash
# 롤플레이 전용 SOUL.md 작성
nano ~/.hermes/profiles/roleplay/SOUL.md
```

롤플레이 캐릭터의 성격, 말투, 배경 등을 설정합니다.

### 4단계: 텔레그램 봇 연결

> ⚠️ **중요**: 각 프로필은 **별도의 텔레그램 봇 토큰**이 필요합니다.
> 같은 봇 토큰을 두 프로필이共享하면 충돌이 발생합니다.

#### 새 봇 생성
1. Telegram에서 [@BotFather](https://t.me/BotFather)에게 `/newbot` 전송
2. 봇 이름과 사용자명 설정
3. 발급된 토큰 복사

#### 롤플레이 프로필에 봇 토큰 설정
```bash
# 롤플레이 프로필의 .env에 새 봇 토큰 추가
echo 'TELEGRAM_BOT_TOKEN=새-봇-토큰-여기에' >> ~/.hermes/profiles/roleplay/.env
```

### 5단계: 게이트웨이 시작

```bash
# 롤플레이 프로필의 게이트웨이 시작
hermes -p roleplay gateway start
```

---

## 운영 방법

### 두 프로필 동시 실행

```bash
# 기본 프로필 (메인)
hermes gateway start

# 롤플레이 프로필
hermes -p roleplay gateway start
```

### 프로필 전환 (CLI 모드)

```bash
# 기본 프로필 사용
hermes chat

# 롤플레이 프로필 사용
hermes -p roleplay chat
```

### 프로필 확인

```bash
# 현재 프로필 목록
hermes profile list

# 특정 프로필 정보
hermes profile info roleplay
```

---

## 프로필 삭제

```bash
hermes profile delete roleplay
```

---

## 프로필 구조

```
~/.hermes/
├── config.yaml              # 기본 프로필 설정
├── .env                     # 기본 프로필 환경 변수
├── SOUL.md                  # 기본 프로필 성격
├── memories/                # 기본 프로필 메모리
├── sessions/                # 기본 프로필 세션
│
└── profiles/
    └── roleplay/
        ├── config.yaml      # 롤플레이 설정
        ├── .env             # 롤플레이 환경 변수 (다른 봇 토큰)
        ├── SOUL.md          # 롤플레이 캐릭터
        ├── memories/        # 롤플레이 메모리
        └── sessions/        # 롤플레이 세션
```

---

## 주의사항

1. **봇 토큰 충돌**: 같은 텔레그램 봇 토큰을 두 프로필이 사용하면 안 됩니다
2. **게이트웨이 포트**: 여러 프로필을 같은 서버에서运行할 때 포트 충돌에 주의
3. **API 키共享**: `.env`의 `NANOGPT_API_KEY`는 같은 키를 사용해도 됩니다 (NanoGPT 계정共享)
4. **메모리 분리**: 각 프로필의 대화 기록과 메모리는完全独立입니다

---

**관련 문서**: [SETUP_GUIDE.md](./SETUP_GUIDE.md) | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
