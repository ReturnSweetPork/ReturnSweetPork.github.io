# JavaScript(1) 생활코딩 1~10



## 자바스크립트란.

- 웹페이지를 동적으로 제어하기 위해서 고안된 언어



## 자바스크립트의 실행

1. 웹페이지에서 자바스크립트 작성

```html
##메모장
##helloworld.html

<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body>
        <script>
            alert('Hello world');
        </script>
    </body>
</html>
```



2. 크롬개발자 도구 사용

- 크롬브라우저 F12버튼을 통해 개발자 도구 실행
- console창을 통해서 명령어 실행





## 자바스크립트의 숫자

```javascript
alert(1+1);   //2
alert(1.2+1.3);    ///2.5
alert(2*5);      //10
alert(6/2);      //3

Math.pow(3,2)   //9   3의 2승
Math.round(10.6)   //11, 10.6을 반올림
Math.ceil(10.2) //11, 10.2를 올림
Math.floor(10.2) // 10, 10.2를 내림
Math.sqr(9) //3 , 3의 제곱근
Math.random() /// 0부터 1.0 사이의 숫자
```



## 자바스크립트의 문자

```javascript
alert('coding everybody')
alert("coding everybody")
alert('hyunsang's coding') // 에러메세지 출력됨, 이경우 \를 추가하면 에러없이 출력가능
alert('hyunsang\'s coding')

alert('hyunsang \n coding') //여러줄의 출력
alert('hyunsang' + 'coding') // 문자에도 연산자 적용가능
alert('hyunsang coding'.length) // 결과는 15

```



## 자바스크립트의 변수

```javascript
var a = 1
alert(a+1); //2

var a = 2
alert(a+1); //3

var a = 'first'


alert(a+'everybady') // 'first everybody'


```

