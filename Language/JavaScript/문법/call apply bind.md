## call(), apply(), bind()의 특징
- 이 3가지 기본메서드는 함수 호출 방식과 상관없이 this를 지정할 수 있습니다.
- 대부분의 경우 this의 값은 함수를 호출한 방법에 의해 결정됩니다.   실행 중에는 할당으로 설정할 수 없고 함수를 호출할 때마다 다를 수 있습니다.
- 함수를 어떻게 호출했는지 상관하지 않고 this값을 설정할 수 있는 메서드입니다.

### call() 과 apply()

call / apply this로 사용될 값, 호출할 함수의 매개변수들을 배열로 받는다.

```
const obj1 = {
    value : 'B'
}

const obj2 = {
    value : 'C'
}

function consoleValue(){
    console.log(this.value);
}

consoleValue(); // this => window
consoleValue.call(obj1); // 결과:B this => obj1
consoleValue.call(obj2); // 결과:C this => obj2
consoleValue.apply(obj1); // 결과:B this => obj1
consoleValue.apply(obj2); // 결과:C this => obj2
```

### call(), apply() 메서드의 차이
호출할 함수의 매개변수들을 배열로 담아서 처리할 경우 apply()를 사용하며, 그렇지 않을 경우 call()을 사용합니다.

```
const obj1 = {
    value : 'B'
}

const obj2 = {
    value : 'C'
}

function consoleValue(add1,add2){
    console.log(this.value, 'add1+add2 => ', add1, add2);
}

// apply()는 배열로 call()은 ','로
consoleValue.call(obj1,'오늘도','힘내자');
consoleValue.apply(obj2,['내일도','힘내자']);
```

### bind()

bind() 메서드는 call(), apply() 메서드처럼 this를 제어하지만 함수 호출을 하지 않는다. 따라서 bind() 메서드를 사용할 경우 
변수에 해당 함수를 담아서 사용합니다.

```
const obj1 = {
    value : 'B'
}

function consoleValue(add1,add2){
    console.log(this.value,'add1+add2 => ', add1, add2);
}

console.log('bind는 함수호출을 하지않는다.');
consoleValue.bind(obj1,'바인드','함수'); // this => obj1으로 바꿨지만 함수호출을하지않는다.
console.log('함수호출을 해보자')
let obj1Value = consoleValue.bind(obj1,'바인드','함수');
obj1Value();
```




