# JavaScript(4) 생활코딩 34~40

## 자바스크립트의 배열

- 배열은 array

- ```javascript
  var member = ['hyunsang','hyunjoo','hodoo']
  //배열을 선언함
  alert(member[0]);
  //결과값은 hyunsang
  alert(member[1]);
  //결과값은 hyunjoo
  alert(member[2]);
  //결과값은 hodoo
  ```

- ```javascript
  function get_member(){
      return ['hyunsang','hyunjoo','hodoo']
  }
  
  members = get_members
  
  for(var i =0; i< member.length; i++){
      document.write(member[i].toUpperCase() + '<br/>')
  }
  /*
  결과값은
  hyunsang
  hyunjoo
  hodoo
  */
  
  document.write(members[0].toUpperCase())
  //toUpperCase() 소문자를 대문자로 바꾸어 주는 함수
  ```



## 자바스크립트 배열 삽입, 삭제, 정렬

- ```javascript
  var member = ['hyunsang', 'ahn', 'hyunjoo'];
  member.push('coco')
  //데이터 삽입 
  //배열 맨 뒤에 삽입됨
  
  member.concat('coco', 'bomi')
  //복수의 데이터를 삽입할때 사용함
  //배열 맨뒤에 순서대로 삽입됨
  
  member.unshift('coco')
  //데이터를 가장 맨 앞에 삽입하고 싶을때 사용한다.
  //배열 맨 앞에 삽입됨
  
  ```

- ```javascript
  //데이터 제거
  var member = ['hyunsang', 'ahn', 'hyunjoo'];
  
  //데이터 첫번째 원소를 제거하고 싶다면
  
  member.shift()
  
  //데이터 맨 뒤 데이터를 제거하고 싶다면.
  
  member.pop()
  
  
  //데이터 정렬하고 싶다면
  member.sort()
  
  //데이터 역순 정렬
  member.reverse()
  
  //데이터를 특정한 기준에 정렬하고 싶다면.
  member.sort(sortFunction)
  //sortFunction 을 작성하여 특정 기준을 맞추어 정렬함.
  ```

- ```javascript
  var member = ['hyunsang', 'ahn', 'hyunjoo'];
  
  member.splice(인덱스, howmany, '요소')
  member.splice(1,1,'coco','bomi')
  //리턴값은 ['hyunsang', 'coco','bomi', 'hyunjoo']; 임
  
  ```



## 자바스크립트의 객체

- 객체를 만드는 방법

- ```javascript
  var grades = {'hyunsang':10, 'hyunjoo':8, 'hodoo':5}
  //'hyunsang'은 key
  //10은 value
  
  alert(grades['hyunsang'])
  alert(grades.hyunsang)
  //두개 모두 호출 가능한 방법
  ```

- ```javascript
  var grades = {'hyunsang':10, 'hyunjoo':8, 'hodoo':5}
  for(key in grades){
      document.write(key)
  }
  //키값이 리턴됨
  var grades = {'hyunsang':10, 'hyunjoo':8, 'hodoo':5}
  for(key in grades){
      document.write(grades[key])
  }
  //객체 안에 저장된 값을 찾음 즉 value가 리턴됨
  ```

- 객체 안에는 함수도 담을수 있고 객체도 담을수 있다.

- ```javascript
  var grades = {
      'list' : {'hyunsang':10, 'hyunjoo':8, 'hodoo':5},
      'show' : function(){
          alert('hello world')
          alert(this.list)
      }
  }
  
  //this는 자바 스크립트 언어에서 약속되어있는 변수이다.
  //this는 함수에 소속되어있는 현재의 객체를 나타낸다
  ```

- ```javascript
  var grades = {
      'list' : {'hyunsang':10, 'hyunjoo':8, 'hodoo':5},
      'show' : function(){
          for(var name in this.list){
              document.write(name, this.list[name])
          }
      }
  }
  
  grades.show();
  //함수의 호출
  
  ```



## 객체 지향 프로그래밍이란?

- 연관되어 있는 데이터와 처리를 하나의 객체(그릇) 안에 넣어 Grouping 해놓은 프로그래밍 기법