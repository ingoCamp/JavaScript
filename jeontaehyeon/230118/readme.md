## Day1

#### JavaScript란?

**자바스크립트**는 **웹페이지에 생동감을 불어넣기 위해** 만들어진 프로그래밍 언어

***

#### 자바스크립트만의 강점
>
-   HTML/CSS와 완전히 통합할 수 있음
-   간단한 일은 간단하게 처리할 수 있게 해줌
-   모든 주요 브라우저에서 지원하고, 기본 언어로 사용됨
***
#### Hello, world!
\<script>태그엔 자바스크립트 코드가 들어간다. 브라우저는 이 태그를 만나면 안의 코드를 자동으로 처리한다.

```javascript
<body>
<script>
alert('Hello World!');
</script>
</body>
```

문장은 세미콜론으로 구별한다, 줄바꿈이 있으면 생략가능
***
#### strict mode
기존 기능 중 일부가 계선되어 use strict 라는 명령어를 사용할 때에만 변동사항이 적용되도록 하였다.
***
#### 변수
java script에서는 let을 사용하여 변수를 선언한다.

```javascript
<body>
<script>

let  a="hello a"

alert(a);

</script>
</body>
```
***
#### 상수
변화하지 않는 변수를 선언할 땐 let대신 const를 사용한다.
***
#### 문자형
**숫자형** : 정수, 부동 소수점 숫자 등의 숫자를 나타낼 때 사용한다.
**bigint** :  길이 제약 없이 정수를 나타낼 수 있다.
**문자형** : 빈 문자열이나 글자들로 이뤄진 문자열을 나타낼 때 사용한다. 단일 문자를 나타내는 별도의 자료형은 없다.
**불린형** : true, false를 나타낼 때 사용.
**null** : null 값만을 위한 독립 자료, null은 알 수 없는 값을 나타낸다.
**undefined** : undefined 값만을 위한 독립 자료형,. undefined는 할당되지 않은 값을 나타낸다.
**객체형** : 복잡한 데이터 구조를 표현할 때 사용.
**심볼형** : 객체의 고유 식별자를 만들 때 사용.
***
#### alert, prompt, confirm을 이용한 상호작용
promt 함수는 2개의 인자를 받는다.  함수가 실행되면 텍스트 메시지와 입력 필드(input field), 확인(OK) 및 취소(Cancel) 버튼이 있는 모달 창을 띄운다.

confirm 대화상자는 확인을 누르면 true 아니면 false를 반환한다.

```javascript
<body>
<script>

let  p=prompt("현재시각은?",100);

alert(p);  

let  c=confirm("안녕하세요?");

alert(c);

</script>
</body>
```
***
#### 문자열 비교
1.  두 문자열의 첫 글자를 비교.
2.  첫 번째 문자열의 첫 글자가 다른 문자열의 첫 글자보다 크면(작으면), 첫 번째 문자열이 두 번째 문자열보다 크다고(작다고) 결론 내고 비교를 종료.
3.  두 문자열의 첫 글자가 같으면 두 번째 글자를 같은 방식으로 비교.
4.  글자 간 비교가 끝날 때까지 이 과정을 반복.
5.  비교가 종료되었고 문자열의 길이도 같다면 두 문자열은 동일하다고 결론. 비교가 종료되었지만 두 문자열의 길이가 다르면 길이가 긴 문자열이 더 크다고 결론.

```javascript
alert(  'Z'  >  'A'  );true
alert(  'Glow'  >  'Glee'  );  // true  
alert(  'Bee'  >  'Be'  );  // true
```

***
#### 다른 형을 가진 값 간의 비교
숫자형으로 변환하여 비교한다.


*** 
#### nullish 병합 연산자 ??

<span style='background-color: #dcffe4'>형광펜?</span>

`a ?? b`의 평가 결과는 다음과 같다.

-   `a`가  `null`도 아니고  `undefined`도 아니면  `a`
-   그 외의 경우는  `b`
***
#### 레이블

이중 반복문이 사용됐을 때는 break만으로 빠져나올 수 없다.
이때 label을 사용하여 빠져나올 수 있음.

```javascript
_outer:_  for  (let i =  0; i <  3; i++){
  for  (let j =  0; j <  3; j++)  {
    let input =  prompt(`(${i},${j})의 값`,  '');  // 사용자가 아무것도 입력하지 않거나 Cancel 버튼을 누르면 두 반복문 모두를 빠져나옵니다.  
     if  (!input)  break outer;   
  // 입력받은 값을 가지고 무언가를 함  
     }  
  }
    alert('완료!');
```

#### 함수 표현식

```javascript
function  sayHi()  {  
alert(  "Hello"  );
  }//함수 선언문

let  sayHi  =  function()  
{  alert(  "Hello"  );
  }; //함수 표현식
```
위 두개의 코드가 동일하게 동작한다.

함수 선언문으로 선언한 코드는 선언문이 정의되기 전에도 사용할 수 있다. 하지만 함수 표현식은 실제 실행 흐름이 해당 함수에 도달했을 때 동작한다.
