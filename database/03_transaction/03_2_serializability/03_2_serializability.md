# Transaction, Schedule, Serializability

[24_04_08_daily_certification](https://www.notion.so/24_04_08_daily_certification-e2957cd6887d47b18ec955ae8e7a4521?pvs=21)

## Schedule, Serializability

A가 B에게 20만원을 이체할 때, B도 본인에게 30만원을 입금하는 경우를 생각해보자.

다음과 같은 여러 형태의 실행이 가능하다.

### **case 1**

![concurrency1.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/concurrency1.jpeg)

A가 B에게 20만원을 이체하는 트랜잭션 1이 발생한 후, B가 A에게 30만원을 이체하는 트랜잭션 2가 발생한다.

### **case 2**

![concurrency2.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/concurrency2.jpeg)

B가 A에게 30만원을 이체하는 트랜잭션 2가 발생한 후, A가 B에게 20만원을 이체하는 트랜잭션 1이 발생한다.

### case 3

![concurrency3.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/concurrency3.jpeg)

A가 B에게 20만원을 이체하는 트랜잭션 1 중, A의 잔액을 읽고 20만원을 뺀 80만원을 쓴 다음에 트랜잭션 2가 발생하여 B의 계좌에 30만원을 추가하여 트랜잭션 2가 종료된 후, 트랜잭션 1 중 B의 잔액을 확인하고 20만원을 추가한 금액을 쓴 후 트랜잭션 1이 종료된다.

### case 4

![concurrency4.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/concurrency4.jpeg)

A가 B에게 20만원을 이체하는 트랜잭션 1 중, A의 잔액을 읽고 20만원을 뺀 80만원을 쓰고, B의 계좌를 읽어 200만원을 확인한 다음에 트랜잭션 2가 발생하여 B의 계좌를 읽어서 200만원을 확인하고, 30만원을 추가한 금액 230만원을 쓴 다음에 트랜잭션 2를 종료한다. 트랜잭션 2가 종료된 후, 트랜잭션 1의 남은 연산인  20만원을 추가하는 연산을 수행하여 이전에 읽은 200만원에 20만원을 추가한 220만원을 쓰고 트랜잭션 1을 종료한다.

**30만원을 추가한 Update가 사라졌다. Lost Update가 발생한다.**

**case 1 ~ 4에서 read, write 하나 하나를 operation이라고 한다.**

k번 Transaction의 X의 계좌를 read하는 operation을 간단하게 rk(X)라고 하고, X 계좌에 write하는 것을 간단하게 wk(X)라고 하자. k번 Transaction을 commit하는 것을 ck로 나타낼 수 있다.

case 1 ~ 4를 간소화해서 나타내면 다음과 같다. 물론 case 1 ~ 4 외에도 더 많은 경우가 존재할 수 있다.

![schedule.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/schedule.jpeg)

### Schedule

여러 transaction들이 동시에 실행될 때, 각 transaction에 속한 operation들의 실행 순서를 **schedule**이라고 한다. 이 때, 각 transaction 내의 operation들의 순서는 바뀌지 않는다.

위의 case 1, 2, 3, 4 각각이 schedule이다.

![schedule.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/81658b7c-1314-4c00-a9de-cb8c551d23e7.png)

**Serial Schedule**

schedule 1, 2는 두 transaction이 겹치지 않고 한 번에 하나씩 실행된다. transaction1이 모두 실행되고 transaction2가 실행되거나, transaction2가 모두 실행되고 transaction1이 실행된다. 이러한 schedule을 Serial Schedule이라고 한다.

![interleaving.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/interleaving.jpeg)

**Nonserial Schedule**

schedule 3, 4는 두 transaction의 operation들이 겹쳐서(interleaving) 실행된다. 그림 상으로는 Transaction 1의 operation들과 Transation2의 operation이 나란히 일렬로 있는 것 같지만 실제로는 동시에 실행될 수 있고 Serial Scheulde보다 빠르게 끝난다.

### Serial Schedule vs Nonserial Schedule

**Serial Schedule**

한 Transaction의 read, write 작업은 I/O 작업인데, I/O 작업을 하는 동안 CPU는 idle한 상태가 된다. CPU가 다른 Transaction을 실행할 수도 있는데 Serial Schedule이므로 그럴 수 없다. 따라서 성능이 떨어진다.

**Lost Update와 같이 잘못된 데이터가 저장될 일은 없다.** 

**하지만 한 번에 하나의 Transaction만 실행하기 때문에 현실적으로 사용할 수 없을 정도로 성능이 매우 떨어진다.**

**Nonserial Schedule**

한 Transaction의 read, write 작업은 I/O 작업인데, 한 Transaction의 I/O 작업을 하는 동안 CPU는  다른 Transaction을 실행한다.

**Transaction들이 겹쳐서 실행되기 때문에 동시성이 높아져서 같은 시간동안 더 많은 Transaction들을 처리할 수 있다.**

**하지만 Transaction들이 어떤 형태로 겹쳐서 실행되는지에 따라 잘못된 데이터가 저장될 수 있다.**

### Serial Schedule과 equivalent한 Nonserial Schedule

Nonserial Schedule을 사용하되 Serial Schedule처럼 정확한 결과를 얻고 싶다면, Serial Schedule과 동일한(Equivalent) Nonserial Schedule을 만들면 된다.

### **Equivalent Schedule**

**Conflict**

어떤 두 개의 operation이

1. **서로 다른 Transaction에 소속되어 있다.**
2. **같은 데이터에 접근한다.**
3. **둘 중 최소 하나는 write operation이다.**

위 3개의 조건을 모두 만족하면 두 operation은 conflict이다.

Schedule 3에는 총 3개의 Conflict가 존재한다.

![conflict.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/conflict.jpeg)

**두 개의 Conflict한 Operation의 순서가 변경되면 결과가 바뀐다.**

![conflict_swapl.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/conflict_swapl.jpeg)

**Conflict Equivalent**

어떤 두 schedule이

1. **같은 Transaction들을 가진다.**
2. **어떤 Conflicting Operations의 순서도 양쪽 Schedule 모두 동일하다.**

두 조건을 만족하면 두 Schedule은 **Conflict Equivalent**하다.

![conflict_equivalent.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/conflict_equivalent.jpeg)

Schedule 2와 Schedule 3은 모두 동일한 Transaction과 Conflict를 가지고 있고, Conflictin Operations의 순서도 동일하다. 따라서 Schedule 2와 Schedule 3은 Conflict Equivalent하다.

한편 Schedule 2는 Serial Schedule이고 Schedule 3은 Nonserial Schedule이므로 Schedule 3은 Serial Schedule과 Conflict Equivalent하다.

**어떤 Schedule이 Serial Schedule과 Conflict Equivalent할 때 해당 Schedule을 Conflict Serializable하다고 한다.**

따라서 Schedule 3은 Nonserial Schedule이지만 올바른 결과를 도출한다.

![non_conflict_serializable.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/non_conflict_serializable.jpeg)

Schedule 2와 Schedule 4은 모두 동일한 Transaction과 Conflict를 가지고 있다.

하지만 Schedule 2는 Conflicting Operations의 순서가 w2(B), r1(B)의 순서지만, Schedule 4는 r1(B), w2(B)의 순서로 순서가 반대이다.

따라서 Schedule 4는 Schedule 2와 Conflict Equivalent하지 않다.

그래도 만약에 Schedule 4가 Schedule 1과 Conflict Equivalent하다면, Schedule 4는 Conflict Serializable할 것이다. 하지만 그렇지 않다면 Schedule 4는  Conflict Serializable하지 않으므로 잘못된 결과를 도출할 수 밖에 없다. (Transaction이 총 2개이므로 Serializable한 Schedule은 1, 2 두 개 뿐이다.)

![non_conflict_serializable2.jpeg](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_08_daily_certification%20e2957cd6887d47b18ec955ae8e7a4521/non_conflict_serializable2.jpeg)

하지만 Schedule 1의 Conflict Operations의 순서는 w1(B), r2(B)와 w1(B), w2(B)이므로 Schedule 4의 Conflict Operations의 순서인 r2(B), w1(B)와 w2(B), w1(B)의 순서와 일치하지 않는다.

따라서 Schedule 4는 Schedule 1과 Conflict Equivalent하지 않다.

**Schedule 4는 그 어떤 Serial Schedule과도 Conflict Equivalent하지 않으므로 Conflict Serializable하지 않다. 따라서 잘못된 결과를 도출하게 된다.**

### 구현

**그러면 여러 Transaction이 실행될 때마다, 해당 Schedule이 Conflict Serializable한지 확인할까?**

No!! 

Transaction이 많아지면 Serializable Schedule도 많아지고(n개의 Transaction, n!개의 Serializable Schedule) 그만큼 어떤 Schedule이 Conflict Serializable한지 확인하는 비용도 많이 든다.

Transaction들을 동시에 실행해도 Schedule이 Conflict Serializable하도록 보장하는 Protocol을 적용한다.

**Protocol이 Conflict Serializable한 Schedule만 실행되도록 보장한다.**

### 정리

어떤 Schedule이 있을 때, 어떤 임의의 Serial Schedule과 equivalent하면 해당 Schedule은 Serializable하다고 한다. (Serializability를 가진다고도 한다.)

**Equivalent**

- Conflict Equivalent → Conflict Serializabliity
- View Equivalent → View Serializabliity

### Isolation

어떤 Schedule도 Serializable함을 보장하는 것이 **Concurrency Control이다.**

이것과 관련된 Transaction의 성질이 **Isolation이다.**

Isolation이 너무 엄격하면 성능이 저하되므로 개발자가 적절히 선택할 수 있게 해주는 것이 Isolation Level이다.