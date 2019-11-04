# JavaScript(5) 생활코딩 41~55

## 자바스크립트의 모듈

- 코드의 재활용성을 높이고 유지 보수를 쉽게 할수 있는 다양한 방법들이 존재함.

- 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선됨

- 코드 수정시에 필요한 로직을 빠르게 찾는것이 가능함

- 메모리의 낭비를 줄임

- 네트워크 트래픽을 절약할수 있다.

- ```javascript
  //greeting.js
  function welcome(){
      return 'hello world'
  }
  ```

- ```javascript
  //main.html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="utf-8"/>
      <script src="greeting.js"></script>
  </head>
  <body>
      <script>
          alert(welcome());
      </script>
  </body>
  </html>
  ```

- script 태그 안쪽에 위차하는 컨텐츠는 브라우저에 의해서 자바스크립트로 인식된다.



## 자바스크립트의 라이브러리

- 라이브러리는 모듈과 비슷한 개념이다.
- 모듈이 프로그램을 구성하는 작은 부품이라면 라이브러리는 로직을 재사용하기 편리하도록 정리한 일련의 코드의 집합이다.
- 좋은 라이브러리를 잘 선택하고 잘 사용하는것이 프로그래밍의 핵심이다.
- 자바스크립트에서 가장 유명한 라이브러리는 jQuery



## 자비스크립트의 정규표현식

- 정규표현식은 문자열에서 특정한 문자를 찾아내는 도구임.

- 정규표현식의 2개 단계(컴파일->실행)

- 정규표현식을 만드는 방법(exec)

- ```javascript
  //정규표현식 리터럴
  var pattern = /a/;
  
  //정규표현식 객체 생성자
  var pattern = new RegExp('a')
  ```

- ```javascript
  var pattern = /a/;
  pattern.exec('dsdfsfssssssa');
  // 결과값은 ['a']
  ```

- ```javascript
  var pattern = /a./;
  pattern.exec('dsdfsfssssssaddd');
  // 결과값은 ['ad']
  //.은 한개의 문자이다. 그러므로 a 이후의 한개의 문자를 추가해서 출력됨
  ```

- ```javascript
  var pattern = /a/;
  pattern.exec('vdvdvddvd');
  // 결과값은 null
  //찾고자 하는 대상이 문자내에 없어서 null값을 출력
  ```

- ```javascript
  var pattern = /a/;
  pattern.test('avdvdvddvd');
  // 결과값은 true
  pattern.test('vdvdvddvd');
  // 결과값은 false
  // test는 찾는 정보가 있는지 없는지를 판별해 주는 명령어임.
  ```

- 문자열 메소드

- ```javascript
  var pattern = /a/;
  'abcdef'.match(pattern);
  //결과값은 ['a']
  'bcdef'.match(pattern);
  //결과값은 null
  ```

- ```javascript
  var pattern = /a/;
  'abcde'.replace(pattern, 'A');
  //결과값은 'Abcde'출력
  //문자열에서 패턴을 검색해서 이를 변경한 후에 변경된 값을 리턴한다.
  ```

- 정규표현식의 옵션

- ```javascript
  var xi = /a/;
  console.log("Abcde".match(xi)); // null
  var oi = /a/i;
  console.log("Abcde".match(oi)); // ["A"];
  //i를 붙이면 대소문자를 구별하지 않는다.
  ```

- ```javascript
  var xg = /a/;
  console.log("abcdea".match(xg));
  //["a"]
  var og = /a/g;
  console.log("abcdea".match(og));
  //["a","a"]
  //g를 붙이면 모든 결과를 리턴한다.
  ```

- 정규표현식 치환은 다시 공부하자....너무어렵당....ㅠ.ㅠ

