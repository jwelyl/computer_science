# NoSQL

# NoSQL

## 1. NoSQL 등장 배경

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled.png)

2000년대 이후 인터넷 보급률이 매우 높아지고 SNS 사용자가 폭발적으로 늘어나면서 기존 RDBMS만으로는 커버할 수 없는 트래픽이 발생한다. **더 높은 처리량/더 짧은 응답 시간/비정형 데이터의 처리가** 요구된다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%201.png)

그래서 등장한 것이 NoSQL이다.

## 2. NoSQL

### Not-Only SQL

RDB가 커버하지 못하는 단점들도 커버하는 DBMS이다.

### 종류

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%202.png)

종류가 매우 많고 각각의 특색이 존재하며, SQL처럼 표준화가 잘 되어 있지는 않다.

따라서 사용하고자 하는 NoSQL의 특징을 자세히 확인해서 사용해야 한다.

그럼에도 RDB와 비교했을 때 NoSQL의 공통적인 특징이 있다.

## 3. NoSQL의 특징

mongoDB를 예시로 알아보자.

### 3-1. Flexible Schema

RDB에서는 Student 정보를 저장하기 위해 아래와 같은 테이블 schema를 정의해야 했다.

```sql
create table student (
	id INT PRIMARY KEY,
	name VARCHAR(20)
);
```

미리 schema에 정의된 컬럼 외 데이터를 저장하려면 schema를 수정해야 한다.

![1.png](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/1.png)

mongoDB에서는 유연하게 collection schema를 생성할 수 있다.

![2.png](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/2.png)

![3.png](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/3.png)

데이터의 저장도 원하는 데이터를 Key : Value 형태로 저장 가능하다. primitive type만 아니라 JSON, Array 값도 저장 가능하다.

![4.png](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/4.png)

데이터 조회의 경우 찾으려는 속성의 값을 조건으로 찾을 수 있다. 이렇게 찾아진 데이터를 Document라고 한다.

기타 특징은 mongoDB 공식 문서를 찾아보자.

**RDB에서는 schema를 DB Server에서 관리해줬다면 NoSQL에서는 application level에서 schema를 관리해야 한다. (개발자의 부담)**

### 3-2. 중복 허용 (JOIN 회피)

RDB에서는 테이블을 분리해서 데이터의 중복 저장을 최소화한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%203.png)

NoSQL에서는 중복을 허용하여 JOIN을 회피한다. JOIN을 회피해서 검색 성능을 높인다.

**하지만 application level에서 중복된 데이터들이 일관성 있게 최신 데이터를 유지할 수 있도록 관리해야 한다.**

### 3-3. Scale-out에 최적화되어 있다.

NoSQL DB Servers는 RDBMS Server보다 증설이 쉽다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%204.png)

서버 여러 대로 하나의 클러스터를 구성해서 사용한다.

각 서버 별로 데이터를 나눠서 중복을 허용하여 저장한다. JOIN이 필요 없으므로 collections을 분산해서 저장하면 된다.

RDB의 경우 서버 별로 테이블을 나누어 저장하면 JOIN을 위한 테이블이 여러 서버에 분산되어 Network Traffic까지 발생하여 성능이 더 떨어진다.

### 3-4. High-Throughput

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%205.png)

**ACID의 일부를 포기하고 High-Throughput, Low-Latency를 추구한다.**

금융 시스템처럼 Consistency가 중요한 환경에서는 매우 조심해서 사용해야 한다.

ACID를 얼마나 보장하고 포기하는지는 NoSQL마다 다르다.

## 4. Redis

### 4-1. Redis의 특징

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%206.png)

Redis에 데이터 저장하고 조회하기

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%207.png)

- 메모리에 Key-Value 형태로 데이터를 저장하는 NoSQL DB (in-memory DB)
- 데이터베이스로도 사용되고, 캐시로도 사용된다.
- 여러 데이터 타입을 저장할 수 있다.
- Hash 기반 sharding된 cluster를 구성할 수 있다.
- High Avaliability(고가용성) : Replication, Automatic Failover
- 메모리의 응답성이 SSD보다 빠르므로 cache로 사용된다.

### 4-2. Redis를 cache로 사용하기

**YouTube 예시**

**RDB만 사용하는 경우**

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%208.png)

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%209.png)

요청이 많아질 경우, 성능이 떨어지고, 응답이 느려진다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2010.png)

Replication, Secondary Server를 추가할 수도 있지만 Redis Cache를 사용할 수 있다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2011.png)

조회하려는 데이터가 Redis 캐시에 존재하는지 우선 확인한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2012.png)

조회하려는 데이터가 Redis 캐시에 존재하지 않을 경우 RDB에서 조회한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2013.png)

RDB에서 가져온 정보를 BE Server에서 Redis 캐시에 저장한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2014.png)

Redis에는 Key = Primary Key, Value = 영상 관련 데이터 를 저장한다. 동시에 timeout을 같이 저장하여 timeout 동안에만 Redis 캐시에 존재한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2015.png)

BE Server에서 가공한 정보를 FE에 전달한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2016.png)

같은 요청이 다시 오면 RDB에서 찾을 필요 없이 Redis 캐시에 저장된 정보를 빠르게 가져올 수 있다.

Redis는 Memory Cache이므로 SSD, HDD를 사용하는 DB에 비해 매우 빠르다.

[Redis - The Real-time Data Platform](https://redis.io/)

[NoSQL Databases List by Hosting Data - Updated 2024](https://hostingdata.co.uk/nosql-database/)