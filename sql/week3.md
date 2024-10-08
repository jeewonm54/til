### 연습문제 1. 포켓몬 중에 type2가 없는 포켓몬의 수를 작성하는 쿼리를 작성해주세요
   
![week3_sql1](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql1.png)

### NULL은 뭘까?

 - 아무것도 없는 값. 값이 존재하지 않을 때 NULL이라고 표시함 
 
 - NULL 은 0 이랑 다르고, ""과도 다름 => 값이 아예 없는 상태. 결측치
 
 - 연산자 : IS NULL
 
 - type2 IS NULL
 
 - NULL은 다른 값과 직접 비교할 수 없음. NULL = NULL 거짓이 아니라 알 수 없음
 
 - 핵심 : NULL은 IS 연산자를 사용한다 !!

- WHERE 절에서 여러 조건을 연결하고 싶은 경우 => AND 조건을 사용
- OR 조건 => (  ) OR (  )
---

### 연습문제 2. type2가 없는 포켓몬의 type1과 type1의 포켓몬 수를 알려주는 쿼리를 작성해주세요. 단, typw1의 포켓몬 수가 큰 순으로 정렬해주세요.
    
![week3_sql2.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql2.png)

- 빨간 밑줄 : 에러 메ㅔ지
- 집계 함수는 GROUP BY 와 같이 다님. 집계하는 기준(컬럼)이 없으면 COUNT만 쓸 수 있으나, 집계하는 기준이 있다면 그 기준 칼럼을 GROUP BY에 써줘야 한다.
---

### 연습문제 3. type2 상관없이 type1의 포켓몬 수를 알 수 있는 쿼리를 작성해주세요

![week3_sql3.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql3.png)

- DISTINCT 언제 쓸까? => 고유한 값만 보고 싶을 때 사용한다. Unique 한 값만 알고 싶은 경우 사용
- IF id를 설걔할 때, 중복이 없게 설계한 상황이라면(두개의 결과가 동일한 상)
- COUNT(id) = COUNT(DISTINCT id)
- BUT 어떤 컬럼은 중복이 있게 설계되곤 함.
- 그렇기에 DISTINCT 도 걸어보고 어떤 값이 더 맞을지 고민 ㄱ ㄱ
---

### 연습문제 4. 전설 여부에 따른 포켓몬 수를 알 수 있는 쿼리를 작성해주세요. 

![week3_sql4.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql4.png)

- 칼럼의 이름 앞부분 일부를 입력하고 기다리면 자동 완성을 할 수 있는데, 이 때 찾아서 엔터
- GROUP BY : is_legendary 가 길다. GROUP BY 에 칼럼이 많이 있을 수도 있음
- 이때 GROUP BY 1 => SELECT의 첫 컬럼을 의미
- ORDER BY 에도 1,2 등을 사용할 수 있음
- 1, 2 => 쿼리를 빠르게 작성하고, 결과를 보는 과정에서 사용하기. 완성된 쿼리문에서는 1, 2 같은 표현보단 명확하게 컬럼을 명시하는게 좋다.(가독성 관점에서)
---

### 연습문제 5. 동명 이인이 있는 이름은 무엇일까요? 

![week3_sql5.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql5.png)

- 집계 후 조건 => HAVING, FROM
- WHERE : 원본 데이터 FROM 절에 있는 데이터에 조건을 설정하고 싶은 경우
- HAVING : GROUP BY 와 함께 집계 결과에 조건을 설정하고 싶은 경우 
- 서브쿼리 : 쿼리문을 한번 감싸서 다른 쿼리문에서 사용할 수 있음
- HAVING 을 쓰면 쿼리 줄 수가 줄어듦
---

### 연습문제 6. trainer 테이블에서 "Iris" 트레이너의 정보를 알 수 있는 쿼리를 작성해주세요.

![week3_sql6.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql6.png)

---

### 연습문제 7. trainer 테이블에서 "Iris", "WHitney", "Cynthia" 트레이너의 정보를 알 수 있는 쿼리를 작성해주세요. 

![week3_sql7.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql7.png)

- OR 조건으로 쓰는거 너무 길다. 귀찮다 => IN => name에 괄호 안의 Value가 있는 Row만 추출
---

### 연습문제 8. 전체 포켓몬 수는 얼마나 되나요?

![week3_sql8.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql8.png)

---

### 연습문제 9. 세대(Generation) 별로 포켓몬 수가 얼마나 되는지 알 수 있는 쿼리를 작성해주세요.

![week3_sql9.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql9.png)

---
### 연습문제 10. type2가 존재하는 포켓몬의 수는 얼마나 되나요? 

![week3_sql10.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql10.png)

---
### 연습문제 11. type2가 있는 포켓몬 중에 제일 많은 type1은 무엇인가요?

![week3_sql11.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql11.png)

---
### 연습문제 12. 단일(하나의 타입만 있는) 타입 포켓몬 중 많은 type1은 무엇일까요?

![week3_sql12.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql12.png)

---
### 연습문제 13. 포켓몬의 이름에 "파"가 들어가는 포켓몬은 어떤 포켓몬이 있을까요?

![week3_sql13.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql13.png)

- 칼럼 LIKE "특정단어%", %는 앞에도 붙을 수 있고, 뒤에도 붙을 수 있음
- %파 : 파로 끝나는 단어, 파% : 파로 시작하는 단어, %파% : 파가 들어간 단어
- 문자열 칼럼에서 특정 단어가 포함되어 있는지 알고 싶은 경우엔 LIKE를 사용하면 편함
---
### 연습문제 14. 뱃지가 6개 이상인 트레이너는 몇 명이 있나요?

![week3_sql14.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql14.png)

---
### 연습문제 15. 트레이너가 보유한 포켓몬(trainer_pokemon)이 제일 많은 트레이너는 누구일까?

![week3_sql15.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql15.png)

---
### 연습문제 16. 포켓몬을 많이 풀어준 트레이너는 누구일까?

![week3_sql16.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql16.png)

---
### 연습문제 17. 트레이너 별로 풀어준 포켓몬의 비율이 20%가 넘는 포켓몬 트레이너는 누구일까요? 풀어준 포켓몬 비율 = (풀어준 포켓몬 수/전체 포켓몬의 수)

![week3_sql17.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql17.png)

---


### 정리

![week3_sql18.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql18.png)


### GROUP BY ALL
:  Group By 함수에 칼럼을 명시하지 않고 GROUP BY ALL 함수 사용 가능!

---
# 섹션3

## SQL 쿼리 작성하는 흐름 

![week3_sql19.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql19.png)

## 쿼리 작성 템플릿 

-- 쿼리를 작성하는 목표, 확인할 지표:

-- 쿼리 계산 방법:

-- 데이터의 기간 :

-- 사용할 테이블 :

-- Join KEY :

-- 데이터 특징 :

```
SELECT

FROM
WHERE
```

## 생산성 도구 : Espanso

특정한 단어를 입력하면 원하는 문장(템플릿)으로 변경해줌

![week3_sql20.png](https://github.com/jeewonm54/til/blob/31d01a06a00bcfb0e02038b1b423e37d4d396deb/img/week3_sql20.png)
