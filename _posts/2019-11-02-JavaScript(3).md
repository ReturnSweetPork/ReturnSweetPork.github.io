# JavaScript(3) 생활코딩 22~33



## 자바스크립트의 반복문

- 자바스크립트에서 반복문은 while 문과 for 문이 있다.



## while

- 형식

- ```javascript
  while(조건){
      반복해서 실행할 코드	
  }
  ```

- ```javascript
  while(true){
      document.write('coding everybody<br/>')
  }
  ```

- 위의 코드는 무조건 참인 조건을 만족하기에 coding everybody라는 무한한 글을 출력함.

- ```javascript
  while(false){
      document.write('coding everybody<br/>')
  }
  ```

- 위의 코드는 무조건 부정이기에 어떠한 내용도 출력하지 않는다.



- ```javascript
  var i = 0
  while(i < 10){
  	document.write('coding everybody <br/>');
  	i++;
  }
  ```

- 위의 내용은 i를 0으로 지정한 뒤, 출력을 1번 할때마다 i 값을 1씩 더해주어 i 값이 9가 될때까지 총 10번 출력함.



## for

- ```
  for(초기화;, 반복조건;, 반복이 될때마다 실행되는 코드){
  	반복해서 실행할 코드    
  }
  ```

- ```javascript
  for(var i=0; i<10; i++){
  	document.write('coding everybody<br/>')    
  }
  ```

- for문은 제일 먼저 초기화를 한다. 그뒤 반복조건을 설정하고 반복이 실행될때 마다 실행할 코드를 작성한다.



## 반복문의 제어

- 반복문의 제어는 break와 continue로 진행한다.

- ```javascript
  for(var i=0; i <10; i++){
      if(i === 5){
  		break        
      }
      document.write('coding everybody'+i+ '<br/>')
  }
  ```

- ```javascript
  //위의 코드의 결과는
  ding everybody 0
  coding everybody 1
  coding everybody 2
  coding everybody 3
  coding everybody 4
  ```

- break가 실행될 경우 반복문을 즉시 종료함.

- ```javascript
  //break를 continue로 바꾸었음.
  for(var i=0; i <10; i++){
      if(i === 5){
  		continue        
      }
      document.write('coding everybody'+i+ '<br/>')
  }
  ```

- ```
  //위의 코드의 결과는
  coding everybody 0
  coding everybody 1
  coding everybody 2
  coding everybody 3
  coding everybody 4
  coding everybody 6
  coding everybody 7
  coding everybody 8
  coding everybody 9
  ```

- i의 값이 5가 되었을 때 실행이 중단 됐기 때문에 continue 이후의 구문이 실행되지 않은 것이다. 하지만 반복문은 중단되지 않았기 때문에 나머지 결과가 출력된 것이다.

## 반복문의 중첩

- ```javascript
  for(var i = 0; i < 10; i++){
      for(var j =0; j <10; j++){
          document.write(str(i)+str(j)+'<br/>')
      }
  }
  ```

- 위의 결과로 00~ 99까지의 값을 얻을수 있다.



## 자바스크립트의 함수

- 함수는 코드의 재사용성을 증가시켜준다.

- ```
  function 함수명(인자){
      코드
      return 반환값
  }
  ```

- ```javascript
  function numbering(){
      i = 0;
      while(i <10){
  		document.write(i);
          i += 1;
      }
  }
  
  numbering();
  // 함수 실행의 결과는 012345676789
  ```

- ```javascript
  function get_member1(){
      return 'egoing';
  }
   
  function get_member2(){
      return 'k8805';
  }
  
  function get_member(){
      return 'egoing';
      return 'k8805';
      return 'sorialgi';
  }
  
  
  alert(get_member1());
  alert(get_member2());
  alert(get_member());
  //결과값은 egoing 과 k8805가 각각출력된다.
  //마지막 함수는 egoing 만 출력한다. 그 이유는 함수가 이미 egoing 출력한뒤 함수가 종료되었기 때문이다.
  ```



## 자바스크립트의 함수 인자

- 인자란 함수로 유입되는 입력값을 칭한다(argument)

- ```javascript
  function get_argument(arg){
  	return arg;    
  }
  
  alert(get_argument(1));
  alert(get_argument(2));
  ```



![1572744087454](C:\Users\안현상\AppData\Roaming\Typora\typora-user-images\1572744087454.png)



- ```javascript
  function get_arguments(arg1, arg2){
      return arg1 + arg2
  }
   
  alert(get_arguments(10, 20));
  alert(get_arguments(20, 30));
  //결과 값은 30,50
  ```



![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/743/1515.gif)

## 자바스크립트 함수를 정의하는 여러가지 방법

```javascript
//첫번째 기존 함수 정의 방법
function numbering(){
    i = 0;
    while(i < 10){
          document.write(i);
          i += 1;
    }
}

numbering();


//두번째 함수 정의 방법
var numbering = function(){
    i = 0;
    while(i<10){
          document.write(i);
          i+=1;
    }
}
numbering();


//3번째 직접 실행방법
(function(){
    i=0;
    while(i<10){
          document.write(i)
          i+=1;
    }
})();

//3번째 함수는 직접 호출한다.



```





