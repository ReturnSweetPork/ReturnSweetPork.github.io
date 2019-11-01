# JavaScript(2) 생활코딩 11~21



### 자바스크립트에서의 주석

- // 슬래쉬 두개는 주석으로 처리함

- 여러줄의 주석을 할 경우

- ```javascript
  /*
  여러줄의
  주석을 
  사용함
  */
  
  
  ```

### 자바스크립트에서의 세미콜론

- 세미콜론은 명령이 끝났음을 알린다.
- 줄바꿈도 같은 역할을 함.
- 같은줄에 2개의 명령어를 써야할 경우가 생길수 있음
- 그러므로 각 명령어의 끝마다 세미콜론을 써주는 습관을 갖는게 좋다.



### 자바스크립트의 연산자

- = 대입연산자
- ==동등연산자
- === 일치연산자(완벽하게 정확)

```javascript
var a; // undefined
var b = null; // null
alert(a==b); // true
alert(a===b); // false


alert(true == 1); //true
alert(true === 1); //false
alert(0===-0); //true
alert(NaN === NaN); //false
```

- != 부정을 의미한다.

- 부정은 같지 않다를 의미함.

- !== 정확하게 같지 않다를 의미한다.



### 자바스크립트의 조건문

- 조건문의 시작은 if
- if(조건문의 기준이 되는 내용){조건이 맞다면 진행되는 코드}

- 아이디의 조건이 맞다면 '아이디가 일치합니다 ' 코드가 실행됨
- 아이디의 조건이 맞지 않다면 ' 아이디가 일치하지 않습니다' 코드실행

```javascript
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<script>
		id = prompt('아이디를 입력해 주세요');
		if(id=='hyunsang'){
			alert('아이디가 일치합니다.')
		} else{
			alert('아이디가 일치하지 않습니다.')
		}
	</script>
</body>
</html>
```



- if 문 안쪽에 if 문이 있는경우
- 아이디 일치 후, 패스워드 조건문이 실행
- 패스워드 조건문을 일치할 경우 '로그인하였습니다 000님 반가워요' 코드 실행
- 아이디는 일치하였으나 패스워드가 불일치 할 경우 '비밀번호 틀림' 코드실행
- 아이디가 일치하지 않는경우  ' 아이디가 일치하지 않습니다' 코드실행

```javascript
<!DOCTYPE html>
<html>
<head>
	<title>	</title>
</head>
<body>

	<script>
		id = prompt('아이디를 입력해 주세요');
		if(id=='hyunsang'){
			var password = prompt('비밀번호를 입력해 주세요')
			if(password == '11111'){
				alert('로그인하였습니다.' + id + '님 반가워요')
			}else{
				alert('비밀번호 틀림 돌아가세요.')
			}
	} else{
			alert('아이디가 일치하지 않습니다.')
	}
	</script>
</body>
</html>
```



### 자바스크립트의 논리 연산자

- &&  좌항 우항 모두 참일때 참이다 (and  기능)
- 아이디와 패스워드 모두 참일때 '로그인 하였습니다' 코드 실행
- 아이디 패스워드 둘중 하나라도 일치하지 않을 경우 '아이디 또는 비밀번호가 틀렸습니다' 코드 실행

```javascript
<!DOCTYPE html>
<html>
<head>
	<title>	</title>
</head>
<body>
	<script>
		var id = prompt('아이디를 입력해 주세요');
		var password = prompt('비밀번호를 입력해 주세요');
		if(id=='hyunsang' && password === '111111){
				alert('로그인하였습니다.' + id + '님 반가워요');
			} else {
				alert('아이디 또는 비밀번호가 틀렸습니다..');
			}
	</script>
</body>
</html>
```

- || 좌항 우항 둘중 하나만 일치하면 참임(or 기능)
- 아이디는 3개중 1개만 일치하고 패스워드가 일치할 경우에 '인증했습니다 코드 실행'
- 아이디 또는 패스워드가 틀릴경우 '인증에 실패하였습니다' 코드 실행

```javascript
var id = prompt('아이디를 입력해주세요.');
var password = prompt('비밀번호를 입력해주세요.');
if((id==='egoing' || id==='k8805' || id==='sorialgi') && password==='111111'){
    alert('인증 했습니다.');
} else {
    alert('인증에 실패 했습니다.');
}
```

