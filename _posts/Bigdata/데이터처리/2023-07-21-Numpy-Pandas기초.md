---
title: "[Data] Numpy/Pandas 기초"
date: 2023-07-20 21:00:00 +09:00
categories: [Bigdata, 데이터처리]
tags: [Python, Numpy, Pandas]
---

판다스와 넘파이 기초

<!-- ## 목차
- [용어](#용어)
- [Data Cleansing Process](#data-cleansing-process)
  * [Importing Data](#importing-data)
  * [데이터 특성 및 오류 점검](#데이터-특성-및-오류-점검)
  * [Scrub for Duplicate](#scrub-for-duplicate)
  * [Scrub for Irrlevant / Incorrect Data](#scrub-for-irrlevant--incorrect-data) -->

## 용어
DataFrame  
Series - 열  
Columns - axis=1  
Index - axis=0, 행 이름  

## Data Cleansing Process
### Importing Data
- `pd.read_csv(파일명)`

### 데이터 특성 및 오류 점검
- `df.head()` - 첫 5개 데이터 반환
- `df명.info()` - 정보

### Scrub for Duplicate
- `df명.drop_duplicates()` - 중복 데이터 제거
- `df명.set_index(’열이름’)` - 분석에 사용 안 되는데 레코드 구분에 도움이 되는 열 index로 지정!! **지정한 열을 인덱스(행이름)으로 지정.**
- `df명.reset_index()` - 기존 인덱스를 첫 번째 열로 생성, 인덱스 01234.. 형식으로 복원
    - **drop=True** 옵션 - **복원시 인덱스 제거** - **인덱스 재설정**

<br>

### Scrub for Irrlevant / Incorrect Data
**날짜 데이터**
- `pd.to_datetime(Series)` - series를 datetime형식으로 변환
    - `errors=`
        - `'raise’` - 에러 발생 (default)
        - `‘coerce’` - 바꿀 수 있는 값은 바꾸고 못 바꾸는 건 NaT 결측치 처리 ← 오류 X
        - `‘ignore’` - 오류나면 반환 X
- `.dt.weekday` - 요일 숫자로. 정렬 가능! 0-월, 1-화 (int)
- `.dt.is_month_end` - 말일 여부(bool)

- `pd.date_range()` - 일정 기간의 날자 만들기
- `pd.Timedelta()` - 시간간격 다루기

<br>

**새로운 열 생성 / 데이터 프레임의 수정**
- 맨 뒤에 열 추가 - df명[’새로운열이름’] = pd.Series
- 지정 위치에 열 추가 - df명.insert(위치, ‘새로운열이름’, pd.Series) → 바로 update되니 앞에 df = 같은 거 하면 안 됨.
- 이름 변경 - df명.rename(index={’기존행이름’:’바꿀행이름’,…}, columns={’기존열이름’:’바꿀열이름’,…})
- 삭제 - df명.drop([’이름1’, ‘이름2’, … ], axis=’index’)
    - 행 삭제 - axis=0 or axis=’index’
    - 열 삭제 - axis=1 or axis=’columns’

<br>

**행 == index == axis=0**  
**열 == columns == axis=1**