## [컴파일러 링크](https://godbolt.org/)

~~~
#include <stdio.h>

int main(){
    int a = 10;
    int b = 20;
    int c = a + b;
    printf("%d\n", c);
    return 0;
}
~~~

### x86-64 gcc 13.2 
~~~
.LC0:
        .string "%d\n"
main:
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     DWORD PTR [rbp-4], 10
        mov     DWORD PTR [rbp-8], 20
        mov     edx, DWORD PTR [rbp-4]
        mov     eax, DWORD PTR [rbp-8]
        add     eax, edx
        mov     DWORD PTR [rbp-12], eax
        mov     eax, DWORD PTR [rbp-12]
        mov     esi, eax
        mov     edi, OFFSET FLAT:.LC0
        mov     eax, 0
        call    printf
        mov     eax, 0
        leave
        ret
~~~