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



### 집계함수

- 집계함수는 값 집합에 대한 계산을 수행하고 단일 값을 변환한다.
- 집계함수는 SELECT 목록 또는 SELECT 문의 HAVING 절에 사용이 가능하다
- GROUP BY 절과 함께 행 범주에 대한 집계를 계산한다



**집계 함수 종류**

- AVG() = 평균
- SUM() = 총합
- COUNT() = ROW의 개수
- MIN() = 최소값
- MAX() = 최대값







































