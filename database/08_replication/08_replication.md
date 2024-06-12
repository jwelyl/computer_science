# Replication

[24_06_08_daily_certification](https://www.notion.so/24_06_08_daily_certification-cf2c1e33294e42e0a6b4b1571a7c3685?pvs=21)

# Replication

DB Server에 장애가 생겼을 때를 대비해서 원본 데이터베이스의 복제본을 가지는 보조 DB Server를 두는 것을 Replication이라고 한다.

![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled.png)

원본 DB Server에 데이터를 삽입/수정/삭제하면 복제본에서도 삽입/수정/삭제해서 Sync를 맞춘다.

![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%201.png)

원본 DB Server를 Master**/Primary**/Leader라고 한다.

보조 DB Server를 Slave/**Secondary**/Replica라고 한다.

### **Replication의 장점**

- **High Availability (고가용성, HA)**
    
    ![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%202.png)
    
    Primary DB Server에 장애가 발생할 경우
    
    ![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%203.png)
    
    BE 서버는 빠르게 Secondary DB Server에서 read/write할 수 있도록 한다. (Fail Over)
    
- **DB Server load 분산**
    
    대부분 Query는 Read Query이다. 따라서 Primary와 Secondary가 나눠서 처리할 수 있다.
    
    ![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%204.png)
    
    BE 서버의 read 요청을 분산시킬 수 있다.
    

## 정리

![Untitled](08_replication/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%205.png)

Partitioning, Sharding, Replication의 더 자세한 내용은 따로 공부해야 한다.