## 8. 총 정리 문제 풀이

### 문제 1. 
각 트레이너별로 가진 포켓몬의 평균 레벨을 계산하고, 그 중 평균 레벨이 높은 top3 트레이너의 이름과 보유한 포켓몬의 수, 평균 레벨 출력
 ```SQL 
 WITH trainer_avg_level AS (
  SELECT
  trainer_id,
  ROUND(AVG (level), 2) As avg_level,
  count (id) As pokemon_cnt
FROM basic.trainer_pokemon
WHERE
  status != "Released" 
Group By
  trainer_id  
)

SELECT
  t.name,
  tal.avg_level,
  tal.pokemon_cnt
FROM basic. trainer AS t
LEFT JOIN trainer_avg_level AS tal 
ON t.id=tal.trainer_id  
ORDER BY 
  avg_level DESC
Limit 3
 ```


### 문제 2. 
각 포켓몬 타입1을 기준으로 가장 많이 포획된(방출 여부 상관없음) 포켓몬의 타입1, 포켓몬의 이름과 포획 횟수 출력
```SQL
SELECT
  type1,
  kor_name,
  COUNT(tp.id) AS cnt
FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id = p.id
GROUP BY
  type1,
  kor_name
ORDER BY
  cnt DESC
LIMIT 1
```


### 문제 3. 
전설의 포켓몬을 보유한 트레이너들은 전설의 포켓몬과 일반 포켓몬을 얼마나 보유하고 있을까? (트레이너의 이름을 함께 출력)

=> COUNTIF, SUM(CASE WHEN ~) 둘다 사용 가능
```SQL
WITH legendary_cnts AS(
  SELECT
    tp.trainer_id,
    SUM(CASE
      WHEN p.is_legendary IS TRUE THEN 1 ELSE 0 END) AS legendary_cnt,
    SUM(CASE
      WHEN p.is_legendary IS NOT TRUE THEN 1 ELSE 0 END) AS normal_cnt
  FROM basic.trainer_pokemon AS tp 
  LEFT JOIN basic.pokemon AS p
  ON tp.pokemon_id = p.id
  WHERE tp.status IN ("Active", "Training")
  GROUP BY
  tp.trainer_id
)

# legendary_cnts + trainer
SELECT
 t.name AS trainer_name,
 lc.legendary_cnt,
 lc.normal_cnt
FROM basic.trainer AS t
LEFT JOIN legendary_cnts AS lc
ON t.id = lc.trainer_id
WHERE
 lc.legendary_cnt >= 1

```


### 문제 4. 
가장 승리가 많은 트레이너 id, 트레이너의 이름, 승리한 횟수, 보유한 포켓몬의 수, 평균 포켓몬의 레벨 출력. 단, 포켓몬의 레벨은 소수점 둘째자리에서 반올림

참고. 반올림 함수: ROUND

쿼리 계산 방법 : battle 테이블 => winner_id. 승리 횟수를 COUNT + 트레이너 이름 + trainer_pokemon의 포켓몬 수, 포켓몬 레벨
```SQL
# 1. winner_id COUNT (승리 횟수)
WITH winner_counts AS(
    SELECT
    winner_id,
    count(winner_id) AS win_counts
    FROM basic.battle 
    WHERE
    winner_id IS NOT NULL 
    GROUP BY
    winner_id
),

# 2. 이름추가
top_winner AS (
    SELECT
    wc.winner_id as trainer_id,
    wc.win_count,
    t.name as trainer_name
    FROM winner_counts AS wc
    LEFT JOIN basic.trainer AS t
    ON wc.winner_id = t.id
    ORDER BY 
     win_counts DESC
    LIMIT 1
)

# 3.  평균 포켓몬 수, 레벨 추가
SELECT
  tw.trainer_id,
  tw.trainer_name,
  tw.win_counts,
  count(tp.pokemon_id) AS pokemon_cnt,
  ROUND(AVG(tp.level),2) AS avg_level

FROM top_winner AS tw
LEFT JOIN basic.trainer_pokemon AS tp
ON tw.trainer_id = tp.trainer_id
WHERE 
  tp.status IN ("ACTIVE","Training")
GROUP BY
  tw.trainer_id,
  tw.trainer_name,
  tw.win_counts
```


### 문제 5. 
트레이너가 잡았던 포켓몬의 총 공격력(attack)과 방어력(defense)의 합을 계산하고, 이 합이 가장 높은 트레이너를 찾아보자.
```SQL
#트레이너가 보유한 포켓몬들의 attack, defense 합치기 
WITH total_stats AS(
    SELECT
    trainer_id,
    -- p.attack,
    -- p.defense,
    SUM(p.attack + p.defense) AS total_stat
    FROM basic.trainer_pokemon AS tp
    LEFT JOIN basic.pokemon AS p
    ON tp.pokemon_id = p.id
    GROUP BY
    tp.trainer_id
)

SELECT
 t.name, 
 trainer_id,
 total_stat
FROM total_stats AS ts
LEFT JOIN basic.trainer AS t
ON ts.trainer_id = t.id
ORDER BY
  total_stat DESC
LIMIT 1
```


### 문제 6. 
각 포켓몬의 최고 레벨과 최저 레벨을 계산하고, 레벨 차이가 가장 큰 포켓몬의 이름을 출력하라.

- 포켓몬 레벨 차이(최고 레벨 - 최저 레벨)
- trainer_pokemon에서 포켓몬의 최고 레벨, 최저 레벨을 계산 -> 차이를 구하고 -> 차이가 큰 순으로 정렬
```SQL
# 1. 레벨 차이 구하기
WITH level_diff AS(
  SELECT
    tp.pokemon_id,
    p.kor_name,
    MIN(tp.level) AS min_level,
    MAX(tp.level) AS max_level,
    Max(tp.level) - MIN(tp.level) as level_differnce
  FROM basic.trainer_pokemon as tp
  LEFT JOIN basic.pokemon as p
  ON tp.pokemon_id = p.id
  GROUP BY
  tp.pokemon_id,
  p.kor_name
)
  # pokemon_id => min lvl:6, max lvl:22. lvl_differnece = 16

# 2. 
SELECT
  kor_name,
  level_differnce
FROM level_diff
ORDER BY
  level_differnce DESC
LIMIT 1
```


### 문제 7. 
각 트레이너가 가진 포켓몬 중에서 공격력(attack)이 100 이상인 포켓몬과 100 미만인 포켓몬의 수를 각각 계산하라. 트레이너의 이름과 두 조건에 해당하는 포켓몬의 수를 출력하라.
- COUNTIF 사용
```SQL
WITH active_and_training_pokemon AS (
  SELECT
      *
  FROM basic.trainer_pokemon 
  WHERE 
   status IN ("Active", "Training")
), trainer_high_and_low_attack_cnt AS (
  SELECT
    atp.trainer_id,
    #trainer_name은 이후에 JOIN
    COUNTIF(p.attack >= 100) AS high_attack_cnt,
    COUNTIF(p.attack < 100) AS low_attack_cnt
    FROM active_and_training_pokemon AS atp
    LEFT JOIN basic.pokemon AS p
    ON atp.pokemon_id = p.id
    GROUP BY 
    atp.trainer_id
)

SELECT
 t.name,
 thala.*
FROM trainer_high_and_low_attack_cnt AS thala
LEFT JOIN basic.trainer AS t
ON thala.trainer_id = t.id
```

## 전체 총정리

### 쿼리작성 템플릿
쿼리를 작성하는 목표, 확인할 지표:

쿼리 계산 방법:

데이터의 기간:

사용할 테이블:

Join Key:

데이터 특징:


