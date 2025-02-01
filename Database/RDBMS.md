# RDBMS (관계형 데이터베이스 관리 시스템)

### 개념
<b> 관계 </b>
- 테이블 간의 상호작용을 기반으로 설정되는 여러 테이블 간의 논리적 연결
  
<b> 관계형 데이터베이스 (RDB) </b>
- 데이터가 열과 행의 테이블(또는 '관계') 하나 이상에 저장되는 사전 정의된 관계로 데이터를 구성하는 정보 모음

<b> 관계형 데이터베이스 관리 시스템 (RDBMS) </b>
- 데이터베이스 관리 시스템의 일종으로, 데이터를 표(테이블) 형태로 저장하고 관리하는 시스템

### 특징
- 데이터 구조 : 데이터를 테이블 형태로 저장, 테이블 간의 관계 정의
- SQL 지원 : SQL(Structured Query Language) 사용하여 데이터를 쿼리, 삽입, 삭제, 업데이트 등 작업 수행
- 데이터 무결성: 제약 조건(constraints)을 사용하여 데이터의 무결성 유지
- 동시성 제어: 여러 사용자가 동시에 데이터베이스에 접근하여 작업할 때, 데이터 충돌이나 불일치가 발생하지 않도록 관리
- 트랜잭션 관리: 하나의 작업 단위를 트랜잭션으로 묶어 처리하며, 트랜잭션의 원자성(atomicity), 일관성(consistency), 독립성(isolation), 지속성(durability) 보장하는 ACID 속성 지원
- 보안: 사용자 권한 관리와 같은 보안 기능을 제공하여 데이터에 대한 접근 제어

### 장점
- 유연성 : 전체 데이터베이스 구조를 변경하거나 기존 애플리케이션에 영향을 주지 않고 필요할 때마다 간편하게 테이블, 관계를 추가, 업데이트 또는 삭제하고 데이터 변경 가능
- ACID 규정 준수 : 오류, 실패 또는 기타 잠재적 오작동에 관계없이 데이터 유효성 보장
- 사용 편의성 : 기술자가 아닌 사용자도 데이터베이스와 상호작용하는 방법을 배울 수 있는 SQL을 사용하여 복잡한 쿼리를 쉽게 실행 가능
- 공동작업 : 여러 사용자가 동시에 데이터를 운영하고 액세스 가능. 기본 제공되는 잠금 기능으로 업데이트 중에는 동시에 데이터에 액세스할 수 없음 (동시성 제어 특징)
- 기본 제공 보안 기능 : 역할 기반 보안을 통해 데이터 액세스가 특정 사용자로 제한 (role 등록)

### 종류
- MySQL, PostgreSQL, MariaDB, Microsoft SQL Server, Oracle Database
  
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

Reference

- https://cloud.google.com/learn/what-is-a-relational-database?hl=ko
- https://aitrearc.com/%EA%B4%80%EA%B3%84%ED%98%95-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EA%B4%80%EB%A6%AC-%EC%8B%9C%EC%8A%A4%ED%85%9C-rdbms-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%A2%85%EB%A5%98/
- https://www.oracle.com/kr/database/what-is-a-relational-database/
