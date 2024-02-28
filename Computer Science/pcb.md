> ### 프로세스 제어 블록(Process Control Block)
> 프로세스 제어 블록(이하 PCB)은 특정한 프로세스를 관리할 필요가 있는 정보를 포함하는 운영 체제 커널의 자료 구조이다.
> 쉽게 말하면 운영체제가 프로세스를 제어하기 위해 프로세스의 상태 정보를 저장해 놓는 구조체이다.   
 
 

PCB는 다음과 같은 항목들을 저장하고 있다. 

- Process Id : 프로세스의 고유 번호
- Process State : ready, wait, running 등의 실행 상태
- Program Counter(PC) : 프로그램 카운터, 다음 실행될 명령의 포인터
- CPU registers :  CPU 레지스터
- CPU scheduling information : CPU 스케줄링 정보 
- Memory-management information : 할당된 자원 정보
- Accounting information : CPU 사용시간 등 
- I/O status information : 입출력 상태 정보

## Context Switching
Context Switching을 알아보기 전에, Context(문맥)가 무엇인지 알 필요가 있다. 
 
Process의 Context란 프로그램 카운터(PC), CPU 레지스터들의 값, 메모리 관리 상태 등을 포함한 프로세스의 상태를 뜻한다.
 

Context Switching은 동작 중인 프로세스의 상태를 PCB에 보관하고 context를 바꿀 프로세스의 상태를 불러와 복구하는 과정을 뜻한다. 


P0를 실행 중 interrupt가 발생하거나 system call이 발생하면 P0의 상태를 PCB0에 저장한다.
PCB1에 저장된 P1의 상태를 불러와 복구한다.
P1를 실행한다.   
이때 다시 interrupt가 발생하거나 system call이 발생하면 P1의 상태를 PCB1에 저장한다.
PCB0에 저장된 P0의 상태를 불러와 복구한다.
P0를 실행한다.

## Context Switching Overhead
Context Switching은 오버헤드가 존재한다. 이때 오버헤드는 Context Switching에 걸린 시간과 메모리를 뜻한다.   
Context Switching 오버헤드는 machine 마다 다르다. 일반적으로 매우 적은 시간이 걸린다.