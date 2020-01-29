# Arrow Function(화살표 함수)

- ES6문법으로 새로 등장한 함수임.
- function 키워드를 통해서 함수를 만드는 것 보다 쉽게 함수를 표현가능함.

```javascript
//일반 함수의 경우
var foo = function (){ console.log('foo')}
//결과값 'foo'

//화살표 함수의 경우
var bar =() => console.log('bar')
//결과값 'bar'
```



## 화살표 함수의 기본 문법

```javascript
//매개변수가 없는 경우
var foo = () => console.log('bar')
foo()
//결과는 bar

//매개변수가 하나인 경우
var foo = x => x
foo('bar')
//결과는 bar

//매개변수가 여러개인 경우
var foo (a,b) = (a+b) => a + b
var foo (a,b) = (a+b) => {return a+b}
foo(1,2)
//결과값은 3

var foo (a,b) = (a+b) => {a+b}
foo(1,2)
//결과값은 undefined
//{}을 사용하면 값을 반환할때 return을 사용해야 함.
//{}을 사용하지 않으면 undefined를 반환함

//객체 반환시
var foo = () => ({ a : 1, b: 2, c: 3})
foo()
//결과는 { a : 1, b: 2, c: 3}


```

