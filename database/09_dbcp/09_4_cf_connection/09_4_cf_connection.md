# cf. 적절한 Connection 개수 정하기

[24_06_10_daily_certification](https://www.notion.so/24_06_10_daily_certification-9694524834cd43f482a0878914d7c95d?pvs=21)

## cf. 적절한 Connection 수 정하기

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled.png)

Primary DB Server는 Read/Write 둘다 처리

Secondary DB Server(Replication)는 Read만 처리

일단 Primary DB Server만 고려

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%201.png)

**부하 테스트**

- 요청을 조금씩 늘려가면서 BE Server가 어떻게 동작하는 지 테스트한다.
- request per second
- average response time
- nGrinder (NAVER)

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%202.png)

트래픽이 많아질 수록 request per second는 더 이상 증가하지 못하고, average response time은 크게 증가한다. 즉, 성능이 떨어진다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%203.png)

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%204.png)

BE Server의 CPU, Memory 리소스 사용량을 확인해보고 일정 수준 이상이면(60% 이상), 현재 BE Server만으로는 트래픽을 처리를 못하므로 추가해줘야 한다. BE Server 추가를 통해 트래픽을 분산시킬 수 있다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%205.png)

만약 Server의 CPU, Memory 리소스 사용량이 일정 수준 이상이면 여러 방법이 있다.

- Secondary Server 추가
    
    select 쿼리를 분산시킬 수 있다.
    
- Cache Layer
    
    DB Server가 직접 받는 부하를 줄여준다
    
- Sharding

만약 BE Server, DB Server 모두 적정량의 리소스를 사용하는데도 성능이 일정 트래픽 이상에서 급격히 나빠진다면 

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%206.png)

**thread per request 모델**

request마다 thread를 할당하는 모델이라면, thread pool의 active thread 수를 확인하고 필요 시 늘려준다.

만약 thread pool의 여우 thread가 많다면 thread 문제는 아니다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%207.png)

이 때 DBCP의 active connection의 수를 확인하고 BE Server의 maximumPoolSize를 올려준다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%208.png)

maximumPoolSIze 합이 DB Server의 max_connections 수와 같을 때 까지 늘려본다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%209.png)

그 이후에는 DB Server의 max_connections를 증가시키고 그에 맞게 maximumPoolSize를 증가시켜본다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2010.png)

이렇게 각 parameter들을 조정하면서 원하는 트래픽을 잘 처리하는 값을 찾는다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_10_daily_certification%209694524834cd43f482a0878914d7c95d/Untitled%2011.png)

**DB Server의 max_connections 수를 먼저 정하고, 그에 맞춰 BE Server 수(예비 Server)를 고려해 maximumPoolSize를 정하면 된다.**

**참고**

[Commons DBCP 이해하기](https://d2.naver.com/helloworld/5102792)