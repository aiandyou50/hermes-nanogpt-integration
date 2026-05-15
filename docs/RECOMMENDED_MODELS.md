# 추천 모델 목록 (2026년 5월 기준)

NanoGPT에서 Hermes AI와 함께 사용하기 위해 검증된 모델 목록입니다.

> 💡 모든 모델은 NanoGPT $12/월 멤버십으로 주 60,000,000 토큰 내에서 사용 가능합니다.

---

## 🏆 최우선 추천 모델

### DeepSeek V4 시리즈

| 모델 | 특징 | 추천 용도 |
|------|------|----------|
| `deepseek/deepseek-v4-flash` | 빠르고 저렴, tool calling 지원 | **일반 대화, 에이전트 작업** |
| `deepseek/deepseek-v4-pro` | 고품질, tool calling 지원 | 복잡한 추론, 코드 생성 |
| `deepseek/deepseek-v4-pro-cheaper` | Pro 대비 저렴 | Pro 품질 + 비용 절감 |
| `deepseek/deepseek-latest` | 항상 최신 버전 | 최신 기능 사용 시 |

> 💡 `:thinking` 접미사를 붙이면 reasoning 모드가 활성화됩니다. (예: `deepseek/deepseek-v4-flash:thinking`)
> 더 깊은 추론이 가능하지만 응답 시간이 길어지고 토큰 소비가 늘어납니다.

### Xiaomi MiMo

| 모델 | 특징 | 추천 용도 |
|------|------|----------|
| `xiaomi/mimo-v2.5-pro` | 균형 잡힌 성능 | **범용 메인 모델** |

### Moonshot Kimi

| 모델 | 특징 | 추천 용도 |
|------|------|----------|
| `moonshotai/kimi-k2.6` | 빠른 응답, 한국어 잘함 | 한국어 작업, 일반 대화 |
| `moonshotai/kimi-k2.6:thinking` | reasoning 모드 | 복잡한 분석, 추론 |

---

## 🎯 카테고리별 모델

### 🗣️ 일반 대화 및 한국어

| 모델 | Tool Calling | 비고 |
|------|:---:|------|
| `xiaomi/mimo-v2.5-pro` | ✅ | 균형 잡힌 범용 모델 |
| `moonshotai/kimi-k2.6` | ✅ | 한국어 강점 |
| `deepseek/deepseek-v4-flash` | ✅ | 빠르고 안정적 |

### 🧠 추론 및 코딩 (Reasoning)

| 모델 | Tool Calling | 비고 |
|------|:---:|------|
| `deepseek/deepseek-v4-pro:thinking` | ✅ | 최고 품질 추론 |
| `deepseek/deepseek-v4-flash:thinking` | ✅ | 저렴한 reasoning |
| `moonshotai/kimi-k2.6:thinking` | ✅ | 한국어 reasoning |
| `zai-org/glm-5.1:thinking` | ✅ | GLM reasoning |

### 💻 코딩 특화

| 모델 | Tool Calling | 비고 |
|------|:---:|------|
| `deepseek/deepseek-v4-pro` | ✅ | 코드 생성 최강 |
| `deepseek/deepseek-v4-pro-cheaper` | ✅ | 비용 효율적 코딩 |
| `minimax/minimax-m2.7` | ✅ | 대안 모델 |

### 📚 롤플레이 / 창작 (Derestricted)

> ⚠️ 이 모델들은 제한이 완화된 파인튜닝 버전입니다. 롤플레이, 창작 글쓰기에 적합합니다.
> Tool calling은 지원하지 않을 수 있으므로 에이전트 작업보다는 대화 용도로 사용하세요.

| 모델 | 비고 |
|------|------|
| `Gemma-4-31B-DarkIdol` | 인기 롤플레이 모델 |
| `Gemma-4-31B-Queen` | Gemma 기반 |
| `Gemma-4-31B-Cognitive-Unshackled` | 창의적 글쓰기 |
| `gemma-4-31B-MeroMero` | 일본 스타일 |
| `Qwen3.5-27B-Queen-Derestricted` | Qwen 기반 롤플레이 |
| `Qwen3.5-27B-RpRMax-v1` | 롤플레이 특화 |
| `Qwen3.5-27B-NaNovel-Derestricted` | 소설/이야기 |
| `Qwen3.5-27B-BlueStar-v3-Derestricted` | 다목적 |
| `Qwen3.5-27B-Infracelestial` | 판타지 |
| `Qwen3.5-27B-earica-Derestricted` | 대화 특화 |
| `Qwen3.5-27B-Marvin-DPO-V2-Derestricted` | DPO 최적화 |
| `Qwen3.5-27B-Omega-Evolution-v2.2-Derestricted` | 진화형 |

### 🔬 기타

| 모델 | Tool Calling | 비고 |
|------|:---:|------|
| `zai-org/glm-5.1` | ✅ | 중국어 강점 |
| `huihui-ai/DeepSeek-R1-Distill-Qwen-32B-abliterated` | ❌ | 탈감화 모델 |
| `nousresearch/hermes-3-llama-3.1-70b` | ❌ | Hermes 원본 모델 |

---

## 📊 용도별 추천 조합

### 🤖 에이전트 모드 (Tool Calling 필수)
```
메인: deepseek/deepseek-v4-flash
서브: xiaomi/mimo-v2.5-pro
추론: deepseek/deepseek-v4-pro:thinking
```

### 💬 한국어 대화
```
메인: moonshotai/kimi-k2.6
서브: xiaomi/mimo-v2.5-pro
```

### 📖 롤플레이 / 창작
```
메인: Gemma-4-31B-DarkIdol
서브: Qwen3.5-27B-Queen-Derestricted
대안: Qwen3.5-27B-RpRMax-v1
```

### 💰 비용 최적화
```
메인: deepseek/deepseek-v4-flash
서브: deepseek/deepseek-v4-pro-cheaper
```

---

## 🔄 모델 업데이트

- **마지막 업데이트**: 2026년 5월 16일
- 모델 가용성은 NanoGPT 사정에 따라 변경될 수 있습니다.
- 새 모델이 추가되면 `~/.hermes/config.yaml`의 `models:` 목록에 수동으로 추가해야 합니다.

---

**관련 문서**: [SETUP_GUIDE.md](./SETUP_GUIDE.md) | [MODELS_SELECTION.md](./MODELS_SELECTION.md)
