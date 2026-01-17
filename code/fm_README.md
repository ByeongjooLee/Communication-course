# 🔍 에프엠코리아 크롤러 (Google Colab 전용)

Selenium 기반의 에프엠코리아(FMKorea) 게시물 및 댓글 크롤러입니다. Google Colab 환경에서 최적화되어 작동합니다.

## ✨ 주요 기능

- **키워드 검색**: 원하는 키워드로 게시물 검색
- **날짜 필터링**: 특정 기간 내 게시물만 수집
- **상세 정보 수집**: 제목, 작성자, 날짜, 본문 내용
- **댓글 수집**: 각 게시물의 댓글 작성자 및 내용
- **Excel 저장**: 결과를 Excel 파일로 자동 저장 및 다운로드

## 📋 요구사항

- Google Colab 환경
- Python 3.x
- 인터넷 연결

## 🚀 사용 방법

### 1단계: 환경 설정
첫 번째 셀을 실행하여 필요한 패키지를 설치합니다.

```python
!pip install selenium
!apt-get update
!apt install -y chromium-chromedriver
```

### 2단계: 크롤러 클래스 로드
두 번째 셀을 실행하여 크롤러 클래스를 로드합니다.

### 3단계: 크롤링 설정 및 실행

```python
# 크롤러 초기화
crawler = FMKoreaCrawlerSelenium(delay_min=3, delay_max=6)

# 설정값 지정
KEYWORD = "검색어"        # 검색할 키워드
MAX_POSTS = 50            # 최대 수집 게시물 수
START_DATE = "2024-01-01" # 시작 날짜
END_DATE = "2025-12-31"   # 종료 날짜

# 크롤링 실행
posts_data, comments_data = crawler.crawl_with_details(
    keyword=KEYWORD,
    max_posts=MAX_POSTS,
    start_date=START_DATE,
    end_date=END_DATE
)
```

### 4단계: 결과 확인 및 저장
크롤링 완료 후 자동으로 Excel 파일이 생성되어 다운로드됩니다.

## ⚙️ 설정 옵션

| 파라미터 | 설명 | 기본값 |
|---------|------|--------|
| `delay_min` | 요청 간 최소 대기 시간(초) | 3 |
| `delay_max` | 요청 간 최대 대기 시간(초) | 6 |
| `max_pages` | 최대 검색 페이지 수 | 50 |
| `max_posts` | 최대 수집 게시물 수 | 200 |
| `start_date` | 수집 시작 날짜 | 2024-01-01 |
| `end_date` | 수집 종료 날짜 | 2025-12-31 |

## 📁 출력 파일 형식

### 게시물 데이터 (`{키워드}_게시물_{타임스탬프}.xlsx`)
| 컬럼 | 설명 |
|-----|------|
| title | 게시물 제목 |
| url | 게시물 URL |
| author | 작성자 |
| date | 작성 날짜 |
| content | 본문 내용 |
| keyword | 검색 키워드 |
| comment_count | 댓글 수 |

### 댓글 데이터 (`{키워드}_댓글_{타임스탬프}.xlsx`)
| 컬럼 | 설명 |
|-----|------|
| post_title | 원본 게시물 제목 |
| post_url | 원본 게시물 URL |
| comment_author | 댓글 작성자 |
| comment_content | 댓글 내용 |
| keyword | 검색 키워드 |

## ⚠️ 주의사항

- 과도한 크롤링은 서버에 부담을 줄 수 있습니다
- 요청 간 적절한 딜레이를 유지하세요 (기본 3~6초)
- 수집한 데이터는 개인 연구 목적으로만 사용하세요
- 웹사이트의 이용약관을 준수하세요

## 🔧 문제 해결

### 크롤링이 중간에 멈추는 경우
- `delay_min`, `delay_max` 값을 늘려보세요
- 일시적인 네트워크 오류일 수 있으니 재실행해보세요

### 게시물을 찾지 못하는 경우
- 검색 키워드를 확인하세요
- 날짜 범위가 올바른지 확인하세요

### 브라우저 종료
크롤링 완료 후 반드시 브라우저를 종료하세요:
```python
crawler.close()
```

## 📜 라이선스

이 프로젝트는 교육 및 연구 목적으로 제작되었습니다.
