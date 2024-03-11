## 프로세스 스케줄링 = CPU 스케줄링
운영체제가 수행해야할 역할 중 가장 핵심적인 역할이다.   
각각의 운영체제는 자기만의 강점이 될 수 있는 스케줄링 알고리즘을 가지고 있다.
 
 
### 스케줄링 큐 (queue)
운영체제가 이해하는 프로세스는 PCB이기 때문에, 스케줄링 큐는 PCB의 링크드 리스트로 관리되고 있다.
 
1. Job queue : 시스템 안에 존재하는 프로세스들
2. Ready queue : 메모리 상 존재하며 실행 준비가 되어 있는 프로세스들
3. Device queue : 입출력 장치의 사용을 기다리는 프로세스들
 


### 선점 스케줄링 (Preemptive Scheduling)
운영체제의 판단에 따라 현재 실행 중인 프로세스를 강제로 중단시키고, CPU 스케줄링을 수행한다.   
타이머 인터럽트가 발생하거나 입출력 완료 시에 해당 된다.   


장점 : 각 프로세스의 빠른 응답을 지원할 수 있다.


단점 : 문맥 교환(Context Switch)을 위한 커널 코드가 실행이 빈번하게 발생하여 overhead가 증가한다. 
(현재 프로세스의 PCB 저장과 새로운 프로세스를 위한 PCB 복구를 위한 overhead)
 
### 비선점 스케줄링 (Nonpreemptive Scheduling)

현재 실행 중인 프로세스가 자발적으로 CPU 사용을 중단하는 경우에만 CPU 스케줄링을 수행하는 방법

실행중인 프로세스가 종료되거나 (Running -> Terminated) 외부 장치 입출력 요청 시 (Running -> Waiting) 프로세스가 스스로 CPU 사용을 중단하고, 자신의 상태를 변경한다.