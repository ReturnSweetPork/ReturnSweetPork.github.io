#  JavaScript(8) 생활코딩 76~85

## 객체

- 객체란 서로 연관된 변수를 그룹핑 한것.

- 객체 내의 변수를 프로퍼티(property)

- 객체 내의 함수를 메소드(method)

- ```javascript
  var person = {}
  person.name = 'egoing';
  person.introduce = function(){
      return 'My name is '+this.name;
  }
  document.write(person.introduce());
  ```

- 위의 코드는 객체를 만드는 과정이 분산이 되어있다.

- ```javascript
  var person = {
      'name' : 'egoing',
      'introduce' : function(){
          return 'My name is '+this.name;
      }
  }
  document.write(person.introduce());
  ```

- 위의 객체에서 다른사람의 이름을 사용할경우 객체의 정의를 다시 해야할까??

- 답은 아니다 이다. 이때 생성자 라는것을 사용한다.

## 생성자

- 생성자(constructor)는 객체를 만드는 역할을 하는 함수다.

- ```javascript
  function Person(){}
  var p1 = new Person();
  p1.name = 'egoing';
  p1.introduce = function(){
      return 'My name is '+this.name; 
  }
  document.write(p1.introduce()+"<br />");
   
  var p2 = new Person();
  p2.name = 'leezche';
  p2.introduce = function(){
      return 'My name is '+this.name; 
  }
  document.write(p2.introduce());
  ```

- 위의 코드에서 new Person() 을 통해 새로운 객체를 만들었다.

- 하지만 여러 사람의 객체를 만들경우 여러번 객체를 만들어야하는 아쉬움이 있다.

- ```javascript
  function Person(name){
      this.name = name;
      this.introduce = function(){
          return 'My name is '+this.name; 
      }   
  }
  var p1 = new Person('egoing');
  document.write(p1.introduce()+"<br />");
   
  var p2 = new Person('leezche');
  document.write(p2.introduce());
  ```

- 생성자 내에서 객체의 프로퍼티를 정의함.---> 이 과정을 통해서 코드의 재사용성이 높아짐(초기화)

- 함수에 new를 붙이는 것을 통해서 객체를 만들 수 있다는 점은 자바스크립트에서 함수의 위상을 암시하는 단서이면서 또 자바스크립트가 추구하는 자유로움을 보여주는 사례라고 할 수 있다.

## 전역객체

- ```javascript
  function func(){
      alert('Hello?');    
  }
  func();
  window.func();
  //결과값은 모두 Hello?
  ```

- 모든 전역변수와 함수는 사실 window 객체의 프로퍼티다. 

- ```javascript
  var o = {'func':function(){
      alert('Hello?');
  }}
  o.func();
  window.o.func();
  
  //결과값은 모두 Hello?
  ```

## this

-  this는 함수 내에서 함수 호출 맥락(context)를 의미한다.

- 맥락은 상황에 따라서 달라진다는것을 의미하는데 이것은 함수를 어떻게 호출하느냐에 따라서 this의 대상이 달라짐을 의미함.

- ```javascript
  function func(){
      if(window === this){
          document.write("window === this");
      }
  }
  func(); 
  //결과는 window === this
  ```

- 객체의 소속인 메소드의 this는 그 객체를 가르킨다. 

- ```javascript
  var o = {
      func : function(){
          if(o === this){
              document.write("o === this");
          }
      }
  }
  o.func(); 
  //결과는 o === this
  ```

- 함수를 호출했을 때와 new를 이용해서 생성자를 호출했을 때의 차이

- ```javascript
  var funcThis = null; 
   
  function Func(){
      funcThis = this;
  }
  var o1 = Func();
  if(funcThis === window){
      document.write('window <br />');
  }
  //결과값은 window
   
  var o2 = new Func();
  if(funcThis === o2){
      document.write('o2 <br />');
  }
  //결과값은 o2
  ```

- o1은 함수를 호출하였다. 이과정에서 함수의 호출은 this 이며 이것은 window를 가리킨다.

- o2는 생성자이며 이것은 빈객체를 만든다. 그리고 빈객체내에서  this는 만들어진 객채를 가르킨다. 즉 이것은 o2를 가르킨다고 불수있다.

- ```javascript
  function Func(){
      document.write(o);
  }
  var o = new Func();
  //결과값은 undefined
  ```

- 생성자가 실행되기 전까지는 객체는 변수에도 할당될 수 없기 때문에 this가 아니면 객체에 대한 어떠한 작업을 할 수 없기 때문이다. 

- 함수의 메소드인 apply, call을 이용하면 this의 값을 제어할 수 있다. 

- ```javascript
  var o = {}
  var p = {}
  function func(){
      switch(this){
          case o:
              document.write('o<br />');
              break;
          case p:
              document.write('p<br />');
              break;
          case window:
              document.write('window<br />');
              break;          
      }
  }
  func();
  func.apply(o);
  func.apply(p);
  //결과값
  //window
  //o
  //p
  ```

  

