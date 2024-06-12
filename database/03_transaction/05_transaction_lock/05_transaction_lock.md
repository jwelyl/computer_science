# Transaction Lock

[24_04_15_daily_certification](https://www.notion.so/24_04_15_daily_certification-58d72f98a9124025ba90e0cf6fc983b8?pvs=21)

## Transaction

### write-lock

**실제로 데이터베이스에서 write는 생각보다 복잡한 작업이다.** 

- 인덱스가 걸려있다면 인덱스에 대한 처리도 필요하다.
- 실제로 데이터가 저장된 파일에 대한 처리도 필요하다.

하나의 Transaction이 한 데이터에 write하는 동안 다른 Transaction이 해당 데이터에 read/write하려 한다면 문제가 발생할 수 있다.

**이를 방지하기 위해 write_lock을 사용한다.** 

**어떤 Transaction이 데이터에 대해 write_lock을 획득하면 다른 Transaction은 해당 Transaction이 write_lock을 해제할 때까지 해당 데이터에 대해 block된다.**

**예시 (write vs write)**

초기 x = 10이다.

![write_lock_ex1.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/write_lock_ex1.png)

Transaction 1이 먼저 x에 대해 write_lock을 얻었으므로 Transaction 2는 x에 대해 write_lock을 얻으려고 시도하지만 Transaction 1이 x에 20을 write하고 unlock할 때까지 block된다. 

Transaction 1이 unlock하면 Transaction 2가 write_lock을 얻고 x에 20을 write한 후 unlock한다.

**예시 (write vs read, write 먼저)**

초기 x = 10이다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled.png)

Transaction 1이 먼저 x에 대해 write_lock을 얻었으므로 Transaction 2는 x에 대해 read_lock을 얻으려고 시도하지만 Transaction 1이 x에 20을 write하고 unlock할 때까지 block된다. 

Transaction 1이 unlock하면 Transaction 2가 read_lock을 얻고 x=20을 read한 후 unlock한다.

### write-lock (exclusive lock)

- read/write(insert, modify, delete)할 때 사용한다.
    - read할 때도 사용할 수 있다.
- **다른 Transaction이 같은 데이터를 read/write하는 것을 허용하지 않는다.**

### read-lock (shared lock)

- read할 때 사용한다.
- **다른 Transaction이 같은 데이터를 read하는 것은 허용한다.**

**예시 (write vs read)**

초기 x = 10이다.

![read_write_ex1.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/read_write_ex1.png)

Transaction 2가 먼저 x에 대해 read_lock을 얻었으므로 Transaction 1은 x에 대해 write_lock을 얻으려고 시도하지만 Transaction 2가 x=10을 read하고 unlock할 때까지 block된다. 

Transaction 2가 unlock하면 Transaction 1이 write_lock을 얻고 x=20을 write한 후 unlock한다.

**예시 (read vs read)**

초기 x = 10이다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%201.png)

Transaction 2가 먼저 x에 대해 read_lock을 얻었지만 Transaction 1은 x에 대해 read_lock을 얻으려고 시도하고 얻을 수 있다.

Transaction 1, 2 모두 동시에 x=10을 읽고 unlock할 수 있다.

### 정리

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/75e193f5-10d1-4a89-a36b-00d01728819e.png)

### Two-Phase Locking Protocol

Lock을 사용하는 것만으로 Transaction의 Serializability를 보장할 수 없다.

**예시**

초기 x = 100, y = 200이다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%202.png)

Transaction 1, 2는 각각 위와 같이 동작한다.

두 Transaction이 Serial Schedule로 동작한다면 어떨까?

**Transaction 1 → Transaction 2**

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%203.png)

x = 300, y = 500이 된다.

**Transaction 2 → Transaction 1**

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%204.png)

x = 400, y = 300이 된다.

아래와 같은 Schedule로 동작한다고 가정하자.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%205.png)

x = 300, y = 300이다. 위의 어떤 Serial Schedule과도 결과가 다르다. 

![nonserializable.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/nonserializable.png)

즉, 위의 Schedule은 Nonserializable Schedule이다.

이러한 일이 왜 발생할까?

Transaction 2가 업데이트되지 않은 x를 읽었고 Transaction 1은 업데이트되지 않은 y를 읽었다. Transaction 2가 y에 대한 write를 수행하려고 write_lock을 얻으려고 했지만, Transaction 1이 y에 대한 read_lock을 가지고 있어서 y를 업데이트하지 못했고 Transaction 1이 업데이트되지 않은 y를 읽었다.

아래와 같은 Schedule은 Serial Schedule 2와 같은 결과를 내므로 Serializable Schedule이다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%206.png)

각 Transaction에서 write_lock(x)와 unlock(y), write_lock(y)와 unlock(x)의 순서를 바꾸었다.

![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%207.png)

Lock과 관련된 operation만 보면 다음과 같은 특징이 있다.

**Transaction의 모든 Locking Operation이 최초의 Unlock Operation보다 먼저 수행된다.**

이를 **2PL Protocol (Two-Phase Protocol)**이라고 한다.

### 2PL Protocol

**Transaction의 모든 Locking Operation이 최초의 Unlock Operation보다 먼저 수행된다.**

![2pl_protocol.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/2pl_protocol.png)

- Expanding Phase (Growing Phase)
    
    Lock을 취득하기만 하고 반환하지는 않는 Phase
    
- Shrinking Phase (Contracting Phase)
    
    Lock을 반환하기만 하고 취득하지는 않는 Phase
    

**2PL Protocol은 Serializbility는 보장한다. 하지만 심각한 문제가 발생할 수 있다.**

### 2PL Protocol Deadlock

![deadlock.png](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/deadlock.png)

Transaction 1은 Transaction 2가 획득한 x의 lock을 unlock하기를 기다리고 있고, Transaction 2는 Transaction 1이 획득한 y의 lock을 unlock하기를 기다리고 있다.

**결국 두 Transaction 모두 서로를 기다리느라 진행되지 못한다.**

Deadlock이 발생하는 이유, Deadlock을 해결하는 방법은 OS의 Deadlock을 참고하자.

### 2PL Protocol의 종류

- **Conservative 2PL**
    - 모든 Lock을 취득한 뒤 Transaction을 시작한다.
        
        ![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%208.png)
        
    - Deadlock이 발생하지 않는다.
    - 실용적이지 않다. Transaction 자체가 시작되기 어려울 수 있다.
- **Strict 2PL (S2PL)**
    - Strict Schedule을 보장한다.
    - Recoverability를 보장한다.
    - write-lock을 commit하거나 rollback할 때 반환한다.
        
        ![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%209.png)
        
- **Strong Strict 2PL (SS2PL or Rigorous 2PL)**
    - Strict Schedule을 보장한다.
    - Recoverability를 보장한다.
    - read-lock / write-lock을 commit하거나 rollback할 때 반환한다.
        
        ![Untitled](%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%8C%E1%85%B3%E1%86%BC%20ef1ee6d7779941e38c35974449a20434/24_04_15_daily_certification%2058d72f98a9124025ba90e0cf6fc983b8/Untitled%2010.png)
        
    - S2PL보다 구현이 쉽다.
    - 하지만 read-lock을 가지고 있는 시간이 길어져서 다른 Transaction이 read-lock을 얻기 어렵다.