## 1. 명령어 파이프라인(Instruction Pipeline)

명령어 파이프라인(Instruction Pipeline)은 CPU의 성능을 향상시키기 위해 명령어 처리를 여러 단계로 나누어 동시에 실행하는 명령어 병렬 처리 기법입니다.

CPU의 명령어가 처리되는 과정은 인출(fetch)과 실행(execution) 2단계로 나눌 수 있다고 했는데, 이를 비슷한 시간 간격으로 나누어 명령어 인출(Instruction Fetch), 명령어 해석(Instruction Decode), 명령어 실행(Execute Instruction), 결과 저장(Write Back) 4단계로 나눌 수도 있습니다.

1) 명령어 인출(Instruction Fetch) : 명령어를 기억장치로 부터 인출

2) 명령어 해석(Instruction Decode) : 디코더를 사용하여 명령어 해석

3) 명령어 실행(Execute Instruction) : 해석된 명령어에 따라 데이터 연산을 수행

4) 결과 저장(Write Back) : 명령어대로 처리된 데이터를 메모리에 기록


## 2. 파이프라인 위험(Pipeline Hazard)

파이프라인 위험(Pipeline Hazard)은 파이프라인 기법을 사용하는데 있어서 발생할 수 있는 문제점을 말합니다.

파이프라인 위험에는 크게 데이터 위험(Data Hazard), 제어 위험(Control Harzard), 구조적 위험(Structural Harzard) 3가지로 나눌 수 있습니다

1) 데이터 위험(Data Hazard)

데이터 위험(Data Hazard)은 명령어 간의 의존성으로 인해 아직 수행되지 않은 명령어의 결과값을 참조함으로써 발생하는 위험입니다.

예를 들어 아래와 같이 명령어1, 명령어2가 있습니다.

명령어1 : R1 ← R2 + R3

명령어2 : R4 ← R1 * R2

명령어1은 R2와 R3 레지스터값을 더하여 R1 레지스터에 저장하고, 명령어2는 R1과 R2 레지스터값을 곱하여 R4 레지스터에 저장합니다.


이 경우 아래와 같이 명령어 파이프라인을 사용한다면 R1 레지스터에 명령어1의 저장단계가 수행되기 전에 명령어2의 인출 및 해석이 발생하기 때문에 잘못된 결과값이 R4 레지스터에 저장됩니다.

이러한 위험을 데이터 위험이라고 합니다. 데이터 위험의 경우 다음과 같이 명령어 단계가 지연(Stall)됩니다.

2) 제어 위험(Control Harzard)

제어 위험(Control Harzard)은 Jump나 Call, Interupt 같은 분기 명령어에 의해 프로그램 카운터(PC)가 갑작스럽게 변함으로써 발생하는 위험입니다.

기본적으로 명령어는 프로그램 카운터가 순차적으로 증가하여 실행됩니다. 하지만 분기(branch) 명령어를 싱행하게 된다면 프로그램 카운터가 비순차적으로 변하기 때문에 동시에 실행되는 명령어가 필요없어지게 될 수도 있습니다.

이러한 위험을 제어 위험이라고 합니다. 제어 위험의 경우 인출 단계 이후에 명령어 단계가 지연(Stall)됩니다.

3) 구조적 위험(Structural Harzard)

구조적 위험(Structural Harzard)은 서로 다른 명령어가 같은 자원에 접근함으로써 발생하는 위험입니다.

예를 들어 Load 명령어의 경우 데이터를 인출하기 위해 메모리에 접근하는 단계가 있어는데, 다음과 같이 동일한 레지스터에 쓰기 접근을 할 수 있습니다.

이러한 위험을 구조적 위험이라고 합니다. 구조적 위험의 경우 다음과 같이 명령어 단계가 지연(Stall)됩니다.

## 3. 슈퍼스칼라(Supserscalar)

슈퍼스칼라(Supserscalar)는 CPU 내에 파이프라인을 여러 개 두어 명령어를 동시에 실행하는 기술로서, 멀티 스레드 프로세서를 의미합니다.

이론적으로는 파이프라인 개수에 비례하여 CPU의 처리 속도가 증가하지만, 그만큼 파이프라인 위험도 증가하므로 실제로 파이프라인 개수에 비례하여 처리 속도가 증가하지는 않습니다.

## 4. 명령어 집합 구조(Instruction set architecture, ISA)



명령어 집합 구조(Instruction set architecture, ISA)는 CPU가 이해할 수 있는 기계어 명령어들의 집합을 의미합니다. 하드웨어와 시스템 소프트웨어 사이의 인터페이스를 정의하며, 최하위 레벨의 프로그래밍 인터페이스로서 CPU가 실행할 수 있는 모든 명령어를 포함합니다.



ISA를 물리적으로 구현한 CPU 내부의 하드웨어 구조를 마이크로 아키텍쳐(Micro Architecture)라고 합니다. CPU 제조사마다 마이크로 아키텍쳐가 다르므로 ISA 역시 서로 다릅니다. 대표적으로 CISC(Complex Instruction Set Computer)와 RISC(Reduced Instruction Set Computer)가 있습니다.

1) CISC(Complex Instruction Set Computer)



CISC(Complex Instruction Set Computer)는 복잡한 명령어 집합을 가지는 CPU로서, 인텔이나 AMD의 x86, x86-64는 CISC 기반의 ISA를 사용합니다.



CISC는 복잡하고 다양한 가변 길이 명령어를 사용하며, 상대적으로 적은 수의 명령어만으로도 프로그램을 실행할 수 있습니다. 그렇기 때문에 메모리를 최대한 아끼며 개발해야 했던 시절에 인기가 높은 아키텍쳐였으나, 가변 길이 명령어를 사용하므로 명령어 파이프라이닝이 불리하며 속도가 느리고 가격이 비싸다는 단점이 있습니다.



일반적으로 하드웨어 스택(Stack)이 내장되어 있으며, 서브루틴의 return 주소나 파라미터, 지역변수 등을 저장하는데 사용됩니다. 따라서 call, ret, push, pop 같은 명령어를 통해 스택 데이터를 관리할 수 있습니다.





2) RISC(Reduced Instruction Set Computer)



RISC(Reduced Instruction Set Computer)는 명령어 집합의 수를 줄여 하드웨어 구조를 간단하게 만든 CPU로서, ARM 계열의 CPU는 RISC 기반의 ISA를 사용합니다.



RISC는 짧고 규격화된 명령어를 사용하여 명령어 파이프라이닝에 유리합니다. 또한 메모리 접근을 최소화 하고 많은 범용 레지스터를 사용하므로 속도가 빠르며, 전력소모가 적고 가격이 저렴합니다.



CISC와 달리 스택 관련 명령어가 존재하지 않기 때문에 서브루틴의 return 주소나 파라미터, 지역변수 등은 소프트웨어적으로 처리해야 합니다.