## 오류를 디버깅 하는 방법

 syntax : 문법
 syntax error : 문법 오류

 오류 메세지가 알려주고자 하는 것
 - 현재 작성한 방식으로 하면 답을 얻을 수 없어요 (길잡이 역할)
 - 이부분에 문제가 되어요 (문제 진단)

 오류가 발생하면
 -> 아 길잡이가 나를 더 좋은 길로 나아가게 하려는구나!

### 대표적인 오류 카테고리 : Syntax Error (문법 오류)
- 문법을 지키지 않아 생기는 오류
- Error Message를 보고 번역 또는 해석한 후, 해결 방법  찾아보기
     - 구글에 검색
    - ChatGPT에 질문
    - 지인에게 질문


- 빨간 밑줄이 있으면 밑줄 앞뒤로 오류가 있을 가능성 큼


< Number of argurments does not match for aggregate function COUNT

```
SELECT
 COUNT (id, kor_name)
FROM basic.pokemon
```
해석 : 집계 함수 COUNT의 인자 수가 일치하지 않습니다. 

=> 
COUNT(1개만 들어가야됨)

< SELECT list expression references column type1 a which is neither grouped nor aggregated 

```
SELECT
 type1,
 COUNT (id) AS cnt
FROM basic.pokemon
```
해석 : SELECT 목록 식은 다음에서 그룹화되거나 집계되지 않은 열을 참조합니다. 

=> GROUP BY에 적절한 컬럼을 명시하지 않았을 경우 발생하는 오류

< Syntax error : Expected end of input but got keyword SELECT>

```
SELECT
 type1,
 COUNT (id) AS cnt
FROM basic.pokemon
GROUP BY 
 type1

SELECT
*
FROM basic.trainer
```
해석 : 입력이 끝날 것으로 예상되었지만 SELECT 키워드가 입력되었습니다.

- SELECT 근처 확인하기
- 하나의 쿼리엔 SELECT가 1개만 있어야 함
- 혹은 쿼리가 끝나는 부분에 ; 붙이고 실행할 부분만 드래그 앤 드랍해서 실행하기 

< Syntax error : Expected end of input but got keyword WHERE at [5:1]>

```
SELECT
 *
FROM basic.trainer LIMIT 10
WHERE
 id=3
```
해석 : 입력이 끝날 것으로 예상되었지만 [5:1]에서 키워드 WHERE을 얻었습니다. 
- limit을 옮기거나 삭제하면됨

## 데이터 변환
### 변화을 위한 함수
- SELECT 문에서 데이터를 변환시킬 수 있음
    - 또는 WHERE의 조건문에도 사용할 수도 있음
- 데이터의 타입에 따라 다양한 함수가 존재 

```
SELECT
 칼럼1,
 칼럼2,
 칼럼3
FROM 테이블
WHERE <조건문>
GROUP BY <집계할 컬럼>
```

### 데이터 타입 
숫자, 문자, 시간날짜, 부울(Bool  )

### 데이터 타입이 중요한 이유
- 보이는 것과 저장된 것의 차이가 존재한다
    - 엑셀에서 보면 빈값 => ""일 수도 있고, NULL일 수도 있음
    - 1이라고 작성된 경우 => 숫자 1일 수도 있고, 문자 1일 수도 있음
    - 2023-12-31 => DATE 2023-12-31 일 수도 있고, 문자 2023-12-31 일 수도 있음
    - 내 생각과 다른 경우 데이터의 타입을 서로 변경해야 함

### 자료 타입 변경하기
자료 타입을 변경하는 함수 : SAFE_CAST
- SAFE_가 붙은 함수는 변환이 실패할 경우 NULL 변환됨

![week4_1]()