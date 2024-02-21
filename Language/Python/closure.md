> ## 클로저 (Closure)
> - 함수 안의 함수를 결과로 반환할 때, 그 내부 함수를 '클로저(Closure)' 라고 합니다.
> - 사용되는 곳
>   - 콜백(Callback) 함수에 사용
>   - 함수의 순차적 실행
>   - 데코레이터 함수

<br>

### 1.클래스(Class) 사용하기

    class Mul:
    def __init__(self, m):
        self.m = m

    def mul(self, n):
        return self.m * n

    if __name__ == "__main__":
        mul3 = Mul(3)
        mul5 = Mul(5)

        print(mul3.mul(10)) 
        print(mul5.mul(10)) 

30   
50  

<br>

### 2.클로저(Closure) 사용하기

    def mul(m):           # 외부 함수
        def wrapper(n):   # 내부 함수 (클로저)
            return m * n
        return wrapper

    if __name__ == "__main__":
        mul3 = mul(3)    # m = 3 인 wrapper 함수가 mul3 에 저장 
        mul5 = mul(5)    # m = 5 인 wrapper 함수가 mul5 에 저장

        print(mul3(10))  # m = 3, n = 10 인 wrapper 함수가 실행
        print(mul5(10))  # m = 5, n = 10 인 wrapper 함수가 실행

30   
50 