![alt text](<../ETC/Screenshot 2024-02-27 at 16.51.46.png>)

> ## 1. 롬(ROM)
>롬은 기억된 내용을 읽을 수만 있는 기억장치로써 일반적으로 쓰기가 불가능합니다. 또한 시스템의 전원이 꺼져도 기억된 내용이 지워지지 않는 비휘발성 메모리입니다. 실제로 롬(ROM)은 주기억장치로 사용되기보단 주로 기본 입출력 시스템, 자가 진단 프로그램 같은 변경 가능성이 없는 시스템 소프트웨어를 기억시키는데 이용됩니다.
 
### ROM은 크게 5가지 종류로 나뉩니다.

- Mask ROM : 제조 과정에서 프로그램화하여 생산한 ROM으로, 사용자가 내용을 변경시킬 수 없음.
- PROM(Program-mable ROM) : ROM에 사용자가 한번만 내용을 기록할 수 있음. 전기적 신호에 의해 기록.
- EPROM(Erasable PROM) : 사용자가 여러 번 반복해서 지우거나 기록할 수 있음. 자외선 신호에 의해 기록.
- EEPROM(Electro-nic EPROM) : 사용자가 여러 번 바녹해서 지우거나 기록할 수 있음. 전기적 신호에 의해 기록.
- EAROM(Erasable Alterable ROM) : 전기적 특성을 이용하여 기록된 정보의 일부를 바꿀 수 있음.

 
> ## 2.램(RAM)
>램은 컴퓨터의 핵심 부품으로 CPU(중앙처리장치)는 연산 작업, 보조기억장치는 각종 데이터를 보관하는 작업을 수행합니다. 자유롭게 읽고 쓸 수 있는 기억장치로, RWM(Read Write Memory)라고 부르기도 합니다. 또한 RAM에는 현재 사용 중인 프로그램이나 데이터가 저장되어 있습니다. 시스템의 전원이 꺼지면 기억된 내용이 모두 사라지는 휘발성 메모리의 특징을 가집니다. 일반적으로 주기억장치 또는 메모리라고 부르는 게 램입니다.
 

RAM은 크게 5가지 종류로 나뉩니다.

- SRAM(Static RAM) : 정적램이라 표현되며, DRAM에 비해 용량은 적으나 속도가 빠르고 가격이 비쌉니다.
- DRAM(Dynamic RAM) : 동적램이라 표현되며, 전원이 공급되어도 일정 시간이 지나면 전하가 방전되므로 주기적인 충전이 필요합니다. 전력 소모가 적고 IC집적도가 SRAM에 비해 높아서 용량은 크지만 속도가 느리며 가격이 저렴합니다.
- PSRAM(Pseudo sram) : 내부에 전하 충전회로를 내장하여 DRAM의 단점을 보완한 RAM으로써 주기적으로 전하를 충전하기 때문에 데이터 유실을 막고 SRAM처럼 사용이 가능합니다.
- SDRAM(Synchronous DRAM) : 100MHz 이상의 버스 속도를 유지하는 내장 DRAM의 일종입니다. 시스템의 클럭 속도와 동기화하여 동작함으로 CPU가 동작할 때 DRAM도 함께 동작하여 CPU가 수행할 수 있는 명령어의 양을 증가시킴으로써 효율적으로 동작합니다.
- DDR SDRAM(Double Data Rate SDRAM) : SDRAM보다 처리속도가 2배 빠른 RAM으로써 시스템버스 클럭의 Rising edge와 Falling edge를 동작시켜 같은 속도로 2배의 데이터를 보낼 수 있습니다.