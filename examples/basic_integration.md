# 기본 통합 예시

## 📋 문서 설명

이 문서는 **NanoGPT를 Hermes AI에 기본적으로 통합하는 여러 프로그래밍 언어의 코드 예시**를 제공합니다.

---

## 🎯 작성 지침

다음 내용을 작성해주세요:

### 📌 포함되어야 할 섹션

#### 1. **Python 예시**
- 기본 설정 코드
- NanoGPT 클라이언트 초기화
- 간단한 텍스트 생성
- 이미지 생성
- 오류 처리

#### 2. **JavaScript/Node.js 예시**
- 패키지 설치
- 클라이언트 설정
- 기본 쿼리
- 비동기 처리

#### 3. **기타 언어 (선택)**
- Go
- Java
- Ruby

#### 4. **설정 파일 예시**
- 환경 변수 설정
- 설정 JSON/YAML
- 모델 목록 설정

#### 5. **완전한 예제**
- 전체 플로우
- 실제 사용 가능한 코드
- 주석 포함

#### 6. **실행 방법**
- 필수 패키지 설치
- 실행 명령어
- 예상 출력

---

## 📝 작성 형식

```markdown
# 기본 통합 예시

## 📋 문서 설명

## Python

### 1. 설치
\`\`\`bash
pip install hermes-agent nanogpt-client
\`\`\`

### 2. 기본 설정
\`\`\`python
from hermes import Agent
from nanogpt import NanoGPT

# API 키 설정
api_key = "your_nanogpt_api_key"

# NanoGPT 클라이언트 초기화
client = NanoGPT(api_key=api_key)

# Hermes 에이전트 초기화
agent = Agent()
agent.add_provider("nanogpt", client)
\`\`\`

### 3. 텍스트 생성
\`\`\`python
response = agent.generate(
    provider="nanogpt",
    model="model-name",
    prompt="당신의 프롬프트"
)

print(response)
\`\`\`

### 4. 이미지 생성
\`\`\`python
image = agent.generate_image(
    provider="nanogpt",
    model="image-model",
    prompt="이미지 설명"
)
\`\`\`

## JavaScript

### 1. 설치
\`\`\`bash
npm install hermes-agent nanogpt-client
\`\`\`

### 2. 기본 설정
\`\`\`javascript
const { Agent } = require('hermes-agent');
const { NanoGPT } = require('nanogpt-client');

const apiKey = 'your_nanogpt_api_key';
const client = new NanoGPT({ apiKey });
const agent = new Agent();

agent.addProvider('nanogpt', client);
\`\`\`

### 3. 텍스트 생성
\`\`\`javascript
const response = await agent.generate({
  provider: 'nanogpt',
  model: 'model-name',
  prompt: '당신의 프롬프트'
});

console.log(response);
\`\`\`

## 환경 변수 설정

### .env 파일
\`\`\`
NANOGPT_API_KEY=your_api_key_here
HERMES_PROVIDER=nanogpt
\`\`\`

## 완전한 예제

### Python 완전 예제
\`\`\`python
[전체 코드]
\`\`\`

### 실행 방법
\`\`\`bash
python example.py
\`\`\`
```

---

## 💡 작성 팁

✅ **복사-붙여넣기 가능**: 바로 실행 가능한 완전한 코드
✅ **상세한 주석**: 각 라인의 의미 설명
✅ **오류 처리**: try-except 또는 try-catch 포함
✅ **여러 언어**: Python, JavaScript 필수, Go/Java 추가
✅ **실행 결과**: 코드 실행 후 예상되는 출력 표시
✅ **환경 설정**: API 키, 환경 변수 설정 방법
✅ **의존성**: 필요한 패키지 모두 명시

---

## 🎯 작성 목표

이 문서를 본 개발자가 다음을 할 수 있어야 합니다:
- ✅ 개발 환경 설정
- ✅ 코드 복사 후 바로 실행
- ✅ NanoGPT를 통해 텍스트 생성
- ✅ 이미지 생성 기능 사용
- ✅ 오류 상황 대응

---

**관련 문서**: 
- [SETUP_GUIDE.md](../docs/SETUP_GUIDE.md)
- [custom_model_selection.md](./custom_model_selection.md)
