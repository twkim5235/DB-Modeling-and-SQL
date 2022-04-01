# SQL

Structed Query Language

- 관계형 데이터베이스 관리 시스템(RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
- 관계형 데이터베이스 관리 시스템에서 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안



### SQL문장 종류

| 명령어 분류                                              | 명령어    | 설명                                                         |
| :------------------------------------------------------- | --------- | ------------------------------------------------------------ |
| DQL<br>Data Query Language<br>(질의어)                   | SELECT    | 데이터 검색 시 사용한다                                      |
| DML<br/>Data Manipulation Language<br/>(질의어)          | INSERT    | 데이터 입력 시 사용한다.                                     |
| //                                                       | UPDATE    | 데이터 수정 시 사용한다.                                     |
| //                                                       | DELETE    | 데이터 삭제 시 사용한다.                                     |
| DDL<br>Data Definition Language<br>(데이터 정의어)       | CREATE    | 데이터베이스 객체를 생성한다.                                |
| //                                                       | ALTER     | 데이터베이스 객체를 변경한다.                                |
| //                                                       | DROP      | 데이터베이스 객체를 삭제한다.                                |
| //                                                       | RENAME    | 데이터베이스 객체 이름을 변경한다.                           |
| TCL<br>Transaction Control Language<br>(트랜잭션 처리어) | TRUNCATE  | 데이터베이스 객체의 저장 공간을 삭제한다.                    |
| //                                                       | COMMIT    | 트랜잭션의 정상적인 종료를 처리한다.                         |
| //                                                       | ROLLBACK  | 트랜잭션을 취소한다. 트랜잭션을 실행되기 전 상태로 돌아간다. |
| DCL<br>Data Control Language<br>(데이터 제어어)          | SAVEPOINT | 트랜잭션 내 임시 저장점을 설정한다.                          |
| //                                                       | GRANT     | 데이터베이스에 대한 일련의 권한을 부여한다.                  |
| //                                                       | REVOKE    | 데이터베이스에 대한 일련의 권한을 취소한다.                  |



### SELECT 절

- SELECT 문에서 필수 구성 절. SELECT 다음에는 연산식이 온다.
- 열 이름에 사용할 수 있는 문자는 영문자, 숫자 및 $, #, _을 사용할 수 있다.
- 열 이름의 첫 글자는 영문 알파벳만 가능하다.
- 문자 상한의 최대 30자까지 가능하다.
- 기본값은 대문자로 표시된다. 문자 등으로 표시하려면 단일 행 함수를 사용하거나, `''` 로 둘러 싸는 등의 처리가 필요하다.
- 각종 DBMS의 예약어는 사용할 수 없는 경우가 있다.



#### ALL / DISTINCT

ALL - 테이블에 동일한 데이터 행이 있는 경우에도 모든 데이터를 반환한다. 지정하지 않으면 ALL이 선택된다.

DISTINCT (UNIQUE) - 테이블에 동일한 데이터 행이 있는 경우 중복을 제거한 1개만을 반환한다.



#### 컬럼 별칭

컬럼명 [AS] 컬럼 별칭 (AS는 생략가능)으로 컬럼을 다른이름으로 표시할 수 있다.

단, WHERE 절, GROUP BY 절, HAVING 절은 컬럼 별칭은 없다.



- SELECT 다음에는 계산식이 올 수 있음
- 여러 테이블에서 지정하면 결합이 이루어진 JOIN을 이용하는 것 외에 WHERE 절은 공통 열 결합 관계를 지정하는 것도 가능하다. (단, 이 경우 OUTER JOIN은 불가능하다)
- 이 FROM 절에서 테이블 별칭 지정이 가능하지만 일단 테이블 별칭을 지정하면 테이블 별명으로 묘사 해주지 않으면 에러가 발생한다.



#### SELECT 문법

~~~SQL
SELECT [ALL | DISTINCT] 컬럼명 [, 컬럼명...]
[INTO 테이블명]
FROM 테이블명 [, 테이블명...]
[WHERE 조건식]
[GROUP BY 컬럼명 [HAVING 조건식]]
[ORDER BY 컬럼명]
~~~



##### Case 문

~~~sql
select (
  case 기준 col
    when 값 then '결과1'
    when 값 then '결과2'
    else '결과3'
  end
	) as '출력 컬럼',
  col1,
  col2
from 테이블
where 조건
~~~





#### Select into 문법

- 테이블을 복사하는 문법이다.

다른 DB에서는 Select into를 사용하나, MySQL은 지원하지 않는다.



**다른 DB의 Select into 문법**

~~~sql
select *
into 복사하고 싶은 테이블
from 원본 테이블
where 조건식
~~~



**MySQL의 Select into 문법**

~~~sql
create table 복사 테이블 as(
	select * 
	from 원본 테이블
	where 조건식
)
~~~



**union**

컬럼의 데이터 형식이 똑같으면 여러개의 select 절을 union 으로 묶을 수 있다

ex)

```sql
select '남성 고객', count(*)
from Customer
where customer_sex = 0
union
select '여성 고객', count(*)
from Customer
where customer_sex = 1
union
select '미확인 고객', count(*)
from Customer
where customer_sex is null
```

### 집계 함수

- 집계함수는 값 집합에 대한 계산을 수행하고 단일 값을 변환한다.
- 집계함수는 SELECT 목록 또는 SELECT 문의 HAVING 절에 사용이 가능하다
- GROUP BY 절과 함께 행 범주에 대한 집계를 계산한다



**집계 함수 종류**

- AVG() = 평균
- SUM() = 총합
- COUNT() = ROW의 개수
- MIN() = 최소값
- MAX() = 최대값



### 순위 함수

- ROW_NUMBER, DENSE_RANK, RANK, NTILE

- ROW_NUMBER()

  - 1, 2, 3, 4 ... 번호를 부여한다

- SELECT ROW_NUMBER() OVER (PARTITION BY COL ORDER BY PRICE DESC) 별칭, COL1, COL2, ...

  FROM TABLE

MySQL은 8.0 이상부터 지원한다.

조건 없이 숫자 하나씩 매기기

```sql
select
       @rownum := @rownum + 1 as 숫자,
       customer_name,
       customer_address,
       customer_sex,
       customer_age
from Customer, (select @rownum := 0) as R;
```



순위 매기기(이것이 정확한건지는 잘 모르겠으나 의도한대로는 된다)

- 이름 순으로 순위를 매김

```sql
select
       @rownum := @rownum + 1 as 숫자,
       customer_name,
       customer_address,
       customer_sex,
       customer_age
from Customer, (select @rownum := 0) as R
order by customer_name;
```



- 성별로 각각의 그룹마다 번호 매기기

```sql
select case @grouping
           when customer_sex then @rownum := @rownum + 1
           else @rownum := 1
           end as 순위,
       customer_name,
       customer_address,
       @grouping := customer_sex as customer_sex,
       customer_age
from Customer,
     (select @grouping := '', @rownum := 0) as R
order by customer_sex, customer_name desc;
```

결과 값

| 순위 | customer_name | customer_address     | customer_sex | customer_age |
| ---- | ------------- | -------------------- | ------------ | ------------ |
| 1    | 김길산님      | 경기도               | 0            | 43           |
| 2    | 나길동님      | 인천시 연수구 땡땡동 | 0            | 24           |
| 3    | 박길산님      | 충청도               | 0            | 23           |
| 4    | 박길동님      | 인천시 연수구 땡땡동 | 0            | 25           |
| 1    | 김길동님      | 인천시 연수구 땡땡동 | 1            | 29           |
| 2    | 이길동님      | 인천시 연수구 땡땡동 | 1            | 23           |
| 3    | 김길동님      | 인천시 연수구 땡땡동 | 1            | 25           |
| 4    | 이길산님      | 경상도               | 1            | 32           |
| 5    | 이길동님      | 인천시 연수구 땡땡동 | 1            | 26           |
| 6    | 장길산님      | 서울시 마포구 신촌동 | 1            | 45           |
| 7    | 홍길동님      | 인천시 연수구 땡땡동 | 1            | 22           |



### 스칼라 함수

스칼라 함수란 단일 값을 반환하는 함수이다.

| 함수 범주 | 설명                              |
| --------- | --------------------------------- |
| 변환 함수 | 데이터 형식 캐스팅 및 변환을 지원 |

#### 1. CAST

- 문법
  - CAST(expression AS datatype(length))

- 파라미터
  - expression: 필수 항목, 변환될 값
  - datatype: 필수 항목, expression이 변환될 데이터 타입
  - Length: 선택항목, 결과 데이터 타입의 길이를 지정. 문자열에서 사용한다. 
- 사용 예시
  - SELECT CAST('25' as INT) + 3;
  - SELECT CAST('2017-08-25' as datetime);



#### 2. CONVERT

- 문법
  - CONVERT(expression[style], data_type[(length)])

- 파라미터
  - expression: 필수 항목, 변환될 값
  - datatype: 필수 항목, expression이 변환될 데이터 타입
  - Length: 선택 항목, 결과 데이터 타입의 길이를 지정. 문자열에 사용 
- 사용 예시
  - SELECT CONVERT(34, char);
  - SELECT CONVERT(price, NVARCHAR(10)) + '원' as 금액



이외 대표적인 스칼라 함수들(MSSQL 기준이나 궁금한것은 Mysql을 앞에다 붙이거 검색하면 됨)

![](./picture/스칼라_함수_목록.png)



### Join Update, Delete

**Join Update 문**

~~~SQL
update 변경할 테이블 별칭
         join 조인할 테이블 별칭 on 조인 별칭.컬럼 = 변경 별칭.컬럼
set 변경할 테이블의 컬럼 = 100000
where 조건
~~~



**Join Delete 문**

```sql
delete 삭제할 테이블 from 삭제할 테이블 별칭
         join 조인할 테이블 별칭 on 조인 별칭.컬럼 = 삭제 별칭.컬럼
[where 조건]
```



### 서브쿼리

**서브뤄리란 하나의 쿼리문 안에 포함되어 있는 또 하나의 쿼리문**

- 여러 번의 쿼리를 수행해야만 얻을 수 있는 결과를 하나의 중첩된 쿼리 문장으로 간편하게 결과를 얻을 수 있게 해준다.
- 서브쿼리는 괄호로 묶어서 사용한다
- 서브쿼리 안에서 order by 절을 사용할 수 없다.

**반환 값에 따른 서브쿼리**

- 단일 행 서브쿼리: 서브쿼리의 결과가 1행
- 다중 행 서브쿼리: 서브쿼리의 결과가 여러행
- 다중 컬럼 서브쿼리: 서브쿼리의 결과가 여러 컬럼

서브쿼리는 독립적으로 어떠한 테이블에서든 다 가져올 수 있다.



**SELECT 절 서브쿼리(스칼라 서브쿼리)**

```sql
select (select COUNT(*) from Customer where customer_sex = 1) 여성_고객,
       (select COUNT(*) from Customer where customer_sex = 0) 남성_고객,
       (select COUNT(*) from Customer where customer_sex is null) 미확인_고객,
       (select COUNT(*) from customer_purchase_car) 자동차_총_판매대수,
       (select SUM(purchase_price) from customer_purchase_car) 자동차_총_매출금액
```

**FROM 절 서브쿼리 (인라인 뷰)**

```sql
select * from
(
  select category, count(*) cnt
	from Customer
	group by category) a
where cnt = 1;
```

**WHERE절 서브쿼리**

도메인의 역할을 함 (영역을 제한 함)

```sql
select *
from Customer
where customer_id in (select customer_id from customer_purchase_car);
```



#### 상관 서브쿼리

- 내부의 쿼리에서 외부 쿼리테이블의 데이터를 참조하는 쿼리

  - 메인 쿼리의 테이블의 행마다 서브쿼리가 반복 실행 됨
  - 다른 행의 열끼리 비교하는 쿼리

  ```sql
  select *
  from Customer a
  where customer_id in (select customer_id from customer_purchase_car b where a.customer_id = b.customer_id);
  ```



### 트랜잭션

트랜잭션이란 데이터 베이스 상호작용 단위이다.

**트랜잭션의 성질**

- ACID
  - 원자성(Atomicity)
    - 트랜잭션의 작업이 부분적으로 실행되다가 중단되지 않는 것을 보장하는 능력이다
      - 만약에 중단 될시 이전 상태로 RollBack 된다
      - 제대로 작업이 진행 되면 마지막에 commit 된다.
    - All or Nothing
  - 일관성(Consistency)
    - 트랜잭션이 실행을 성공적으로 완료하면 언제나 일관성 있는 데이터베이스 상태로 유지하는 것을 의미한다.
  - 독립성(Isolation)
    - 트랜잭션을 수행 시 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다.
  - 지속성(Durability)
    - 성공적으로 수행된 트랜잭션은 영원히 반영되어야 함을 의미한다.



#### mysql Transaction 사용법

~~~sql
start transaction; //트랜잭션 시작

insert into customer_purchase_car (customer_id, car_id, purchase_date, purchase_price)
VALUES (9, 4, '20210206', (select price from Car where id = 4));

update Customer a
    join (select customer_id, COUNT(*) cnt
          from customer_purchase_car
          group by customer_id) cpc on a.customer_id = cpc.customer_id
set number_of_car = cnt
where a.customer_id = cpc.customer_id;

select a.customer_id, a.customer_name, a.number_of_car, car_id, purchase_date
from Customer a
         join customer_purchase_car cpc on a.customer_id = cpc.customer_id;

rollback; //rollback 전속

commit; //commit을 전송하여 영속화
~~~



































































































