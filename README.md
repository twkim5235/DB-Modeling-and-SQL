# DB Modeling & SQL

## 1. 관계형 데이터베이스

### 데이터 베이스

- 구조화된 데이터들의 집합

### 관계형 데이터베이스

- 데이터들을 2차원 배열과 같은 테이블에 저장하고 관리

### 관계 정의

- 1:M 관계(부자지간 관계)
- M:N 관계(비즈니스 관계)
- 1:1 관계 (부부 관계)



### 관계형 데이터베이스 특징

#### 고유 식별자

- 테이블은 각 행(레코드)를 식별하기 위하여 고유 식별자를 정의할 수 있음
- 고유 식별자는 NOT NULL, UNIQUE 속성을 갖음
- 고유 식별자는 하나 또는 여러 개의 컬럼들로 정의 할 수 있음

#### 참조 무결성

- 테이블에서 외래 키를 선언
- 외래 키는 다른 테이블에 정의된 고유 식별자를 참조
- 외래 키의 값은 다른테이블에 정의된 고유 식별자의 값의 범위를 넘을 수 없도록 제한 됨.



### 테이블 구조

#### 테이블 (Table, relation, entity)

- 컬럼 속성들과, 여러 개로 구성된 레코드들의 집합
- 테이블 명으로 구분
- 스키마 객체의 하나로 관계형 데이터베이스를 구성하는 기본 데이터 구조
- 테이블을 대상으로 데이터를 입력, 수정, 삭제, 조회

#### Column (attribute, 속성, property)

- 테이블의 속성들의 집합

#### Row (tuple, record)

- 하나의 속성들의 집합을 모아놓은 행
- Record(레코드)는 Row와 동의어



## 2. Key

### Key의 정의

- 하나의 테이블에서 각 레코드를 고유하게 실별할 수 있는 컬럼 또는 컬럼의 조합
- Key의 조건은 NOT NULL, UNIQUE
- 테이블 디자인 시 Key를 정하고, 테이블을 데이터베이스에 만들 때 명시적으로 Key를 선언 함
- Key는 Key에 대응하는 인덱스 테이블이 생성 됨
  - 인덱스 테이블은 키값에 의해서 정렬되어 있음

### Candidate Identifier (후보 키)

- 주 식별자가 될 가능서이 있는 식별자
- 모든 식별자는 주식별자가 될 수 있는 후보이므로, 식별자와 후보 식별자는 사실상 동일어 이다.
- 결정자(Determinant): 결정자 값을 알면 결정자가 속해있는 행의 나머지 속성(또는 Column) 값도 알 수 있다.



### Prinary Key (PK - 주 식별자)

- 테이블 컬럼에서 각 레코드를 유일하게 식별할 수 있는 컬럼 또는 컬럼들의 집합
- 후보 키들 중에 대표 키로 선정된 식별자
  - 최소한의 속성 조합이 주 식별자가 되도록 해야 한다.
  - 테이블 내의 각 레코드가 정확하게 식별되도록 보장한다.
  - 다양한 종류의 무결성을 설정하고 강화하는 것을 도와준다.
  - 테이블 관계를 설정하도록 해준다.



## 3. Data Type

| 데이터 타입             | 범위                                                         | 저장소 크기          |
| ----------------------- | ------------------------------------------------------------ | -------------------- |
| Bit                     | 0 또는 1                                                     | 1bit                 |
| Int                     | –2,147,483,648 ~ 2,147,483,647                               | 4byte                |
| SmallInt                | -32,768 ~ 32,767                                             | 2byte                |
| TinyInt                 | 0 ~ 255                                                      | 1byte                |
| Bigint                  | -2^63 ~ 2^63 -1 약 920경                                     | 8byte                |
| Float                   | 3.4E-38(-3.4*10^38) ~ 3.4E+38(3.4*10^38) (7digits)           | 4byte                |
| Real(decimal - numeric) | 1.79E-308(-1.79*10^308) ~ 1.79E+308(1.79*10^308) (15digits)  | 8byte                |
| Char[n]                 | n = 1 ~ 8000                                                 | n바이트              |
| varChar[n]              | n = 1 ~ 8000 <br/>varchar[(n\|max)] <br/>max는 최대 저장소 크기가 2 ^ 31 -1 바이트임 | 입력한 데이트의 길이 |
| Text                    | 최대 2,147,483,647자의 가변길이<br/>키에 참여할 수 없음      |                      |
| datetime                | 1753/1/1 ~ 9999/12/31                                        | 8바이트              |
| smalldatetime           | 1900/1/1 ~ 2079/6/6                                          | 4바이트              |

## 4. Primary Key 설계

### 고려사항

- 유일하고, 모든 레코드에 NOT NULL일 수 있는 컬럼을 찾는다.
- 후보 식별자가 없는 경우 임의의 식별자를 만들어 부여한다(인조 식별자)
  - ex - Id Column을 만들어서, Auto increment나, Sequence를 통해 레코드가 추가될 때 마다 자동 증가 시킨다.
- PK의 데이터 타입 결정
  - 레코드의 발생 가능한 최대 수를 예측한다.
    - 예) 1년에 몇 개 정도 발생하는가? 한달에 몇 개정도 발생하는가?
    - 
- 발생 가능한 최대 레코드 수를 커버할 수 있는 데이터 타입을 선정한다.
  - 만일 대상 레코드가 수십만개 정도라면 999,999로 커버할 수 있다.
    - 따라서 32bit(= 4byte) int (2,147,483,647)를 사용할 수 있다.
    - 또는 varchar(6)을 사용해서 '999999'까지 처리할 수 있다.
- PK의 데이터 타입 후보를 대상으로 다음을 고려한다.
  - int등 숫자를 PK로 채택할 경우 자동 증분 속성을 사용할 수 있다.(편리함) -  Auto increment, Sequence
  - String을 사용하면 숫자가 아닌 문자를 섞어서 PK값에 의미를 부여할 수 있다.
  - 특별한 의미를 부여할 필요가 없을 경우 정수형을 사용하는 것이 바람직하다.
- PK는 고유 식별자 기능으로 충분하다.
  - PK값에 어떤 의미를 부여하는 것은 부담이 된다.

