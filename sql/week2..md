# 데이터 탐색 (SELECT, FROM, WHERE)
SQL 쿼리 구조
SELECT -> FROM -> WHERE

**SELECT**:  테이블의 어떤 컬럼을 선택(출력)할 것인가?
COL1 AS new_ name,      (여기서 new_name 은 별)
Col2,
Col3,
**FROM** Dataset, Table : 어떤 테이블에서 데이터를 확인할 것인가?
**WHERE**: 만약 원하는 조건이 있다면 어떤 조건인가?
 Col1 = 1 : 조건문

```
select
 id
from 'basic.pokemon'
where
 type1 = "Fire"
```


#til-bigquery : 프로젝트명 
#basic : dataset
#pokemon : table
#<프로젝트 id>, <데이터셋>, <테이블>
#프로젝트 id는 꼭 명시할 필요는 없을 수도 있음(프로젝트가 단일이라면!)
#프로젝트를 여러개 사용한다면 명시하는 것이 좋음 ==> 쿼리를 실행할 때 어떤 프로젝트인지 확인하는 과정이 존재
#프로젝트 명시 ==> tbh 불편함
#프로젝트를 제외하고 사용해도 괜찮긴 함(여러 프로젝트를 쓸 때는 명시해야 한다)
#프로젝트 id를 제외하고 작성할 때는 ' 없어도 괜찮음

 * : 모든 컬럼을 출력하겠다 (비용이 많이 나간다..)

모든 데이터, 모든 컬럼을 출력하고 싶을 때 
```
select
 *
from 'basic.pokemon'
where
 type1 = "Fire"
```
#데이터를 어떻게 활용하고 싶냐에 따라 활용하고 싶은 목적이 있어야 어떤 컬럼을 선택할지 알 수 있게됨

#as 는 별칭을 지어줄 때 사용한다. 
```
select
 id as pokemon_id
from 'basic.pokemon'
where
 type1 = "Fire"
```

SELECT
 * EXCEPT(제외할 칼럼)
이런 형태도 가능. 칼럼이 많을 때 유용. JOIN세어 사용할 때도 유용 
tbh 현업에서 SELECT* 사용 잘 안함. 
```
select
 *EXCEPT(eng_name)
from 'basic.pokemon'
where
 type1 = "Fire"
```

#세미콜론이 있는 경우 : 하나의 커리가 끝났다

![sql5](https://github.com/jeewonm54/til/blob/3c2bd48adfee196ac44be287ae0c06ab168d96b4/img/sql5.png)

*자주하는 실수*
컬럼 이름에 따옴표를 넣는 경우 ==> AS 에서는 따옴표 없이 기록한다

# SELECT 연습문제
1. trainer 테이블에 있는 모든 데이터를 보여주는 SQL 쿼리를 작성해주세요
 1) trainer 테이블에 어떤 데이터가 있는지 확인해보자
 2) trainer 테이블을 어디에 명시해야 할까? => FROM
 3) 필터링 조건이 없을까? => 모든데이터 => 필터링을 할 필요가 없겠다
 4) 모든 데이터 => 모든 컬림일 수도 있겠다(추측) 쿼리 작성 => 애매하면 모든 데이터 정의가 무엇인가?
``` 
select
 *
from basic.trainer 
```

2. trainer 테이블에 있는 트레이너의 name을 출력하는 쿼리를 작성해주세요
 1) trainer 테이블 사용
 2) name 칼럼을 사용
```    
select
 name
from basic.trainer 
```

3. trainer 테이블에 있는 트레이너의 name, age를 출력하는 쿼리를 작성해주세요
   1) trainer 테이블 사용
   2) 조건 설정 없음
   3) name, age 칼럼 사용
  
```
select
 name, age
from basic.trainer 
```

4. trainer의 테이블에서 idrk 3인 트레이너의 name, age, hometown을 출력하는 쿼리를 작성해주세요
 1) trainer 테이블 사용
 2) 조건 설정 => id가 3인
 3) 칼럼: name, age, hometown
```    
select
 name, age, hometown
from basic.trainer 
where
 id = 3
```

5. pokemon 테이블에서 "피카츄"의 공격력과 체력을 확인할 수 있는 쿼리를 작성해주세요
 1) pokemon 테이블
 2) 조건? => "피카츄" kor_name => 피카츄
 3) 공격력, 체력 => 테이블에서 어떤 칼럼인지 확인해야 함 => attack, hp
```
select
  attack
  hp
from basic.pokemon 
where
 kor_name =등)
```

# 데이터 탐색 : 요약(집계, 그룹화) - COUNT, DISTINCT, GROUP BY

집계 : 그룹화해서 계산하다
GROUP BY : 같은 값끼리 모아서 그룹화한다
- 특정 칼럼을 기준으로 모으면서 다른 칼럼에선 집계 가능(합, 평균, MAX, MIN 등 )

```
SELECT
 집계할_컬럼1
 집계함수(COUNT, MAX, MIN 등)
FROM table
GROUP BY
 집계할_컬럼1

```
* 집계할 컬럼을 SELECT에 명시하고 그 컬럼을 꼭 GROUP BY에 작성하기

**DISTINCT : 고유값을 알고 싶은 경우 (중복을 제거하는 것)**
```
SELECT
 집계할_컬럼
 COUNT(DISTINT count할 컬럼)
FROM table
GROUP BY
 집계할_컬럼
```

**연습문제**
1. pokemon 테이블에 있는 포켓몬 수를 구하는 커리를 구하시오.
-- 사용할 테이블 : pokemon
-- 집계할 때 사용할 계산 : 수를 구한다 => COUNT, 포켓몬
```
SELECT
 count(id) AS cnt
FROM basic.pokemon
```

2. 포켓몬의 수가 세대별로 얼마나 있는지 알 수 있는 쿼리를 작성해주세요. 
-- 사용할 테이블 : pokemon
-- 그룹화를 할때 사용할 컬럼 : 세대 
-- 집계할 때 사용할 계산 : 얼마나 있는 => 수를 구한다 => COUNT
```
SELECT
 generation
 count(id) AS cnt
FROM basic.pokemon
GROUP BY
 generation
```

**그룹화(집계) 활용 포인트**
- 일자별 집계(원본 데이터는 특정 시간에 어떤 유저가 한 행동이 기록, 일자별로 집계)
- 연령대별 집계(특정 연령대에서 더 많이 구매했는가?)
- 특정 타입별 집계(특정 제품 타입을 많이 구매했는가?)
- 앱 화면별 집계(어떤 화면에 유저가 많이 접근했는가?)
- etc

**조건을 설정하고 싶은 경우: WHERE**
*table에 바로* 조건을 설정하고 싶은 경우 사용
Raw Data 인 테이블 데이터에서 조건 설정 
```
SELECT
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM <table>
WHERE
 컬럼1>=3
```
**조건을 설정하고 싶은 경우: HAVING**
*GROUP BY한 후* 조건을 설정하고 싶은 경우 사용
```
SELECT
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM <table>
WHERE
GROUP BY 컬럼1, 컬럼2
HAVING
 col1_count>3
```
**WHERE + HAVING**
```
SELECT
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM <table>
WHERE
 컬럼1 >=3
GROUP BY 컬럼1, 컬럼2
HAVING
 col1_count>3
```

**서브쿼리**
- SELCT 문 안에 존재하는 SELECT 쿼리
- FROM 절에 또 다른 SELECT 문을 넣을 수 있음
- 괄호로 묶어서 사용
-> 서브쿼리를 작성하고, 서브쿼리 바깥에서 WHERE 조건 설정하는 것
  = 서브쿼리에서 HAVING으로 하는 것

**정렬하기 : ORDER BY**
```
SELCET
 col
FROM
ORDER BY <컬럼><순서>
```
순서: DESC(내림차순), OSC(오름차순 -  보통 Default)
쿼리의 맨 마지막에만 쓰면 됨

**출력 개수 제한하기 : LIMIT**
쿼리문의 결과 Row 수를 제한하고 싶은 경우 사용
```
SELCET
 col
FROM
LIMIT 10
```
쿼리의 맨 마지막에 작성

**GROUP BY 연습문제**
3. 포켓몬의 수를 타입 별로 집계하고, 포켓몬의 수가 10 이상인 타입만 남기는 쿼리를 작성해주세요. 포켓몬의 수가 많은 순으로 정리해주세요.
-- pokemon
-- 조건(WHERE) => 테이블 원본 => 없음
-- 집계 후 조건(HAVING) => 10 이상
-- 포켓몬의 수가 많은 순으로 정렬 (ORDER BY 포켓몬 수 DESC)
```
SELCET
 type1,
 COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
 type1
HAVING cnt >= 10
ORDER BY cnt DESC
```

--
집계하고 싶은 경우 : GROUP BY + 집계 함수(AVG, MAX 등) 
고유값을 알고 싶은 경우 : DISTINCT
조건을 설정하고 싶은 경우 : WHERE / HAVING
정렬을 하고 싶은 경우 : ORDER BY
출력 개수를 제한하고 싶은 경우 : LIMIT
--
