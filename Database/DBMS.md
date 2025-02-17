# DBMS

### 개념
데이터베이스 관리 시스템
다수의 사용자들이 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어 도구의 집합
- 데이터베이스 언어라고 부르는 특별한 프로그래밍 언어를 한 개 이상 제공
- SQL(Structure Query Language) : 여러 DBMS에서 사용할 수 있는 표준 데이터베이스 언어

### 기능
- 정의 : 데이터에 대한 형식, 구조, 제약조건들 명세 (데이터베이스에 대한 정의 및 설명 : 카탈로그나 사전의 형태로 저장)
- 구축 : DBMS가 관리하는 기억 장치에 데이터 저장
- 조작 : 특정한 데이터를 검색하기 위한 질의, 데이터베이스의 갱신, 보고서 생성 기능 등
- 공유 : 여러 사용자와 프로그램이 데이터베이스에 동시에 접근 가능
- 보호 : 하드웨어나 소프트웨어의 오동작 또는 권한이 없는 악의적인 접근으로부터 시스템 보호
- 유지보수 : 시간이 지남에 따라 변화하는 요구사항 반영 가능

### 유형
- 중앙집중식 시스템 : 일반적인 방식. 모든 데이터가 단일 위치에 보관되며 사용자는 이 위치에 액세스하여 데이터 조작 가능
  - 예시 : IBM 메인프레임 DBMS, 초기 은행 시스템 (중앙서버에서 모든 거래 관리), 대학 행정 시스템 등
- 분산형 시스템 : 데이터가 여러 노드에 보관. 네트워크로 연결된 여러 사이트에 데이터베이스 자체가 분산되어 있으며, 데이터베이스 시스템도 여러 컴퓨터 시스템에서 운영됨.
  - 예시 : Amazon DynamoDB (분산 저장, 높은 가용성 제공), 은행의 지점별 DB 시스템, 온라인 쇼핑몰 글로벌 서버 등
- 클라이언트-서버 데이터베이스 시스템 : PC 또는 워크스테이션처럼 자체 컴퓨팅 능력을 가진 클라이언트를 통해 데이터베이스 서버 접근. 데이터베이스가 하나의 데이터베이스 서버에 저장되어있음. 데이터베이스 시스템의 기능이 서버와 클라이언트에 분산됨
  - 서버 : 데이터베이스를 저장하고 DBMS 운영. 여러 클라이언트에서 온 질의를 최적화하고, 권한 검사 수행, 동시성 제어와 회복 기능 수행, 데이터베이스의 무결성 유지, 데이터베이스 접근 관리
  - 클라이언트 : 사용자 인터페이스 관리 및 응용 수행
  - 2-tier model : 클라이언트와 데이터베이스 서버 직접 연결
  - 3-tier model : 클라이언트와 데이터베이스 서버 사이에 응용 서버 (비즈니스 로직) 추가
  - 예시 : MySQL + 웹 어플리케이션, Oracle DB + ERP 시스템 등

### 종류 및 트렌드
<img width="1053" alt="image" src="https://github.com/user-attachments/assets/db4f4182-ba92-49e4-9c42-65e8187731ba" />

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

Reference

- https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EA%B4%80%EB%A6%AC_%EC%8B%9C%EC%8A%A4%ED%85%9C
- https://www.nutanix.com/kr/info/database-management
- https://movefast.tistory.com/84
- https://db-engines.com/en/ranking_trend
