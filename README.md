# Hermes AI × NanoGPT 통합 가이드

Hermes AI 에이전트에서 NanoGPT를 추가 공급자로 등록하여 사용하는 방법을 안내하는 문서 모음입니다.

## 📖 프로젝트 개요

### 🎯 프로젝트 목표

이 레포지토리는 **Hermes AI 사용자**가 **NanoGPT 구독 서비스**를 Hermes AI 에이전트의 추가 공급자로 설정하고 효과적으로 활용하기 위한 완벽한 가이드를 제공합니다.

### 🌐 NanoGPT란?

**NanoGPT** (https://nano-gpt.com/)는 **600개 이상의 AI 모델**을 한 플랫폼에서 제공하는 종합 AI 서비스입니다.

**12달러 멤버십 혜택:**
- 📊 **주(Week) 60,000,000 토큰** 사용 가능 (일부 모델 무료)
- 🖼️ **매일 100개 이미지 생성** 가능
- 🤖 **600개 이상의 AI 모델** 중 일부 무료 접근 가능

> 💡 12달러 멤버십으로 가입하면 NanoGPT의 600개 이상 모델 중 일부 모델을 무료로 사용할 수 있으며, 주당 60,000,000 토큰의 할당량이 제공됩니다.

### 🔌 Hermes AI와의 통합

**Hermes AI** (https://github.com/NousResearch/hermes-agent)는 오픈소스 AI 에이전트 프레임워크로, 여러 공급자(Provider)를 지원하여 다양한 AI 모델을 통합 관리할 수 있습니다.

이 가이드는 **NanoGPT를 Hermes AI의 새로운 공급자로 추가**하여 `/model` 명령어로 NanoGPT의 모델을 사용할 수 있는 방법을 제시합니다.

**이를 통해 얻을 수 있는 이점:**
- 💰 저렴한 비용으로 대량의 토큰 사용
- 🔄 Hermes AI에서 직접 NanoGPT 모델 활용
- 🎨 이미지 생성 기능 통합
- 📈 600개 이상의 모델 중 필요한 모델만 선택

### ⚠️ 해결하는 문제

**문제점:**
- Hermes AI에서 NanoGPT의 600개 이상 모델을 모두 확인하는 것이 매우 불편함
- 사용자가 원하는 모델만 추가하여 사용할 수 없음

**이 가이드의 해결책:**
- ✅ NanoGPT 공급자 추가 방법 단계별 안내
- ✅ 자신이 원하는 모델만 선택하여 추가하는 방법
- ✅ 커뮤니티 추천 모델 목록
- ✅ AI 에이전트가 바로 사용 가능한 프롬프트

## 📁 파일 구조

```
hermes-nanogpt-integration/
├── README.md                          # 프로젝트 소개 및 가이드
├── LICENSE                            # MIT 라이선스
│
├── docs/                              # 핵심 문서 (작성 지침)
│   ├── SETUP_GUIDE.md                # NanoGPT 공급자 추가 방법
│   ├── MODELS_SELECTION.md           # 커스텀 모델 선택 방법
│   ├── RECOMMENDED_MODELS.md         # 추천 모델 목록
│   └── QUICK_START.md                # AI 에이전트용 프롬프트
│
└── examples/                          # 실제 구현 예시 (작성 지침)
    ├── basic_integration.md           # 기본 통합 코드 예시
    ├── custom_model_selection.md      # 커스텀 모델 선택 코드 예시
    └── agent_prompt.md               # AI 에이전트 프롬프트 템플릿
```

## 📚 구성 문서

### **docs/ - 핵심 가이드 문서**

| 문서 | 설명 |
|------|------|
| **SETUP_GUIDE.md** | NanoGPT API 키 획득부터 Hermes AI 공급자 추가까지의 단계별 설정 방법 및 코드 예시 |
| **MODELS_SELECTION.md** | 600개 이상의 모델에서 원하는 모델만 선택하여 추가하는 방법과 실제 적용 방법 |
| **RECOMMENDED_MODELS.md** | 커뮤니티 추천 모델 목록 (텍스트, 이미지, 성능 기반, 특화 모델 등) |
| **QUICK_START.md** | AI 에이전트에 바로 전달 가능한 시스템 프롬프트, 템플릿, 중요 정보 정리 |

### **examples/ - 실제 구현 예시**

| 문서 | 설명 |
|------|------|
| **basic_integration.md** | NanoGPT 통합의 기본 코드 예시 (여러 프로그래밍 언어) |
| **custom_model_selection.md** | 실제 상황별 모델 선택 시나리오 및 구현 코드 |
| **agent_prompt.md** | AI 에이전트에 복사-붙여넣기로 사용 가능한 프롬프트 모음 |

## 🚀 빠른 시작

### 1️⃣ 설정하기
[`docs/SETUP_GUIDE.md`](./docs/SETUP_GUIDE.md)를 따라 NanoGPT를 Hermes AI 공급자로 추가하세요.

### 2️⃣ 모델 선택하기
[`docs/MODELS_SELECTION.md`](./docs/MODELS_SELECTION.md)에서 600개 이상의 모델 중 필요한 모델만 선택하는 방법을 배우세요.

### 3️⃣ 추천 모델 확인
[`docs/RECOMMENDED_MODELS.md`](./docs/RECOMMENDED_MODELS.md)에서 검증된 추천 모델 목록을 확인하세요.

### 4️⃣ AI 에이전트 활용
[`docs/QUICK_START.md`](./docs/QUICK_START.md)의 프롬프트를 AI 에이전트에 전달하세요.

### 5️⃣ 코드 예시 참고
[`examples/`](./examples/) 폴더의 실제 구현 예시를 참고하세요.

## 📋 사용 방법

### 👤 일반 사용자
1. `docs/` 폴더의 문서들을 순서대로 읽기
2. 필요한 모델 선택 후 설정
3. `examples/`의 코드 참고하여 구현

### 🤖 AI 에이전트 활용
1. [`docs/QUICK_START.md`](./docs/QUICK_START.md)의 프롬프트 복사
2. AI 에이전트(Claude, GPT-4, Hermes 등)에 전달
3. 에이전트가 자동으로 설정 및 사용 지원

## 📝 각 문서의 작성 형식

모든 문서는 **AI 에이전트가 작성하기 쉽도록** 구조화되어 있으며, 각 문서 내에 다음이 포함됩니다:

- **문서 설명**: 해당 문서의 목적
- **작성 지침**: AI가 따라야 할 구조와 형식
- **섹션 안내**: 각 섹션에 포함되어야 할 내용
- **형식 예시**: 마크다운 템플릿 및 표 양식
- **작성 팁**: 더 나은 문서를 위한 조언

## 📌 주요 특징

✅ **단계별 가이드**: 초보자도 쉽게 따라할 수 있는 설정 방법  
✅ **맞춤형 모델 선택**: 600개 이상의 모델 중 필요한 모델만 추가  
✅ **AI 에이전트 최적화**: 프롬프트 복사 후 바로 사용 가능  
✅ **실제 코드 예시**: 다양한 상황의 구현 예시 포함  
✅ **커뮤니티 추천**: 검증된 모델 목록 제공  
✅ **NanoGPT 통합**: Hermes AI에서 직접 NanoGPT 모델 활용  

## 💡 NanoGPT 12달러 멤버십 활용 팁

- **주당 60,000,000 토큰**: 대규모 프로젝트에 충분한 리소스
- **일일 100개 이미지**: 이미지 생성 기능 활발하게 활용
- **일부 모델 무료**: 12달러 멤버십으로 600개 이상 모델 중 일부 무료 사용
- **비용 효율**: Hermes AI와 함께 사용하면 매우 경제적

## 📄 라이선스

MIT License - 자유롭게 사용, 수정, 배포 가능합니다.

자세한 내용은 [`LICENSE`](./LICENSE) 파일을 참고하세요.

## 🔗 참고 링크

- **NanoGPT**: https://nano-gpt.com/
- **Hermes AI**: https://github.com/NousResearch/hermes-agent

## 🤝 기여

이 프로젝트의 개선을 위한 이슈 등록 및 풀 리퀘스트를 환영합니다.

---

**지금 시작하기**: [`docs/SETUP_GUIDE.md`](./docs/SETUP_GUIDE.md)에서 NanoGPT 설정을 시작하세요! 🚀
