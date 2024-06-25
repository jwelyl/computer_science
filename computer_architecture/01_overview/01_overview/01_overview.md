# Overview

# Overview

## 1. Data, Instruction

### 1-1. 데이터 (Data)

- **숫자, 문자, 이미지, 동영상과 같은 정적인 정보**
- 0, 1로 이루이짐
- 컴퓨터와 주고 받는 정보, 컴퓨터에 저장된 정보

### 1-2. 명령어 (Instruction)

- **컴퓨터를 실질적으로 움직이는 정보**
- 데이터는 명령어를 위해 존재하는 재료
- 컴퓨터 프로그램은 명령어의 집합

## 2. 컴퓨터의 4가지 핵심 부품

컴퓨터의 4가지 핵심 부품은 **CPU, Main Memory, Secondary Storage, I/O Device**이다.

![main_board.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/main_board.jpeg)

### 2-1. 주기억 장치(Main Memory)

**현재 실행 중인 프로그램(프로세스)의 데이터와 명령어가 저장된 장치**

비싸고 저장 용량이 적으며, 전원이 꺼지면 메모리에 저장된 데이터, 명령어는 모두 사라진다. (휘발성 저장장치)

![main_memory.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/main_memory.jpeg)

- 메모리에는 현재 실행 중인 프로그램(프로세스)의 데이터와 명령어가 저장되어 있다.
- 프로그램이 실행되기 위해서는 프로그램이 메모리에 저장되어야 한다.
    - 보조 기억 장치에 저장된 프로그램이 메모리에 올라오며 실행된다.
- 메모리에 저장된 명령어와 데이터는 **주소(Address)**를 통해 빠르게 접근할 수 있다.

### 2-2. 중앙 처리 장치(CPU)

**메모리에 저장된 명령어를 읽어들이고 해석하고 실행하는 장치**

크게 ALU, Register, Control Unit으로 구성됨

![cpu.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/cpu.jpeg)

- **ALU** : 프로그램 내부에서 수행되는 계산을 수행하는 부품
- **Register** : CPU 내부의 작은 임시 저장 장치로 프로그램 실행 시 필요한 값들을 저장함, 레지스터마다 역할이 다름
- **Control Unit** : 메모리와 같은 컴퓨터 부품을 제어하는 전기 신호를 보내고, 명령어를 해석하는 부품 ****

### 2-3. 보조 기억 장치(Secondary Storage)

**메모리와 다르게 컴퓨터 전원이 꺼져도 데이터를 영구히 저장하는 장치 (비휘발성 저장 장치)**

![secondary_storage.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/secondary_storage.jpeg)

- 메모리보다 저렴하고 저장 용량이 크다.
- 메모리가 실행 중인 프로세스를 저장한다면, 보조 기억 장치는 프로그램 파일을 영구히 저장한다.
- HDD, Disk, USB Memory 등이 존재한다.

### 2-4. 입출력 장치(I/O Device)

**모니터, 키보드, 마우스와 같이 컴퓨터 외부에 연결되어 컴퓨터 내부와 정보를 주고 받는 장치**

넓은 의미에서 Secondary Storage도 I/O Device에 포함 (Peripheral Device)

보통은  Secondary Storage는 Main Memory를 보조하는 특수한 I/O Device로 구분함

![io_device.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/io_device.jpeg)

### 2-5. Main Board, System Bus

**컴퓨터의 4가지 핵심 부품은 Main Board라는 판에 연결되어 있다.** 

Main Board에 연결된 부품들은 **Bus**라는 통로를 통해 서로 연결되어 있다.

![main_board.jpeg](Daily%20Certification%20ef1ee6d7779941e38c35974449a20434/24_06_25_daily_certification%204fe98a9f2b5b46b48b178cfa9f02ea73/main_board%201.jpeg)

**System Bus**

CPU, Main Memory, Secondary Storage, I/O Device를 연결하는 핵심적인 Bus

- Control Bus : 메모리 읽기, 쓰기와 같은 제어 신호를 주고 받는 통로
- Address Bus : 명령어, 데이터를 읽고 쓰기 위해 메모리와 주소를 주고 받는 통로
- Data Bus : 명령어, 데이터를 주고 받는 통로