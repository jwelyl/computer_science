# Sharding

[24_06_08_daily_certification](https://www.notion.so/24_06_08_daily_certification-cf2c1e33294e42e0a6b4b1571a7c3685?pvs=21)

# Sharding

![Untitled](07_sharding/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled.png)

Horizontal Partioning과 같이 동작한다.

**하지만 각 Partition이 독립된 Database Server에 저장된다.**

### Horizontal Partitioning

![Untitled](07_sharding/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%201.png)

하나의 DB Server에 모든 Partition에 대한 BE 서버 요청이 몰리므로, Hardware 리소스가 한정된다.

### Sharding

![Untitled](07_sharding/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%202.png)

Partition 별로 BE 서버 요청이 각기 다른 DB Server에서 처리되므로 **DB Server의 load를 분산시킬 수 있다.**

**규모가 큰 서비스, 데이터가 많이 저장되는 테이블, Traffic이 많이 몰리는 테이블에 대해 고려할 수 있다.**

Sharding에서의 Partition Key는 Shard Key, Partition은 Shard라고 한다.