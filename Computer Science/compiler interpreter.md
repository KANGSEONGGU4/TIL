## 1. 커파일러(compiler)
컴파일러(compile)는 특정 프로그래밍 언어로 쓰여있는 문서를 다른 프로그래밍 언어로 옮기는 언어 변역 프로그램을 말합니다. 예를 들어 C로 작성한 소스코드가 있다고 하면 컴파일러는 이를 어셈블리 언어와 같은 다른 언어로 번역해줍니다. 이때, C로 작성한 소스코드는 고급 프로그래밍 언어라고 하며, 어셈블리 언어는 저급 프로그래밍 언어라고 합니다. 즉, 컴파일러는 고급 프로그래밍 언어를 저급 프로그래밍 언어로 바꿔주는 역할을 하며, 컴파일 되기 전 코드를 원시코드(source code)라고 하며, 컴파일 된 이후의 코드를 목적코드(object code)라고 합니다.즉, 원시코드는 컴파일러의 인풋이 되는 것이고 목적코드는 컴파일러의 아웃풋이 되는 것입니다. 정확히 말하면 목적코드(object code)는 머신 코드(machine code)의 실행가능한 버전이라고 생각하면 됩니다.   
즉, 원시코드는 컴파일러의 인풋이 되는 것이고 목적코드는 컴파일러의 아웃풋이 되는 것입니다. 정확히 말하면 목적코드(object code)는 머신 코드(machine code)의 실행가능한 버전이라고 생각하면 됩니다.

## 2. 인터프리터(interpreter)
인터프리터(interpreter)란 프로그래밍 언어의 원시코드를 바로 실행하는 컴퓨터 프로그램을 말합니다. 앞서 원시코드는 고급 프로그래밍 언어라고 했는데, 인터프리터는 원시코드의 내용을 한번에 한줄씩 읽어들여서 실행합니다.인터프리터의 장점은 컴파일 단계를 거칠 필요가 없다는 장점이 있지만 컴파일러를 사용한 것보다 느리다는 단점이 있습니다.

## 3. 컴파일러 vs 인터프리터
컴파일러나 인터프리터 둘다 영어와 같은 인간의 언어로 작성한 코드를 컴퓨터가 이해할 수 있도록 변환시킨다는 점에서는 같습니다. 그러나 둘 사이에는 다음과 같은 차이가 있습니다.

먼저 인터프리터는 소스 코드를 한 줄씩(one statement) 해석하지만, 컴파일러는 전체 프로그램 코드(entire program code)를 스캔하고 코드 전체를 통째로 목적코드로 한번에 변환 시킵니다.

그리고 인터프리터는 소스 코드를 해석하는데는 적은 시간이 걸리지만 실행 시간은 느립니다. 반면 컴파일러는 소스코드를 해석하는데는 많은 시간이 걸리지만 실행 시간은 빠릅니다.

인터프리터 언어의 종류에는 루비, 파이썬 등이 있고 컴파일 언어의 종류에는 C, C++ 등이 있습니다.