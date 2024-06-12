# Partitioning

[24_06_08_daily_certification](https://www.notion.so/24_06_08_daily_certification-cf2c1e33294e42e0a6b4b1571a7c3685?pvs=21)

# Partitioning

Database 테이블을 더 작은 Table들로 나누는 것 

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled.png)

- Vertical Partioning
- Horizontal Partioning

## Vertical Partioning

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%201.png)

Column을 기준으로 Table을 나누는 방식

테이블의 Schema가 변화한다.

### Normalization (정규화)

[Normalization](https://www.notion.so/Normalization-0fd21c574d814475bf33059d4c7766bb?pvs=21)

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%202.png)

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%203.png)

### Vertical Partitioning by Use Case

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%204.png)

화면에서는 content 데이터는 보여줄 필요가 없다.

```sql
SELECT id, title, writer_id, created_at, read_cnt, comment_cnt
FROM article;
```

하지만 쿼리와 관계 없이 일단 Secondary Storage(HDD, SSD)에서는 Row를 통째로 가져온다.

전체 데이터를 Main Memory에서 가져온 후, 원하는 attribute만 사용한다.

따라서 사용하지도 않을 용량이 큰 content에 대한 I/O 부담이 크다.

이를 해결하기 위해 다음과 같이 테이블을 분리할 수 있다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%205.png)

화면에서는 content 데이터는 보여줄 필요가 없다.

```sql
SELECT id, title, writer_id, created_at, read_cnt, comment_cnt
FROM article;
```

용량이 큰 content는 분리된 article_content에 존재하므로 Main Memory에 가져올 필요가 없다.

따라서 필요한 attribute들만 빠르게 Main Memory에 가져올 수 있다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%206.png)

특정 게시글을 누르면 해당 게시글의 정보는 이미 article에서 가져와 FE에서 저장해 두었으므로 그 정보를 이용해 article_content 테이블을 조회해서 content를 가져오면 된다.

이미 정규화가 되어있는 테이블이라도 performance를 위해 Vertical Partitioning이 가능하다.

그 외에도 민감한 정보를 한 번에 가져올 수 없도록 분리하거나, 자주 사용되는 attribute와 그렇지 않은 attribute를 구분해서 Vertical Partitioning을 할 수도 있다. (전체 데이터는 JOIN으로 얻는다.)

## Horizontal Partitioning

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%207.png)

Row를 기준으로 Table을 나누는 방식

테이블의 Schema는 그대로 유지된다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%208.png)

사용자 수가 N명, 채널 수가 M명이면 최악의 경우 구독 수는 N * M이 되어 row가 N * M개가 된다.

N이 100만, M이 1000이면 row 개수는 10억개가 된다.

**테이블 크기가 커질 수록 테이블의 Index 크기도 커진다.**

**테이블에 읽기/쓰기가 있을 때마다 Index에서의 처리되는 시간도 조금씩 늘어난다.**

### Horizontal Partitioning by Hashing

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%209.png)

테이블을 여러개로 분리하고, **Partition Key(user_id)의 Hash결과에 따라 분리된 테이블에 저장한다.**

**같은 schema를 가진 테이블이 여러 개 생긴다.**

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_06_08_daily_certification%20cf2c1e33294e42e0a6b4b1571a7c3685/Untitled%2010.png)

Partition Key로 조회할 경우, Partition Key의 결과에 따른 분리된 하나의 테이블에서 조회하면 된다.

Partition Key가 아닌 값으로 조회할 경우, 분리된 모든 테이블에 대해서 조회를 해야 한다.

**따라서 조회에 가장 많이 사용될 패턴에 따라 Partition Key를 정해야 한다.**

또한 Hash Function을 잘 정의해서 분리된 모든 테이블에 **데이터가 균등하게 분배될 수 있도록** 해야 한다.

한 번 Hash Function으로 Partion을 정하면 Partition을 추가하기가 어려우므로 처음에 잘 정해야 한다.