## IndexError: list index out of range

```
A = []
if not A[0]:
    print("빈 배열")
```


if문의 의미는 A의 0번 인덱스가 없다면 이지만 

이 과정에서도 A의 0번 인덱스를 호출해야 하기 때문에 인덱스에러가 발생한다.

```
A = []
if not A:
    print("빈 배열")
```

```
A = []
if len(A) = 0:
    print("빈 배열")
```
