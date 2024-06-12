# Database 개념

[24_03_19_daily_certification](https://www.notion.so/24_03_19_daily_certification-940bb96a6a324c1b895ea83b61b8162b?pvs=21)

## 데이터베이스

**전자적으로 저장하고 사용하는 관련 있는(related) 데이터(data)의, 조직화된 집합(organized collection)**

## Database Management System (DBMS)

사용자에게 데이터베이스를 정의하고 만들고 관리하는 기능을 제공하는 소프트웨어 시스템

ex) PostgreSQL, MySQL, ORACLE DATABASE, SQL Server

- 부가적인 데이터(metadata) 발생, 데이터베이스를 정의하거나 기술함(catalog)
    - 데이터 유형, 구조, 제약조건, 보안, 저장, 인덱스, 사용자 그룹 등등
    - metadata도 DBMS에 의해 저장되고 관리됨

## Database System (Database)

Database + DBMS + Application

![Simplified-database-system-Risunok-1-Uprosennaa-sistema-baz-dannyh-Slika.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/Simplified-database-system-Risunok-1-Uprosennaa-sistema-baz-dannyh-Slika.png)

## Data Models

DB의 구조를 기술하는데 사용될 수 있는 개념들이 모인 집합

DB 구조를 **추상화해서 표현**할 수 있는 수단을 제공한다.

- DB 구조 : 데이터 유형, 관계(relationship), 제약 사항(constraints) 등등

### **Conceptual Data Models**

일반 사용자들이 쉽게 이해할 수 있는 개념들로 이루어진 모델

추상화 수준이 가장 높음

비즈니스 요구 사항을 추상화하여 기술할 때 사용

- ER diagram
    
    ![ER-Model.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/ER-Model.png)
    

### **Logical Data Models**

데이터가 컴퓨터에 저장될 때의 구조와 크게 다르지 않게 DB 구조화가 가능함

특정 DBMS나 storage에 종속되지 않는 수준에서 DB를 구조화

- **Relational Data Model**
    
    ORACLE, MySQL, SQL Server
    
    ![091318_0803_RelationalD1.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/091318_0803_RelationalD1.png)
    
- Object Data Model
    
    ![objectDataModel.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/objectDataModel.png)
    
- Object-Relational Data Model
    
    PostgreSQL
    
    ![1280px-Object-Oriented_Model.svg.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/1280px-Object-Oriented_Model.svg.png)
    

### **Physical Data Models**

컴퓨터에 데이터가 어떻게 파일 형태로 저장되는지를 기술할 수 있는 수단 제공

Data Format, Data Ordering, Access Path 등등

Access Path : 데이터 검색을 빠르게 하기 위한 구조체 ex) index

## Database Schema

Data Model을 기반으로 Database Structure를 기술한 것

Schema는 DB를 설계할 때 정해지며 한 번 저장하면 자주 바뀌지 않음

## Database State

DB의 실제 데이터는 꽤 자주 바뀜

- 특정 시점에 DB에 있는 데이터를 Database State 또는 Snapshot이라고 한다.
- DB에 있는 현재 instance의 집합이다.

![scheme.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/scheme.png)

## Three-Schema Architecture

Database System을 구축하는 Architecture 중 하나이자 대표격

**User Application으로부터 Physical Database를 분리시키는 목적**

- Physical DB 구조가 변경되더라도 User Application에는 영향을 주지 않기 위해서

**세 가지 Level이 존재하며 각 Level마다 Schema가 정의되어 있음.**

**어느 레벨에서의 변화가 상위 레벨에 영향을 주지 않기 위해서 사용한다.**

![dbms-three-schema-architecture.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_03_19_daily_certification%20940bb96a6a324c1b895ea83b61b8162b/dbms-three-schema-architecture.png)

### Three Level

- **External(View) Level - External Schemas (User Views)**
    - 특정 유저들이 필요로 하는 데이터만 표현한다.
        - 유저마다 필요로 하는 데이터만 보여주고 그 외에는 숨김
        - Logical Data Model을 통해 표현
- **Conceptual Level - Conceptual Schemas**
    - 전체 DB 구조 기술
    - 물리적인 저장 구조 내용은 숨김
    - Entity, Data Types, Relationships, User Operations, Constraints
    - Logical Data Model을 통해 표현
- **Internal Level - Internal Schemas**
    - 물리적 저장 장치에 가장 가까움
    - 물리적으로 데이터가 어떻게 저장되는지 Physical Data Model을 통해 표현
        - Data Storage
        - Data Structure
        - Access Path
    - 실제 데이터가 존재하는 곳

## Definition Language

### Data Definition Language (DDL)

**Conceptual Schemas를 정의하기 위해 사용하는 언어**

Internal Schemas까지 정의할 수 있는 경우도 간혹 존재 (보통 Parameter로 정의)

### Storage Definition Language (SDL)

Internal Schemas를 정의하는 용도로 사용하는 언어 

하지만 보통 RDBMS에는 Paramter 등의 설정으로 대체하여 거의 사용되지 않음

### View Definition Language (VDL)

External Schemas를 정의하기 위해 사용되는 언어

대부분 DBMS에서는 DDL이 VDL 역할까지 수행

## Data Manipulation Language (DML)

DB에 있는 데이터를 활용하기 위한 언어

데이터 추가, 삭제, 수정, 검색 등등의 기능을 제공하는 언어

## SQL

Relational Database Language에서 DDL, VDL, DML을 통합한 언어