# Chapter 6 | 데이터베이스

## 1) 데이터베이스의 큰 그림
- **데이터베이스 (Database)**: 원하는 기능을 동작시키기 위해 필요한 정보를 체계적으로 저장하는 시스템.
- **DBMS (Database Management System)**: 데이터베이스를 관리하는 소프트웨어로,  
  - **RDBMS** 예시: MySQL, Oracle, PostgreSQL, MariaDB, SQL Server  
  - **NoSQL** 예시: MongoDB, Redis
- **언제 사용하는가?**
  - DBMS는 응용 프로그램이 **쿼리(SQL)**를 통해 데이터 요청/응답을 할 수 있도록 서버처럼 동작.
- **SQL 언어 유형**:
  - DDL: `CREATE`, `ALTER`, `DROP`
  - DML: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  - DCL: `GRANT`, `REVOKE`
  - TCL: `COMMIT`, `ROLLBACK`
- **파일 대신 DB 사용 이유**:
  - 데이터의 **일관성** 및 **무결성** 보장  
  - 중복 감소, 연관 데이터 수정 편리  
  - 정교한 검색, 백업 및 복구 용이성
- **저장 단위 및 트랜잭션**:
  - **엔티티(Entity)** → **레코드(Record)** 형태 저장  
  - **스키마(Schema)**: RDBMS는 고정된 구조, NoSQL은 유연한 구조  
  - **트랜잭션(Transaction)**: ACID 속성 (원자성, 일관성, 격리성, 지속성) 요구

<br>

## 2) RDBMS의 기본
- **필드 타입(Field Type)**: 열에 저장되는 데이터의 유형 (예: `INT`, `VARCHAR`, `DATE`)
- **키(Key)**:
  - 후보 키 (유일 & 최소)
  - 기본 키 (Primary Key): 한 테이블에 하나, NULL 불가
  - 외래 키 (Foreign Key): 다른 테이블의 기본 키 참조
- **테이블 관계**:
  - 일대일 (1:1), 일대다 (1:N), 다대다 (N:M) — 다대다 관계는 **중간 테이블**로 구현
- **무결성 제약 조건**:
  - 도메인 제약 (타입/범위/원자성 준수)
  - 엔티티 무결성 (기본 키는 고유 & NULL 불가)
  - 참조 무결성 (외래 키는 원본 기본 키 값이거나 NULL)

<br>

## 3) SQL
- 데이터베이스와 상호작용하는 표준 언어
  - DDL: 테이블과 구조 정의 (`CREATE`, `ALTER`, `DROP`)
  - DML: 데이터 조작 (`SELECT`, `INSERT`, `UPDATE`, `DELETE`)
  - TCL: 트랜잭션 제어 (`COMMIT`, `ROLLBACK`, `SAVEPOINT`)
  - DCL: 접근 권한 관리 (`GRANT`, `REVOKE`)

<br>

## 4) 효율적 쿼리
- **서브쿼리(Subquery)**: 다른 쿼리 내부에 포함된 `SELECT`문  
- **조인(Join)**:
  - `INNER JOIN`: 공통된 행 결합
  - `OUTER JOIN (LEFT, RIGHT, FULL)`: 한쪽 전체 + 조건 불일치 시 NULL 채움
- **뷰(View)**: 복잡한 `SELECT`문을 가상 테이블로 단순화  
- **인덱스(Index)**: B-트리 구조 등의 형태로 검색 속도 향상을 위한 구조

<br>

## 5) 데이터베이스 설계
- **ER 다이어그램 (ERD)**: 엔티티와 관계를 시각적으로 설계하는 도구
- **정규화 (Normalization)**:
  - **제1정규형**: 모든 필드가 원자값  
  - **제2정규형**: 부분 함수 종속 제거  
  - **제3정규형**: 이행적 종속 제거  
  - **BCNF**: 모든 결정자는 후보 키여야 함

<br>

## 6) NoSQL
- **RDBMS vs NoSQL 특징 비교**:
  - RDBMS: 구조화된 스키마, ACID 보장, 정형화된 데이터  
  - NoSQL: 유연한 스키마, 수평 확장성, 높은 성능 및 가용성 강조
- **NoSQL 종류**:
  - 키-값 저장소 (Key-Value Store): 예 `Redis`
  - 도큐먼트 저장소 (Document DB): 예 `MongoDB`
  - 그래프 데이터베이스: 예 `Neo4j`
  - 칼럼 패밀리 저장소 (Column-family): 예 `Cassandra`

<br>

## 예상 질문

<details>
<summary>정규화(Normalization)란 무엇이며, 왜 필요한가요?</summary>
  
---

정규화는 데이터베이스의 중복을 줄이고 무결성을 유지하기 위해 테이블을 구조화하는 과정입니다. 

이를 통해 저장 공간을 절약하고, 데이터 일관성을 유지하며, 업데이트나 삭제 시 오류를 방지할 수 있습니다.

---

</details>

<details>
<summary>조인(Join)이 무엇인지와 그 종류에 대해 설명해주세요.</summary>
  
---

조인은 두 개 이상의 테이블을 조건에 따라 결합해 데이터를 조회하는 방법입니다. 적어도 하나의 컬럼을 공유하고 있어야 사용이 가능합니다.

- **INNER JOIN:** 조건에 맞는 양쪽 테이블의 데이터만 조회합니다.
- **LEFT/RIGHT OUTER JOIN:** 한쪽 테이블의 모든 데이터와 조건에 맞는 상대 테이블 데이터 조회합니다.
- **FULL OUTER JOIN:** 양쪽 테이블의 모든 데이터를 조회하며, 조건 불일치 시 NULL로 표시됩니다.



---

</details>

<details>
<summary>뷰(View)의 정의와 사용 목적은 무엇인가요?</summary>
  
---

뷰는 하나 이상의 테이블로부터 생성된 가상의 테이블입니다. 

복잡한 쿼리를 단순화하고, 특정 데이터만 노출해 보안을 강화하며, 재사용 가능한 쿼리를 제공할 때 활용됩니다.

---

</details>

<details>
<summary>트랜잭션의 격리수준에 대해 설명해주세요.</summary>
  
---

트랜잭션 격리수준은 **동시성 제어(Concurrency Control)** 에서 여러 트랜잭션이 동시에 수행될 때 트랜잭션 간 상호 간섭을 얼마나 제한할지를 정의한 수준입니다. 
즉, 한 트랜잭션이 다른 트랜잭션의 변경 데이터를 볼 수 있는지를 결정합니다.

[주요 격리 수준]
- **Read Uncommitted:** 커밋되지 않은 데이터도 읽을 수 있어 Dirty Read가 발생할 수 있으며, 락은 발생하지 않습니다.
- **Read Committed:** 커밋된 데이터만 읽으며 Nonrepeatable Read가 발생할 수 있고, 락은 발생하지 않습니다.
- **Repeatable Read:** 트랜잭션 내에서 조회 결과가 항상 동일하도록 보장하며, Phantom Read가 발생할 수 있고 락이 발생합니다.
- **Serializable:** 한 트랜잭션에서 사용되는 데이터는 다른 트랜잭션이 접근할 수 없으며, 가장 엄격한 수준으로 락이 발생합니다.

[참고]
- Dirty Read: 커밋되지 않은 데이터를 읽는 현상
- Nonrepeatable Read: 트랜잭션 내 동일한 쿼리 결과가 달라지는 현상
- Phantom Read: 트랜잭션 범위 내에서 새로 삽입된 레코드가 나타나는 현상
- 락(Lock): 데이터 일관성을 위해 트랜잭션이 데이터를 잠그는 방식

---

</details>
