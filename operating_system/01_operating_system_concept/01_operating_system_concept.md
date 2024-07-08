# Operating System Concept

# Operating System

## Resource

- 모든 프로그램은 실행을 위해 **시스템 자원(System Resource)**를 필요로 한다.
- 프로그램 실행에 있어서 반드시 필요한 요소
- **컴퓨터의 네 가지 핵심 부품 (H/W Resource)**
    - **CPU**
    - **Memory**
    - **Secondary Storage**
    - **I/O Device**
- S/W Resource
    - 네트워크 패킷
    - 파일
    - etc

## Operating System (OS)

- 실행할 프로그램에 **필요한 Resource를 할당**한다.
- 응용 프로그램(Application Software)이 올바르게 실행되도록 도와준다.
- **OS 또한 프로그램이다. (Memory에 적재되어 실행되는 특별한 프로그램, System Software)**
    
    ![user_kernel.jpeg](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/user_kernel.jpeg)
    

OS가 적재되는 메모리 영역이 **Kernel Space**이다. OS 외의 일반적인 Application Program/Software이 적재되는 영역은 **User Space**이다.

### Memory Management

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled.png)

워드 프로세서를 실행시켰을때, 워드 프로세서가 2000번지에 적재되는 것은 사용자가 지정한 것이 아니다.

**운영체제가 적재하는 것이다.**

**실행될 프로그램을 메모리의 알맞은 주소에 적재하는 것도, 실행이 완료된 프로그램을 메모리에서 제거하는 것도 OS가 담당한다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%201.png)

### CPU Management

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%202.png)

하나의 프로그램만 실행하는 경우는 없다. 여러 프로그램이 동시에 실행된다.
**정확히는 여러 프로그램이 CPU를 빠르게 번갈아가며 사용한다.**

**어떤 프로그램을 먼저 실행할지, 어떤 프로그램이 얼마나 오래 CPU를  사용할 지** 등등을 사용자가 정하지 않는다.

**이를 결정하는 것이 OS이다.**

### I/O Device Management

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%203.png)

어떤 프로그램이 먼저 프린터를 사용할 지, 어떤 프로그램이 먼저 모니터에 출력할 지, 파일을 어떻게 관리할 지 또한 사용자가 결정하지 않는다. **OS가 결정한다.**

![os.jpeg](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/os.jpeg)

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%204.png)

- **OS는 Application Software와 Hardware 사이에 위치하여 둘 사이를 연결해준다.**
- **OS는 H/W와 맞닿아 있다.**
- **OS는 Application S/W에 필요한 H/W Resource를 할당하여 올바르게 실행되도록 한다.**

### OS가 없다면?

H/W에 접근하고 조작하는 코드를 개발자가 직접 작성해야 한다.

```c
#include <stdio.h>

int main(void) {
	printf("%d\n", 1 + 2);
	return 0;
}
```

위와 같은 간단한 코드조차

- 프로그램을 메모리에 적재하는 코드
- CPU가 1과 2의 덧셈을 계산하는 코드
- 모니터에 계산 결과를 출력하는 코드
- …

위의 과정을 개발자가 모두 직접 작성해야 한다.

```c
printf("Hello World!");
```

printf만 해도 OS의 도움을 받아서 화면에 Hello World!를 출력할 수 있다.

### OS를 굳이 알아야 하는 이유?

**OS는 프로그램을 위한 프로그램이다.**

어차피 OS가 다 알아서 해주는데 굳이 배워야 하나?

일반인은 몰라도 된다.

**개발자는 알아야 한다.**

개발자가 개발한 프로그램이 OS에 어떤 도움을 받을 지 알아야 한다.

**OS도 프로그램이므로 CPU, Memory와 같은 H/W보다는 개발자가 이해하기 쉽다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%205.png)

위와 같은 Error Message를 통해 문제 해결 능력을 키울 수 있다.

# Kernel

**OS는 매우 거대한 프로그램이다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%206.png)

Linux는 2천 7백만 줄, Windows 10은 5천만 줄이다. 사실 더 크다.

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%207.png)

운영체제는 종류가 매우 다양하다. (Windows, macOS, Linux, android, iOS 등등)

다양한 종류만큼 제공하는 기능도 다양하다.

하지만 모든 OS가 제공하는 공통적인 **핵심적인 서비스**가 존재한다.

**OS의 핵심적인 서비스**

- 자원에 접근하고 조작하는 기능
- 응용 프로그램이 올바르게 실행되도록 하는 기능

## Kernel

**OS의 핵심적인 서비스를 담당하는 부분을 Kernel이라고 한다.**

자동차의 엔진, 사람의 심장 또는 뇌와 같은 핵심 부분이다.

**OS라는 것은 결국 Kernel을 지칭하는 것이다. (OS = Kernel + User Interface)**

![kernel.jpeg](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/kernel.jpeg)

### User Interface

GUI, CLI 등등 OS에 속하지만 핵심은 아니다.

# Dual Mode, System Call

**메모장, 워드 프로세서, 스타크래프트는 H/W, S/W Resource에 직접 접근할 수 없고, 접근해서도 안된다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%208.png)

- **응용 프로그램은 자원에 직접 접근할 수 없다.**
- **응용 프로그램은 OS를 통해서만 자원에 간접적으로 접근 가능하다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%209.png)

- **응용 프로그램은 OS의 코드를 실행하여 자원에 간접적으로 접근한다.**

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2010.png)

응용 프로그램이 HDD에 접근하려면 OS의 HDD에 접근하는 코드를 실행하여 HDD에 간접적으로 접근한다.

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2011.png)

이렇게 OS가 Application S/W의 Resource 접근을 대행하는 것은 Dual Mode로 구현한다.

## Dual Mode

**CPU가 명령어를 실행하는 모드를 User Mode와 Kernel Mode로 구분하는 방식이다.**

### User Mode

- OS의 서비스를 제공받을 수 없는 실행 모드이다.
    - OS가 자원에 대신 접근하는 서비스를 제공받을 수 없다.
    - User Mode에서 자원 접근 명령어를 실행하려 할 경우 오류가 발생한다.
- Kernel Space의 코드를 실행할 수 없다.
- H/W, S/W Resource에 접근할 수 없다.

### Kernel Mode

- OS의 서비스를 제공받을 수 있는 실행 모드이다.
    - Kernel Space의 코드를 실행할 수 있어서 OS가 대신 자원에 접근하는 서비스를 제공받을 수 있다.
- 자원 접근을 비롯한 모든 명령어를 실행할 수 있다.

**User Mode/Kernel Mode는 CPU의 Flag Register로 구분한다.**

Flag Register의 Supervisor Flag를 통해 확인 가능하다.

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2012.png)

자원 접근 명령어는 Kernel Mode일 때만 실행 가능하고, User Mode에서는 실행할 수 없다.

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2013.png)

Dual Mode는 Kernel Mode와 User Mode를 나누어 **Kernel Mode일 경우에만 OS를 통해 자원 접근이 가능**하여 **Application Software가 임의로 자원에 접근하는 것을 방지해서 자원을 보호한다.**

언제 Kernel Mode로 변경될까? → System Call

## System Call

- **User Mode에서 Kernel Mode로 전환하여 실행하기 위한 호출이다.**
- **Software Interrupt 중 하나이다.**

![system_call.jpeg](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/system_call.jpeg)

Application Program이 User Mode에서 실행 중 자원에 접근해야 할 경우 System Call을 통해 Kernel Mode로 전환되어 자원 접근이 가능한 Kernel Code를 실행하여 자원에 접근한다.

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2014.png)

![syscall_interrupt.jpeg](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/syscall_interrupt.jpeg)

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2015.png)

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2016.png)

응용 프로그램은 자원에 빈번히 접근하므로 System Call도 자주 발생한다.

# Operating System Core Service

## Process Management

- **Process : Memory에 적재되어 실행중인 프로그램**
- 수많은 Process들이 동시에 실행되고 있다. (CPU를 번갈아가며 점유하여 실행된다.)
- 동시에 생성/실행/삭제되는 Process들을 관리한다.
- Process, Thread, Synchronization, Deadlock

![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2017.png)

## Resource Access, Allocation

- **CPU Scheduling**
    - 어떤 Process를 먼저 실행하고, 얼마나 오래 실행할까?
    - 어떤 Process가 CPU를 먼저 사용하고, CPU를 얼마나 오래 사용할까?
    
    ![Untitled](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/Untitled%2018.png)
    
- **Memory**
    - Process를 Memory의 어느 위치에 적재할 것인가?
    - Paging : 꼭 Process의 모든 코드를 Memory에 적재해야 하는가?
    - Swapping : Process의 크기가 Memory보다 클 경우 어떻게 할 것인가?
    
    ![memory.png](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/memory.png)
    
    ![swapping.png](Operating%20System%20Concept%20e66c0995f5384ee29bd7119035fce485/swapping.png)
    
- **I/O Device**
    - Interrupt Service Routine

## **File System**

- Secondary Storage에 존재하는 정보를 File이라는 단위로, File을 묶어 Directory 단위로 저장한다.
- File
- Directory