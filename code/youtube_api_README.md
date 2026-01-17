# 🎬 유튜브 댓글 분석: YouTube API + KoBERT 감성분석 + 혐오표현 탐지

YouTube Data API v3를 활용하여 공식적으로 댓글을 수집하고, KoBERT 기반 딥러닝 감성분석과 혐오표현 탐지를 수행하는 분석 도구입니다.

## ✨ 주요 기능

- **YouTube API 연동**: 공식 API를 통한 안정적인 데이터 수집
- **동영상 검색**: 키워드 기반 동영상 검색
- **댓글 수집**: 동영상별 댓글 및 메타데이터 수집
- **KoBERT 감성분석**: 딥러닝 기반 긍정/중립/부정 분류
- **혐오표현 탐지**: 7가지 유형의 혐오표현 자동 감지
- **종합 시각화**: 대시보드 및 다양한 차트 생성

## 📚 학습 목표

1. YouTube Data API를 활용하여 공식적으로 댓글을 수집한다
2. KoBERT 기반 딥러닝 감성분석을 수행한다
3. 혐오표현을 탐지하고 분류한다
4. 분석 결과를 시각화한다

## 🔑 YouTube Data API란?

- Google에서 제공하는 공식 YouTube API
- 동영상 검색, 채널 정보, 댓글 수집 등 가능
- **일일 할당량**: 10,000 units (댓글 1회 요청 ≈ 1 unit)
- 무료로 사용 가능 (Google Cloud Console에서 API 키 발급)

## 📋 목차

| Part | 내용 |
|------|------|
| Part 1 | 환경 설정 |
| Part 2 | YouTube API 설정 |
| Part 3 | 동영상 검색 및 댓글 수집 |
| Part 4 | 텍스트 전처리 |
| Part 5 | KoBERT 감성분석 |
| Part 6 | 혐오표현 탐지 |
| Part 7 | 종합 분석 및 시각화 |

## 🚀 사용 방법

### 1단계: 환경 설정

```python
# YouTube API 클라이언트
!pip install google-api-python-client

# 한국어 자연어처리
!pip install konlpy

# 데이터 분석 및 시각화
!pip install pandas numpy matplotlib seaborn wordcloud

# KoBERT 딥러닝
!pip install transformers torch sentencepiece
```

### 2단계: API 키 발급

1. [Google Cloud Console](https://console.cloud.google.com/) 접속
2. 새 프로젝트 생성
3. YouTube Data API v3 활성화
4. API 키 생성

### 3단계: 설정 수정

```python
# API 키 입력
API_KEY = "YOUR_API_KEY_HERE"

# 검색 키워드
KEYWORD = "검색어"

# 수집 설정
MAX_VIDEOS = 10          # 검색할 최대 동영상 수
MAX_COMMENTS = 100       # 동영상당 최대 댓글 수
```

### 4단계: 분석 실행
각 셀을 순차적으로 실행하여 분석을 수행합니다.

## 📊 분석 파이프라인

```
API 키 설정 → 동영상 검색 → 댓글 수집 → 텍스트 전처리
                                          ↓
                          KoBERT 감성분석 ← 혐오표현 탐지
                                          ↓
                                   종합 분석 및 시각화
```

## ⚖️ API vs 크롤링 비교

| 항목 | YouTube API | 크롤링 |
|------|-------------|--------|
| 안정성 | ✅ 높음 | ⚠️ 변동 가능 |
| 속도 | ✅ 빠름 | 🐢 느림 |
| 제한 | 일일 할당량 | 차단 위험 |
| 데이터 품질 | ✅ 정확 | ⚠️ 파싱 오류 가능 |
| 합법성 | ✅ 공식 지원 | ⚠️ ToS 위반 가능 |

## 🤖 KoBERT 감성분석

Hugging Face의 사전학습된 한국어 감성분석 모델을 사용합니다.

| 감성 | 설명 |
|-----|------|
| Positive (긍정) | 긍정적인 감정 표현 |
| Neutral (중립) | 중립적인 표현 |
| Negative (부정) | 부정적인 감정 표현 |

**주요 특징**:
- 사전학습된 한국어 BERT 모델 활용
- Hugging Face transformers 라이브러리
- 신뢰도(confidence) 점수 제공

## 🚫 혐오표현 탐지

7가지 유형의 혐오표현을 자동으로 탐지합니다:

| 유형 | 설명 |
|-----|------|
| 성별 혐오 | 성별 기반 비하 표현 |
| 지역 혐오 | 지역 기반 비하 표현 |
| 정치 혐오 | 정치 성향 기반 비하 |
| 외국인 혐오 | 외국인/이주민 비하 |
| 세대 혐오 | 세대 기반 비하 |
| 일반 욕설 | 일반적인 비속어 |
| 기타 비하 | 기타 비하 표현 |

## ⚙️ 설정 옵션

| 파라미터 | 설명 | 기본값 |
|---------|------|--------|
| `API_KEY` | YouTube Data API 키 | - |
| `KEYWORD` | 검색 키워드 | - |
| `MAX_VIDEOS` | 검색할 최대 동영상 수 | 10 |
| `MAX_COMMENTS` | 동영상당 최대 댓글 수 | 100 |

## 📁 출력 파일

### 분석 결과 (`youtube_api_kobert_analysis_{키워드}.csv`)

| 컬럼 | 설명 |
|-----|------|
| video_title | 동영상 제목 |
| channel | 채널명 |
| text | 원본 댓글 |
| cleaned_text | 전처리된 댓글 |
| likes | 좋아요 수 |
| sentiment | 감성 (긍정/중립/부정) |
| sentiment_confidence | 감성 분류 신뢰도 |
| sentiment_score | 감성 점수 |
| has_hate | 혐오표현 포함 여부 |
| hate_types | 혐오표현 유형 |
| hate_words | 감지된 혐오 단어 |
| hate_score | 혐오 점수 |
| keywords | 추출된 키워드 |

## 📈 시각화 항목

1. **KoBERT 감성 분포**: 긍정/중립/부정 비율 파이 차트
2. **혐오표현 비율**: 혐오 포함 비율
3. **채널별 댓글 수**: 채널별 댓글 분포
4. **키워드 TOP 10**: 자주 등장하는 단어
5. **혐오 유형 분포**: 유형별 혐오표현 빈도
6. **신뢰도 vs 좋아요**: 감성 신뢰도와 좋아요 관계

## 📋 요구사항

- Python 3.x
- Google Colab 환경 (권장)
- YouTube Data API 키
- GPU 사용 권장 (KoBERT 모델 추론 시)

### 주요 라이브러리
- `google-api-python-client`: YouTube API 클라이언트
- `konlpy`: 한국어 형태소 분석
- `pandas`, `numpy`: 데이터 처리
- `matplotlib`, `seaborn`: 시각화
- `wordcloud`: 워드클라우드 생성
- `transformers`, `torch`: KoBERT 감성분석

## 🔧 문제 해결

### API 할당량 초과
- 일일 할당량(10,000 units)을 초과하면 다음 날까지 대기
- 여러 프로젝트를 생성하여 API 키 분산 사용 가능

### KoBERT 모델 로드 실패
- GPU 메모리 부족 시 배치 크기를 줄이세요
- 네트워크 오류 시 모델을 다시 다운로드하세요

### 댓글이 수집되지 않는 경우
- 댓글이 비활성화된 동영상일 수 있음
- API 키가 올바른지 확인

### 한글 폰트 오류
- Colab에서 나눔폰트 설치 코드를 다시 실행
- 런타임을 재시작

## 🔗 API 키 발급 방법

1. [Google Cloud Console](https://console.cloud.google.com/) 접속
2. 새 프로젝트 생성 또는 기존 프로젝트 선택
3. "API 및 서비스" → "라이브러리" 이동
4. "YouTube Data API v3" 검색 후 활성화
5. "API 및 서비스" → "사용자 인증 정보" 이동
6. "사용자 인증 정보 만들기" → "API 키" 선택
7. 생성된 API 키 복사

## ⚠️ 주의사항

- API 키를 공개 저장소에 업로드하지 마세요
- 일일 할당량(10,000 units)을 초과하지 않도록 주의
- 수집한 데이터는 개인 연구 목적으로만 사용
- YouTube 서비스 약관을 준수하세요

## 📚 참고 자료

- [YouTube Data API 공식 문서](https://developers.google.com/youtube/v3)
- [Google Cloud Console](https://console.cloud.google.com/)
- [Hugging Face Korean Models](https://huggingface.co/models?language=ko)
- [KoNLPy 문서](https://konlpy.org/)

## 📜 라이선스

이 프로젝트는 교육 및 연구 목적으로 제작되었습니다.
