# Disadvantage of Relational Database

# Relational Database의 단점

## 1. 경직된 Schema

쇼핑몰에서 상품의 주문 정보를 아래와 같은 Order 테이블로 관리한다고 생각해보자.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled.png)

만약 서비스를 확장하여 로켓 배송 기능을 추가하고 싶다. 기존 Order 테이블로는 각 주문이 로켓 배송인지 확인이 불가하므로 rocket_delivery 컬럼을 추가해야 한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%201.png)

**새로운 컬럼을 추가할 때는 반드시 기존 schema가 변경된다.**

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%202.png)

만약 주문에 이벤트를 추가하고 싶으면 event_id 컬럼을 또 추가해야 한다. 또 schema가 변경된다.

주문이 적어서 Order 테이블의 데이터가 적을 경우에는 별 문제가 안될 수 있지만, 데이터가 많을 경우 새로운 컬럼을 추가할 때 위험 부담이 커진다. (Heavy-write로 인한 DB Server 부담, BE Server 부담)

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%203.png)

Relational Database는 schema를 미리 정의하고 정의한 schema에 맞춰서 데이터를 저장하기 때문에, 테이블에 컬럼을 추가하는 등의 확장이 필요할 경우, 유연한 확장성이 부족하다.

## 2. 과도한 JOIN으로 인한 성능 하락

RDB는 중복으로 저장되는 데이터를 제거를 위한 정규화가 필수적으로 진행된다. (1NF, 2NF, 3NF, BCNF)

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%204.png)

하나의 테이블을 여러 테이블로 분리하면서 데이터의 중복 저장은 사라진다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%205.png)

하지만 원래 전체 데이터를 조회하기 위해서는 여러 테이블의 JOIN이 필요하다.

JOIN을 하려면 DB Server에서 CPU를 많이 사용하게 된다.

또한 응답 시간이 늘어나서 복잡한 JOIN은 read 성능이 낮아진다.

## 3. Scale-out에 적합하지 않음

### Scale-up vs Scale-out

- Scale-up : 한 대의 컴퓨터의의 성능을 높여서(CPU, Memory, …) 서버의 성능을 높임
- Scale-out : 여러 대의 서버를 두어 하나의 서버에 부하가 심해지는 것을 방지

RDB는 기본적으로 한 대의 컴퓨터에 저장된다. 한 대의 컴퓨터에 하나의 Database가 존재하고 여러 테이블이 존재한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%206.png)

한 대의 DB Server에 많은 read/write 요청이 몰리게 되면 DB Server의 부하가 심해진다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%207.png)

RDB는 scale-up을 통해 데이터베이스 성능을 향상시킨다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%208.png)

RDB는 또한 replication을 read-only로 두어 select 쿼리 부하를 분산시킨다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%209.png)

하지만 write 트래픽이 대부분이라면 primary DB Server에 부하가 심해지는 것은 어쩔 수 없다.

그 외에도 Sharding, Multi-master 방법이 존재한다.

Replication, Sharding, Multi-master와 같은 방법은 Scale-out에 속한다.

**하지만 RDB는 일반적으로 Scale-out에 적합하진 않다.**

- Replication을 Secondary Server로 둘 경우 Primary Server 전체를 복제해야 한다.
- Write 트래픽이 많아서 Sharding할 경우, 데이터를 옮겨야 한다. 서비스가 운영중일 경우 데이터를 옮기는 것은 쉽지 않다.

## 4. Transaction ACID

RDB에는 Transaction ACID 자체는 장점도 있지만 이를 보장하기 위한 trade-off로 단점도 존재한다.

![Untitled](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_17_daily_certification%200dab231eecb84747827592e29b1c92ba/Untitled%2010.png)

대표적으로 Isolation Level을 높일 수록 DB Server의 Performance가 저하된다.