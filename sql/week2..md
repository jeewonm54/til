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

![sql5]()

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
 kor_name = "피카츄"
```
