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