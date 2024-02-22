## 윤년
> - 4년마다 돌아오는 **2월이 29일까지 인 해** <br>

~~~
def isLeapYear(year): # 윤년이면 True, 아니면 False 를 출력하는 함수.
    return year % 4 == 0 and year % 100 != 0 or year % 400 == 0
~~~
~~~
isLeapYear(2022)
~~~
False
~~~
isLeapYear(2024)
~~~
True

<br>

~~~
import calendar
~~~
~~~
calendar.isleap(2022)
~~~
False
~~~
calendar.isleap(2024)
~~~
True
~~~
# 윤년 횟수
calendar.leapdays(1990, 2022)
~~~
8