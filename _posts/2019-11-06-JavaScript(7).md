# JavaScript(7) 생활코딩 65-75

## 클로저

- 자바스크립트는 함수내에 함수를 선언가능하다.

- 이것을 내부함수라고 한다.

- ```javascript
  function outter(){
      function inner(){
          var title = 'coding everybody'; 
          alert(title);
      }
      inner();
  }
  outter();
  //결과값은 coding everybody
  ```

- ```javascript
  function outter(){
      var title = 'coding everybody';  
      function inner(){        
          alert(title);
      }
      inner();
  }
  outter();
  ```

- 위의 코드는 내부 함수에서 외부 함수의 title을 호출해도 outter함수의 지역변수에 접근 할수 있음을 보여줌.

-  클로저(closure)는 내부함수와 밀접한 관계를 가지고 있는 주제다. 

- 내부함수는 외부함수의 지역변수에 접근 할 수 있는데 외부함수의 실행이 끝나서 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근 할 수 있다. 이러한 메커니즘을 클로저라고 한다. 

- ```javascript
  function outter(){
      var title = 'coding everybody';  
      return function(){   
          alert(title); 
      }
  }
  inner = outter();
  //외부함수를 호출하였지만 내부
  inner();
  ```

-  클로저란 내부함수가 외부함수의 지역변수에 접근 할 수 있고, 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성을 의미한다. 

# arguments

-  함수에는 arguments라는 변수에 담긴 숨겨진 유사 배열이 있다 

- ```javascript
  function sum(){
      var i, _sum = 0;    
      for(i = 0; i < arguments.length; i++){
          document.write(i+' : '+arguments[i]+'<br />');
          _sum += arguments[i];
      }   
      return _sum;
  }
  document.write('result : ' + sum(1,2,3,4));
  //결과값은 10이다.
  ```

- arguments는 사실 배열은 아니다. 실제로는 arguments 객체의 인스턴스다.

## 매개변수의 수

- ```javascript
  function zero(){
      console.log(
          'zero.length', zero.length,
          'arguments', arguments.length
      );
  }
  function one(arg1){
      console.log(
          'one.length', one.length,
          'arguments', arguments.length
      );
  }
  function two(arg1, arg2){
      console.log(
          'two.length', two.length,
          'arguments', arguments.length
      );
  }
  zero(); // zero.length 0 arguments 0 
  one('val1', 'val2');  // one.length 1 arguments 2 
  two('val1');  // two.length 2 arguments 1
  ```

-  arguments.length는 함수로 전달된 실제 인자의 수를 의미하고, 함수.length는 함수에 정의된 인자의 수를 의미한다. 

