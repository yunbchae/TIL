# MySQL

> [프로그래머스 SQL 고득점 Kit](https://programmers.co.kr/learn/challenges?tab=sql_practice_kit)

---

[TOC]

---



## SELECT

#### WHERE

```mysql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID;

SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID;
```



#### ORDER BY

```mysql
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC;
```



#### LIMIT

```mysql
SELECT NAME 
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1;
```



<a href="#MySQL">Top</a>



## SUM, MAX, MIN

#### MAX

```mysql
SELECT MAX(DATETIME) AS '시간'
FROM ANIMAL_INS;
```



#### MIN

```mysql
SELECT MIN(DATETIME) AS '시간'
FROM ANIMAL_INS;
```



#### COUNT

```mysql
SELECT COUNT(*)
FROM ANIMAL_INS;
```



#### DISTINCT

```mysql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
WHERE NAME is not NULL;
```



<a href="#MySQL">Top</a>



## GROUP BY

#### GROUP BY

```mysql
SELECT ANIMAL_TYPE, COUNT(*) AS 'COUNT'
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Cat'
OR ANIMAL_TYPE = 'Dog'
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE;
```



#### HAVING

```mysql
SELECT NAME, COUNT(*) AS 'COUNT'
FROM ANIMAL_INS
WHERE NAME is not NULL
GROUP BY NAME
HAVING COUNT(*) >= 2
ORDER BY NAME;
```



#### HOUR / BETWEEN

```mysql
SELECT HOUR(DATETIME) AS 'HOUR', COUNT(*) AS 'COUNT'
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) BETWEEN 9 AND 19
GROUP BY HOUR(DATETIME)
ORDER BY HOUR(DATETIME);
```



#### @variable

```mysql
SET @hour = -1;

SELECT  (@hour := @hour+1) AS 'HOUR',
        (SELECT COUNT(*) 
         FROM ANIMAL_OUTS 
         WHERE HOUR(DATETIME) = @hour) AS 'COUNT'
FROM    ANIMAL_OUTS
WHERE   @hour < 23;
```



<a href="#MySQL">Top</a>



## IS NULL

#### IS NULL

```mysql
SELECT ANIMAL_ID 
FROM ANIMAL_INS
WHERE NAME is NULL
ORDER BY ANIMAL_ID;

SELECT ANIMAL_ID 
FROM ANIMAL_INS
WHERE NAME is not NULL
ORDER BY ANIMAL_ID;
```



#### IFNULL

```mysql
SELECT ANIMAL_TYPE, IFNULL(NAME,'No name'), SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



<a href="#MySQL">Top</a>



## JOIN

#### INNER JOIN

```mysql
SELECT INS.ANIMAL_ID, INS.NAME
FROM ANIMAL_INS INS, ANIMAL_OUTS OUTS
WHERE INS.ANIMAL_ID = OUTS.ANIMAL_ID 
AND INS.DATETIME > OUTS.DATETIME
ORDER BY INS.DATETIME;
```



#### Cheatsheet



<img src="https://i.stack.imgur.com/SIc33.png" />



<a href="#MySQL">Top</a>



## String, Date

#### IN

```mysql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy','Ella','Pickle','Rogan','Sabrina','Mitty')
ORDER BY ANIMAL_ID;
```



#### LIKE

```mysql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog'
AND NAME LIKE '%el%'	# 대소문자 구분 X
ORDER BY NAME;
```



#### CASE

```mysql
SELECT  
    ANIMAL_ID, 
    NAME,
    CASE 
        WHEN SEX_UPON_INTAKE LIKE '%Neutered%'
        OR SEX_UPON_INTAKE LIKE '%Spayed%'
        THEN 'O'
        ELSE 'X'
    END AS '중성화'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



#### DATE_FORMAT

```mysql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d')
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```



<a href="#MySQL">Top</a>