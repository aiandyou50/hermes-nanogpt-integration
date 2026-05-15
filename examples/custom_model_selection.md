# 커스텀 모델 선택 코드 예시

## 📋 문서 설명

이 문서는 **NanoGPT의 600개 이상 모델 중에서 자신의 필요에 맞는 모델을 선택하고 설정하는 실제 코드 예시**를 제공합니다.

---

## 🎯 작성 지침

다음 내용을 작성해주세요:

### 📌 포함되어야 할 섹션

#### 1. **시나리오 기반 예시**

각 시나리오마다:
- 상황 설명
- 필요한 모델
- 설정 코드
- 사용 코드
- 토큰 소비 예상

**포함할 시나리오:**
1. **텍스트 중심 작업**: 블로그, 문서 작성
2. **이미지 생성**: 아트, 일러스트
3. **빠른 응답**: 실시간 채팅
4. **혼합 작업**: 텍스트 + 이미지
5. **비용 최적화**: 저비용 모델 조합

#### 2. **모델 필터링 코드**
- 모델 목록 조회
- 특정 조건으로 필터링
- 모델 메타데이터 확인

#### 3. **설정 파일 수정 예시**
- JSON 형식
- YAML 형식
- Python 딕셔너리

#### 4. **모델 검증 코드**
- 선택한 모델이 존재하는지 확인
- 모델 정보 출력
- 토큰 한도 확인

#### 5. **성능 비교 코드**
- 같은 입력으로 여러 모델 실행
- 응답 시간 측정
- 결과 비교

#### 6. **토큰 계산 코드**
- 예상 토큰 사용량 계산
- 월간 비용 예측

---

## 📝 작성 형식

```markdown
# 커스텀 모델 선택 코드 예시

## 📋 문서 설명

## 시나리오 1: 텍스트 중심 작업

### 상황
블로그 글, 뉴스레터 등 장형 텍스트를 생성해야 합니다.

### 권장 모델
- Text Generation: Model-A
- Editing: Model-B

### 설정 코드
\`\`\`python
models_config = {
    "providers": [
        {
            "name": "nanogpt",
            "models": [
                "text-gen-large",
                "text-edit-pro"
            ]
        }
    ]
}

# 저장
import json
with open('models.json', 'w') as f:
    json.dump(models_config, f)
\`\`\`

### 사용 코드
\`\`\`python
agent.generate(
    model="text-gen-large",
    prompt="블로그 글 작성..."
)
\`\`\`

### 예상 토큰 소비
- 글 하나당: ~2,000 토큰
- 월간 예상: ~60,000 토큰

## 시나리오 2: 이미지 생성

### 상황
마케팅 자료, SNS 콘텐츠용 이미지를 생성합니다.

### 권장 모델
- Image Generation: Image-Model-A
- Image Editing: Image-Model-B

### 설정 코드
\`\`\`python
[코드]
\`\`\`

### 일일 이미지 생성 한도
- 12달러 멤버십: 100개/일

## 모델 필터링 코드

### 모델 목록 조회
\`\`\`python
models = agent.list_models(provider="nanogpt")
for model in models:
    print(f"{model['name']}: {model['description']}")
\`\`\`

### 조건으로 필터링
\`\`\`python
# 빠른 모델만
fast_models = [m for m in models if m['latency'] < 100]

# 무료 모델만
free_models = [m for m in models if m['cost'] == 'free']
\`\`\`

## 설정 파일 수정

### JSON 형식
\`\`\`json
{
  "providers": [
    {
      "name": "nanogpt",
      "models": [
        "model-1",
        "model-2"
      ]
    }
  ]
}
\`\`\`

### Python 딕셔너리
\`\`\`python
config = {
    'providers': [
        {
            'name': 'nanogpt',
            'models': ['model-1', 'model-2']
        }
    ]
}
\`\`\`

## 모델 검증 코드

\`\`\`python
# 모델 존재 확인
selected_models = ['model-1', 'model-2']
available_models = [m['name'] for m in agent.list_models()]

for model in selected_models:
    if model not in available_models:
        print(f"경고: {model}을(를) 찾을 수 없습니다.")
    else:
        print(f"✓ {model} 확인됨")
\`\`\`

## 성능 비교

\`\`\`python
import time

test_prompt = "테스트 프롬프트"
models = ['model-1', 'model-2', 'model-3']

for model in models:
    start = time.time()
    response = agent.generate(model=model, prompt=test_prompt)
    elapsed = time.time() - start
    
    print(f"{model}: {elapsed:.2f}초")
\`\`\`

## 토큰 계산

\`\`\`python
# 예상 토큰 계산
words = 1000  # 1000단어
token_per_word = 1.3

expected_tokens = int(words * token_per_word)
weekly_tokens = 60_000_000
weekly_usage = expected_tokens * 7

print(f"주간 토큰 사용: {weekly_usage:,}")
print(f"여유: {weekly_tokens - weekly_usage:,}")
\`\`\`
```

---

## 💡 작성 팁

✅ **5개 시나리오 모두**: 각각 완전히 다른 상황
✅ **완전한 코드**: 복사해서 바로 실행 가능
✅ **실제 모델명**: NanoGPT에 실제로 있는 모델
✅ **토큰 계산 포함**: 비용 예측 가능하게
✅ **비교 분석**: 각 모델의 장단점 명시
✅ **오류 처리**: 모델을 찾을 수 없을 때 처리
✅ **실제 결과**: 코드 실행 시 예상 결과 포함

---

## 🎯 작성 목표

이 문서를 본 사용자가 다음을 할 수 있어야 합니다:
- ✅ 자신의 상황에 맞는 시나리오 선택
- ✅ 권장 모델 조합 이해
- ✅ 코드 복사 후 설정 파일 수정
- ✅ 모델 검증 실행
- ✅ 토큰 사용량 예측
- ✅ 성능 비교로 최적 모델 선택

---

**관련 문서**: 
- [MODELS_SELECTION.md](../docs/MODELS_SELECTION.md)
- [basic_integration.md](./basic_integration.md)
