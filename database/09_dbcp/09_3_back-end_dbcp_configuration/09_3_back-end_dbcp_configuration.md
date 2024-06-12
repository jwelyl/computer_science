# Back-End DBCP Configuration

[24_06_10_daily_certification](https://www.notion.so/24_06_10_daily_certification-9694524834cd43f482a0878914d7c95d?pvs=21)

## Back-End DBCP Configuration

### HikariCP Configuration

**minimumIdle vs maximumPoolSize vs maxLifetime vs** 

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled.png)

**minimumIdle**

pool에서 아무 일을 하지 않더라도 유지하고 있는 최소한의 Idle Connection의 수

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%201.png)

**maximumPoolSize**

pool이 가질 수 있는 최대 connection 수

idle(inactive) connection 수 + active(in-use) connection 수

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%202.png)

**minimumIdle**

pool에서 아무 일을 하지 않더라도 유지하고 있는 최소한의 Idle Connection의 수

**DBCP의 Idle Connection 수가 minimumIdle보다 적고, 전체 Connection 수가 maximumPoolSize보다 적다면 신속하게 추가로 connection을 만든다.**

ex) minimumIdle = 2, maximumPoolSize = 4

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%203.png)

초기 상태는 minimumIdle 개수만큼 Idle Connection이 존재

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%204.png)

BE Server에 하나의 요청이 들어와서 idle connection 1개가 사용됨(active connection)

Idle connection 수는 1개로 minimumIdle보다 적고, 전체 connection 수도 2개로 maximumConnection 수보다 적음

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%205.png)

따라서 새로운 connection을 하나 생성한다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%206.png)

트래픽이 계속 와서 idle connection이 minumumIdle보다 적지만, 전체 connection이 maximumPoolSize만큼 존재하면 더 이상 idle connection은 생성할 수 없다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%207.png)

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%208.png)

트래픽이 더 이상 존재하지 않으면 모든 connection이 idle connection이 되고, minimumIdle개만 남기고 모두 close한다.

**HikariCP의 권장 사항은 minumumIdle을 maximumPoolSize로 설정하는 것이다.**

즉 항상 maximumPoolSize개의 connection을 유지한다. 트래픽이 몰려올 때마다 connection을 새로 추가할 필요가 없으므로 connection 생성 시간을 단축할 수 있다.

**maxLifetime**

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%209.png)

DBCP의 idle connection은 maxLifetime을 넘기면 pool에서 제거된다.

active connection의 경우 pool로 반환된 후 pool에서 제거된다.

idle connection이 4개인 상태에서 1개가 maxLifetime을 넘기면 pool에서 제거되면 빠르게 새로운 idle connection이 추가된다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2010.png)

**pool로 반환되지 않으면 maxLifetime을 지나도 pool에서 제거되지 않는다.**

active connection이 다 사용된 후 반환되지 않으면 pool로 반환되지 않으므로 제거되지 않는다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2011.png)

maxLifetime = 60인데, active connection이 반환되지 않으면 DB Server에서는 해당 connection을 active하다고 인식한다.

DB Server는 wait_timeout 동안 기다리고, 그 동안 해당 connection에서 어떤 요청도 오지 않으면 connection을 close한다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2012.png)

만약 그 이후 DB Server에서 해당 connection으로 요청을 보내려 해도 이미 close되서 Exception이 발생한다. **따라서 사용이 끝난 connection은 즉시 pool로 반환해줘야 한다.**

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2013.png)

maxLifetime은 DB Connection time limit(wait_timeout)보다 몇 초(2 ~ 3초) 정도 짧게 해야 한다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2014.png)

**connectionTimeout**

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2015.png)

BE Server로 요청이 와서 DB Server에 접근할 일이 생겼을 때 DBCP로부터 Connection을 받기 위해 대기해야 하는 시간이다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2016.png)

connectionTimeout이 30초이면, 트래픽이 엄청 몰려오고 모든 connection이 active일 때 DBCP에서 connection이 idle해질 때 까지 최대 30초를 기다린다. 

connectionTimeout이 30초가 지나도록 받지 못한다면 Exception을 발생시킨다. 

connectionTimeout을 잘 설정해야 한다.

보통 일반적인 사용자는 요청을 보내고 30초씩 기다리지 않는다. 많아야 10초 정도 기다린다.

사용자는 10초 정도 기다리다 응답이 없으면 나가는데(Client로부터 연결이 끊긴다.) 29초 즘에 DBCP로부터 connection을 받아서 DB 요청과 응답을 받아서 API 응답을 client에게 주려해도, 이미 client와 연결이 끊겼으므로 응답을 줄 수 없다. 이 경우, connectionTImeout 30초는 너무 길다.

![Untitled](09_3_back-end_dbcp_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2017.png)

**DB Server Parameter, DBCP Parameter를 적절히 잘 설정해야 한다.**