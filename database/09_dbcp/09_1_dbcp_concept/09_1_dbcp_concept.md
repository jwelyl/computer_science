# Database Connection Pool (DBCP)

[24_06_10_daily_certification](https://www.notion.so/24_06_10_daily_certification-9694524834cd43f482a0878914d7c95d?pvs=21)

# DBCP

## DBCP(Database Connection Pool)

## 문제 제기

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled.png)

Front-End에서 API 요청이 오면 Back-End Server에서 API 요청을 받아 처리한다. 처리 중 Database에 접근해야 할 경우 DB Server에 Query 요청을 보내고 Query에 대한 응답을 받아서 API 요청을 마저 처리 후 API 요청에 대한 응답을 FE에 보낸다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%201.png)

실제 Back-End Server와 DB. Server는 다른 컴퓨터에 존재하는 경우가 대다수이기 때문에 둘 사이의 통신은 TCP 기반 네트워크 통신이다.

### **TCP 기반 통신**

**장점**

- 높은 송수신 신뢰성
- 데이터 송수신 시작 전 Open Connection (3-Way Handshake)
- 데이터 송수신 종료 후 Close Connection (4-Way Handshake)

**단점**

- Connection Open/Close의 시간적인 오버헤드가 작지 않음
- BE 관점에서 DB Server로 요청을 보내고 받을 때마다 매번 Connection 열고 닫으면 오버헤드가 매우 큼
- 서비스 성능이 떨어질 수 있음

## DBCP(Database Connection Pool)

TCP 기반 Connection을 DB에 접근할 때마다 open/close하는 단점을 보완

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%202.png)

미리 Back-End Server와 DB Server의 Connection을 여러 개 open해둔다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%203.png)

미리 연결된 Connection들을 Pool에 관리한다.

이렇게 미리 연결해둔 Connection을 하나의 Pool로 만들어서 관리한다.

**이 Pool을 Database Connection Pool (DBCP)라고 한다.**

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%204.png)

FE에서 API 요청을 받아 처리 중 DB Server에 접근해야 할 일이 발생한다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%205.png)

새로 TCP 3-Way Handshake로 Connection을 여는 것이 아니라, 기존에 open해둔 connection 중, 사용되지 않는 connection을 DBCP에서 얻어온다. **(Get Connection)**

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%206.png)

얻어온 connection을 통해 DB Server와 연결하여 쿼리 요청을 보내고 응답을 받는다. 응답을 받은 후 실제로 4-Way Handshake를 통해 connection을 종료하는 것이 아니라 connection을 DBCP에 반납한다. **(Close Connection)**

DB Server의 쿼리 응답으로 API의 요청을 처리하고 FE에 결과를 보내준다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%207.png)

API 요청마다 TCP Connection을 open/close할 필요가 없어서 시간이 절약된다.