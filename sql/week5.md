4-4. 날짜 및 시간 데이터 이해하기 

CURRENT _DATETIME([time_zone]) : 현재 Datetime 출력

**EXTRACT** : Datetime 에서 특정 부분만 추출하고 싶은 경우  

- 날짜, 년도, 월, 일, 시간, 시, 분 단위로 특정 부분만 추출하는 함수

!(week5_1)[]

- 요일을 추출하고 싶은 경우
  **EXTRACT(DAYOFWEEK FROM datetime_col)**
  - 한 주의 첫날이 일요일인 [1,7] 범위의 값을 반환
  - 주말만 찾고 싶으면 IN 조건 혹은 CASE WHEN 조과 함께 1,7 만 찾을 수 있음

- DATE 와 HOUR만 남기고 싶은 경우 => 시간 자르기
  **DATETIME_TRUNC(datetime_col, HOUR)**
  - "2021-01-01 14:42:13" 을 HOUR로 자르면 "2024-01-02 14:00:00"
  - !(week5_2)[]
 
- 문자열로 저장된 DATETIME을 DATETIME 타입으로 바꾸고 싶은 경우
  **PARSE_DATETIME('문자열의 형태', 'DATETIME 문자열') AS datetime**

- DATETIME 타입 데이터를 특정 행태의 문자열 데이터로 변환하고 싶은 경우
  **SELECT_DATETIME("%c", DATETIME "2024-01-11 12:35:35") AS formatted;**

!(week5_3)[]

- 마지막 날을 알고 싶은 경우; 자동으로 월의 마지막 값을 계산하여 특정 연산을 할 경우
  **LAST_DAY(DATETIME) : 월의 마지막 값을 반환**

- 두 DATETIME 의 차이를 알고 싶은 경우
  **DATETIME_DIFF(첫 DATETIME, 두 번째 DATETIME, 궁금한 차이)**

!(week5_4)[]


