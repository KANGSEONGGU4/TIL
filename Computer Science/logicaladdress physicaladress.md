## 물리 주소(Physical Address)

메모리 입장에서 실제로 데이터가 저장된 물리적인 주소를 나타낸다. 주로 하드웨어에서 사용되며 각 데이터의 실제 물리 위치를 가르킨다. 각 주소는 하나의 데이터 위치를 가르키고 물리주소끼리는 겹치지 않는다.

## 논리 주소(Logicla Address)
CPU와 실행 중인 프로그램 입장에서 바라본 주소이다. 각 프로그램은 0번지부터 시작하는 독립적인 논리 주소 공간을 할당 받는다. 서로 다른 프로그램이 동일한 논리 주소를 사용할 수 있으며 이는 각 프로그램이 독립적인 주소 공간을 가지게 하기 위함이다.   
메모리가 사용하는 주소는 하드웨어상의 실제 주소인 물리 주소이고 CPU와 실행 중인 프로그램이 사용하는 주소는 각각의 프로그램에 부여된 논리주소이다. CPU간의 이해하는 주소가 논리주소라고 해도 CPU가 메모리와 상호작용하려면 논리 주소와 물리주소간의 변환이 이루어져야한다.

## 메모리 관리 장치(MMU, Memory Management Unit) 하드웨어
MMU는 논리 주소와 베이스 레지스터(프로그램의 기준주소)값을 더하여 논리 주소를 물리 주소로 변환한다.

### 변환 과정
1. 베이스 레지스터의 역할
베이스 레지스터는 현재 실행 중인 프로그램의 시작 물리 주소를 저장한다. 이는 해당 프로그램이 메모리 어디에 위치하고 있는지 가르키는 것이다.
2. 주소 변환
CPU가 발생시킨 논리 주소와 베이스 레지스터 값을 더하여 논리 주소를 물리주소로 변환한다.   
논리 주소 + 베이지 레지스터 값 = 물리주소

### 메모리 보호 기법

#### 한계 레지스터

다른 프로그램의 영역을 침범할 수 있는 명령어는 위험하기 때문에 논리 주소 범위를 벗어나는 명령어 실행을 방지하고 실행 중인 프로그램이 다른 프로그램에 영향을 받지 않도록 보호할 방법으로 한계 레지스터를 사용한다.

#### 주소 범위 제한

프로그램의 물리 주소 벙위는 베이스 레지스터 값 이상에서부터 베이스 레지스터 값에 한계 레지스터 값을 더한 값 미만까지로 제한된다.   
베이스 레지스터 값 <= 프로그램의 물리주소 범위 < 베이스 레지스터 값 + 한계 레지스터 값