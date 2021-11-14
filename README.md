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

## 5. 1:M 관계

- 1:M 관계는 한쪽이 관계를 맺은 쪽의 여러 객체를 갖는 것을 의미하며, 가장 흔하게 나타나는 매우 일반적인 형태이다.
  - ex) 부모 자식 관계, 학년 반 관계, 컴퓨터 디렉토리 구조, Tree 구조같은 것 등
  - 부모는 여러개의 자식을 가질 수있다.
  - 자식은 부모와 달리 여러개의 부모를 가질 수 없다.
- 테이블은 서로 선천적으로 관계를 가지고 있다.
  - 자식은 부모에 종속되어 있다.
  - 관계를 나타날때는 이웃하는 2개의 테이블만을 관계로 나타낸다.
    - a - b - c : a와 b는 관계로 볼 수 있으나, a와 c는 관계로 볼 수 없다.

- 자식 테이블에서 부모의 PK를 가르킬 때 외래키라 한다.
  - 외래키는 Table 생성시 정의를 해줘야 한다.

- DB는 부자지간의 관계를 명시적으로 선언해주면 부모 없는 자식레코드 추가를 막아준다.
  - 즉 자녀 테이블에서 레코드를 추가할 때 자식 테이블의 외래키값이 부모테이블의 PK에 존재하지 않을 때, 레코드 추가를 DB에서 막아준다

- 부모가 없는 데이터가 있을 시, 가비지 데이터 이므로 무조건 안생기게 막아야 한다.
  - 그러니 부모가 있는 자식 데이터를 만들어야 한다.
  - 자식 이 있는 부모 테이블은 delete가 안되게 설계하고, 부모 없는 자식 데이터는 insert가 안되게 설계하여야 한다.

### 1: M 재귀적 관계

- 재귀적인 관계란 계속 해서 1:M 관계가 맺어지는것을 뜻한다.
- 회사 - 부서 - 세부 부서 - 세부 세부 부서와 같이 계속해서 나눠 지는것을 재귀적 관계라고 한다.
- ex) 회사 부서, 분류 코드, 컴퓨터 directory

| 부서 ID(PK) | 부서 이름 | 상위 부서 ID(FK) - 부서 ID를 참조함 |
| ----------- | --------- | ----------------------------------- |
| 1           | 총무과    | null                                |
| 2           | 총무1팀   | 1                                   |
| 3           | 총무2팀   | 1                                   |
- 설명: 총무 과는 가장 상단의 Column이며, 총무 1팀과 총무 2팀이 총무과의 자식 컬럼이 된다. 왜냐하면 총무 1팀과 총무 2팀의 FK가 1이기 때문이다.
- 위 표와 같이 외래 키가 자신의 PK를 참조하면 재귀적 관계가 맺어진다.

## 6. N:M 관계

- N:M 관계는 관계를 가진 양쪽 당사자 모두에서 1:M 관계가 존재할 때 나타나는 모습이다.
  -  N쪽에서 M을 봐도 1:M 이고 M쪽에서 N을 봐도 1:M 이다.
- ex) 학생과 과목 관계
- N:M 관계는 선천적으로는 테이블과 테이블의 관계가 없다. 각테이블은 스스로 존재하고 있다. 그런데 이들 사이에 어떤 관계를 맺어 줌으로써 관계가 형성된다.

![image-20211028210736219](/Users/taewoo/Library/Application Support/typora-user-images/image-20211028210736219.png)

- 스스로 존재하는 테이블을 마스터 테이블이라 한다.

- 테이블(A, B)이 두개가 있을때 제일먼저 마스터 테이블인지 관계테이블인지 확인하여야한다.

  - 마스터 테이블을 찾기 쉬운 예시 테이블 이름 뒤에 하다를 붙여봤을 때 어색하면 마스터 테이블이다.
    - 학생 하다(마스터), 과목 하다(마스터), 수강하다(관계)

- 테이블 두개가 선천적인 1: M 관계가 있는지 확인하여야 한다.

- 두개의 관계를 확인한 뒤, 어떠한 관계가 없으면 N:M 관계가 된다. 그러나 두개의 테이블이 관계가 맺어질 때가 있는데, 그때를 비즈니스가 생길때라고 하겠다, 비즈니스가 생기면 관계가 형성되는데 이 때, 비즈니스를 설명하는 관계 테이블이 만들어진다. 

  Ex) 학생(N) - 수강신청(관계) - 과목(M), 사람A - 차용(관계) - 사람 B, 고객(N) - 구매(관계) - 상품(M)

  그러므로, 관계 테이블을 찾기 위해서는 두테이블간의 동사를 찾아야 한다.

- 고객이 상품을 구매한다와 같은 관계는 고객이 같은 상품을 여러번 구매가 가능하기 때문에 중복이 가능하나, 학생이 과목을 신청하다와 같은 관계는 같은 시간에 같은 과목을 못들으니 중복이 불가능하다.

- 하나의 테이블은 하나의 객체만 모델링하는거다. 절대 하나의 테이블에 두개 이상의 객체를 모델링하면 안된다.

- Fk(PK이면서 FK인 FK)가 너무 많으면 조회를 할 때, 너무 많은 조건들이 들어가서 후보키(대체키)를 만들어서 효율을 극대화 한다. 후보키는 Not Null & Unique 여야 됨.

- | 후보키 | FK1  | FK2  | FK3  | FK4  |
  | ------ | ---- | ---- | ---- | ---- |
  | 1      | 1    | A    | 가   | a    |
  | 2      | 2    | B    | 나   | b    |
  | 3      | 3    | C    | 다   | c    |

### MySQL procedure 생성 및 호출 방법
~~~mysql
//생성
CREATE PROCEDURE 프로시저 이름(ex: SP_Insert_SchoolClass)(
    필드 이름 필드 타입,
    필드 이름 필드 타입,
    ....
)
BEGIN(ex insert)
	insert into 테이블 이름(필드, 필드, ...)
  values (프로시저 필드, 프로시저 필드, ...);
END

//호출
CALL 프로시저 이름(필드, 필드, ...);
~~~

## 7. 1:1 관계

- 1:1 관계란 어느 쪽 당사자의 입장에서 상대를 보더라도 반드시 단 하나의 관계를 가지는 것을 말한다.
  - ex) 부부 관계

- 개념상 하나로 합쳐도 전혀 문제가 없다.

- 1 Table의 PK 와 2 Table의 PK를 서로가 참조하기 때문에 두개의 값은 무조건 같아야 되며, null이면 안된다. 왜나햐면 둘다 마스터 테이블이기 때문에 하나라도 데이터가 없는데 생성하려고 하면 부모없는 자식이 될 수 있기 때문이다.

- 1 Table 과 2 Table 중 둘중에 하나의 레코드를 삭제하려 하면 그 하나의 레코드는 절대 삭제가 안된다 왜냐하면 둘중에 하나라도 삭제하면 부모없는 데이터가 생기기 때문에 DB자체에서 허용을 안해준다.

- 서류철과 문서(서류철 안에 들어가는 문서)를 정리하는 Table과 같이 서류철이라는 마스터를 공통 문서 양식이 참조하고, 또 세부 내용에 맞는 테이블을 만들어서 관계를 맺어준다. 이때 공통 양식과 각각 세부내용의 형식이 다를 수 있기 때문에 1대1 방식으로 매핑된다.
  - 공통 양식에서 어떤 세부문서인지 구분이 안가기 때문에, 세부 문서 테이블을 확인할 수 있는 필드(= 테이블 이름)를 추가한다.

## 8. Anomaly (데이터 이상현상)

### 데이터 모델링에서 제일 중요한것은 무결성을 보장하는 것

### Anomaly

- 데이터의 이상 현상
- 중복때문에 anomaly가 발생(의도하지 않은 이상 현상 발생 가능)
- Update, Delete, Insert에서 발생할 수 있음

## 8. Anomaly (데이터 이상현상)

### 데이터 모델링에서 제일 중요한것은 무결성을 보장하는 것

### Anomaly

- 데이터의 이상 현상
- 중복때문에 anomaly가 발생(의도하지 않은 이상 현상 발생 가능)
- Update, Delete, Insert에서 발생할 수 있음



## 9.정규화

### 1 정규화

#### 정의

- 데이터 중복을 제거하기 위한 테이블 분할

### 2 정규화

#### 정의

- 두개 이상으로 구성된 PK에서 발생한다. 식별자 일부에 종속되는 어트리뷰트는 제거해야 한다.

  | 주문번호(PK) | 상품코드(PK) | 상품명 | 개수   |
  | ------------ | ------------ | ------ | ------ |
  | 1            | 01           | 배     | 1박스  |
  | 1            | 02           | 사과   | 10박스 |
  | 2            | 01           | 배     | 1박스  |
  | 2            | 03           | 두부   | 2모    |

- 즉 예를 들면 상품명은 상품코드에만 종속되고, 주문번호에는 종속되지 않기때문에 해당 컬럼들은 따로 테이블로 빼준다.

  | 상품코드 | 상품명 |
  | -------- | ------ |
  | 01       | 배     |
  | 02       | 사과   |
  | 03       | 두부   |

### 3 정규화

#### 정의

- 식별자 이외의 속성간에 종속 관계가 존재하면 안된다.
- 종속 관계가 있으면 중복 값이 생긴다
- 이행 종속 관계를 분해하는 것
