# JavaScript(6) 생활코딩 56~65

## 자바스크립트의 유효범위

- 유효범위는 변수의 수명을 의미함.

- ```javascript
  var vscope = 'global';
  function fscope(){
      alert(vscope);
  }
  fscope();
  //결과 값은 global
  ```

- 함수 밖에서 변수를 선언하면 그 변수는 전역변수가 된다.

- 전역변수는 애플리케이션 전역에서 접근이 가능하다.

- ```javascript
  var vscope = 'global';
  function fscope(){
      var vscope = 'local';
      alert('함수안 '+vscope);
  }
  fscope();
  //결과값은 '함수안 local'
  alert('함수밖 '+vscope);
  //결과값은 '함수밖 global'
  ```

- 지역변수와 전역변수 모두 동시에 정의되어 있다면 지역변수를 우선시 한다.

- ```javascript
  var vscope = 'global';
  function fscope(){
      vscope = 'local';
      alert('함수안'+vscope);
  }
  fscope();
  //결과 값은'함수안 local'
  alert('함수밖'+vscope);
  //결과 값은'함수밖 local'
  
  ```

- var를 쓰지 않으면 그 변수는 전역변수가 되고 그로 인해서 모든 vscope는 local을 의미함.

## 지역변수의 사용

```javascript
function a (){
    var i = 0;
}
for(var i = 0; i < 5; i++){
    a();
    document.write(i);
}
//결과값은 01234
```

```javascript
function a (){
    i = 0;
}
for(i = 0; i < 5; i++){
    a();
    document.write(i);
}
//결과값은 무한 반복
```

## 정적유효범위

- 자바스크립트는 함수가 선언된 시점에서의 유효범위를 갖는다. 이러한 유효범위의 방식을 정적 유효범위(static scoping), 혹은 렉시컬(lexical scoping)이라고 한다. 

- ```javascript
  var i = 5;
   
  function a(){
      var i = 10;
      b();
  }
   
  function b(){
      document.write(i);
  }
   
  a();
  //결과값은 5이다.
  //함수가 정의된 시점의 i 값을 사용함.
  //함수가 사용된 시점이 아님!!!
  ```

## 값으로서의 함수

- 함수는 값이기 때문에 다른 함수의 인자로 전달 될수도 있다.

- ```javascript
  function cal(func, num){
      return func(num)
  }
  function increase(num){
      return num+1
  }
  function decrease(num){
      return num-1
  }
  alert(cal(increase, 1));
  alert(cal(decrease, 1));
  ```

- 함수는 함수의 리턴 값으로도 사용할 수 있다.

- ```javascript
  function cal(mode){
      var funcs = {
          'plus' : function(left, right){return left + right},
          'minus' : function(left, right){return left - right}
      }
      return funcs[mode];
  }
  alert(cal('plus')(2,1));
  alert(cal('minus')(2,1)); 
  ```

- 함수는 함수의 배열값으로도 사용할 수 있다.

- ```javascript
  var process = [
      function(input){ return input + 10;},
      function(input){ return input * input;},
      function(input){ return input / 2;}
  ];
  var input = 1;
  for(var i = 0; i < process.length; i++){
      input = process[i](input);
  }
  alert(input);
  //결과는 60.5
  ```

## 비동기처리(Ajax)

- 콜백은 비동기 처리에서 유용하게 사용됨.

- 콜백으로 오래걸리는 작업을 지정하면 해당 작업이 끝났을 경우 미리 등록한 작업을 실행하도록 할수 있음.

- ```javascript
  //datasource.json.js
  {"title":"JavaScript","author":"egoing"}
  ```

- ```html
  //demo1.html
  <!DOCTYPE html>
  <html>
  <head>
  <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
  </head>
  <body>
  <script type="text/javascript">
      $.get('./datasource.json.js', function(result){
          console.log(result);
      }, 'json');
  </script>
  </body>
  </html>
  ```

- 

