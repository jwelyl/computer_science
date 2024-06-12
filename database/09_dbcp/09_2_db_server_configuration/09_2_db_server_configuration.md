# DB Server Configuration

[24_06_10_daily_certification](https://www.notion.so/24_06_10_daily_certification-9694524834cd43f482a0878914d7c95d?pvs=21)

## DB Server, DBCP 설정(Configuration) 방법

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled.png)

### MySQL, HikariCP (Springboot 2.0 이상)

DB Connection은 BE Server와 DB Server 사이의 연결이므로, BE Server와 DB Server 각각에서 설정(Configuration) 방법을 알아야 한다.

## DB Server Configuration

### MySQL Configuration

**max_connections, wait_timeout**

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%201.png)

**max_connections**

client(Back-End Server)와 맫을 수 있는 최대 connection 수

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%202.png)

최대 4개의 connection이 가능하고, 이미 DBCP에 4개의 connection이 존재한다고 가정할 때,

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%203.png)

Back-End Server에 트래픽이 몰릴 경우 Back-End Server의 과부하가 걸리게 된다.(CPU, Memory 등등)

이를 방지하기 위해 WAS를 한 대 더 투입해 트래픽을 분산시키려 한다.

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%204.png)

하지만 새로운 Back-End Server를 실행시키기 위해서는 DBCP가 DB Server와 Connection을 미리 맺어야 하는데 DB Server의 max_connection만큼 이미 기존 Back-End Server와 connection을 맺고 있기 때문에 맺을 수 없다.

**따라서 DB Server의 max_connection이 적절히 설정되어야 한다.**

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%205.png)

**wait_timeout**

connection이 inactive할 때 다시 요청이 오기까지 얼마의 시간을 기다린 뒤에 close할 지 결정

connection을 하염없이 open한 상태로 유지하는 것도 resource 낭비로 DB Server에 악영향을 준다.

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%206.png)

정상적인 경우에는 Connection이 close되면 BE Server에서 connection을 끊고 DB Server에서도 connection을 끊어 리소스를 반환하면 된다.

하지만 비정상적으로 connection을 종료하거나, connection이 사용은 안되지만 반환되지 않거나, 네트워크가 단절될 경우에도 DB Server 입장에서는 연결이 정상적이라고 생각하여 BE Server로부터 요청을 기다리며 resource를 낭비하게 된다. 이는 DB Server에 악영향을 준다.

![Untitled](09_2_db_server_configuration/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%207.png)

이를 방지하기 위해 DB Server에서 wait_timeout을 설정하고, wait_timeout 동안 기다린 후에도 요청이 없으면 connection을 close한다.

만약 wait_timeout이 끝나기 전에 요청이 도착하면 요청에 대한 응답을 보내준 후 다시 wait_timeout 동안 기다린다.