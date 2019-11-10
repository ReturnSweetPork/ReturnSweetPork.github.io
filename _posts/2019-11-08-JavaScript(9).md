# JavaScript(9) 생활코딩

## 상속

- 객체는 연관된 로직들로 이루어진 작은 프로그램.
- 상속은 객체의 로직을 그대로 물려받는것, 다른 객체를 만들수 있는 기능을 의미함.

```javascript
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
var p1 = new Person('hyunsang');
document.write(p1.introduce()+"<br />");

//결과 값은 My name is hyunsang
```

```javascript
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person();
 
var p1 = new Programmer('hyunsang');
document.write(p1.introduce()+"<br />");
```

- Programmer이라는 생성자를 만들고 생성자의 prototype과 Person의 객체를 연결했더니 Programmer 객체도 메소드 introduce를 사용할 수 있게 되었다. 
- Programmer가 Person의 기능을 상속하고 있음

```javascript
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.coding = function(){
    return "hello world";
}
 
var p1 = new Programmer('hyunsang');
document.write(p1.introduce()+"<br />");
document.write(p1.coding()+"<br />");

//결과값은
//My name is hyunsang
//hello world
```



## Prototype

- 프로토 타입이란 객체의 원형이다.
- 함수는 객체이다. 생성자로 사용되는 함수도 객체이다. 
- 객체는 프로퍼티를 갖는다. prototype은 용도가 약속되어있는 특수한 프로퍼티이다.

```javascript
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
Super.prototype = new Ultra();
 
function Sub(){}
Sub.prototype = new Super();
 
var o = new Sub();
console.log(o.ultraProp);
//결과값은 true
```

- 객체 o에서 ultraProp를 찾는다.
- 없다면 Sub.prototype.ultraProp를 찾는다.
- 없다면 Super.prototype.ultraProp를 찾는다.
- 없다면 Ultra.prototype.ultraProp를 찾는다.

# 표준 내장 객체의 확장

### 자바스크립트의 내장객체

- Object
- Function
- Array
- String
- Boolean
- Number
- Math
- Date
- RegExp

### 배열의 확장

```javascript
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
function getRandomValueFromArray(arr){
    var index = Math.floor(arr.length*Math.random());
    return arr[index];
}

Array.prototype.random = function(){
    var index = Math.floor(this.length*Math.random());
    return this[index]
}
//this는 배열객체 자체를 가리킴. 여기서는 arr를 가리킨다
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');

console.log(arr.random());


```

